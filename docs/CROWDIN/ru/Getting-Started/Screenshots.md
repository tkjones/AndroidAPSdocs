# Экраны AAPS

## Главный экран

![Главный экран V2.7](../images/Home2020_Homescreen.png)

Это первый экран, который вы увидите при открытии приложения AAPS. Он отображает почти всю необходимую вам изо дня в день информацию.

### Раздел А - Вкладки

* Переход между различными модулями AAPS.
* Между экранами можно также переходить свайпом влево или вправо.
* Отображаемые здесь вкладки можно выбрать в [Конфигураторе](Config-Builder-tab-or-hamburger-menu).

(Screenshots-section-b-profile-target)=

### Раздел B - Профиль & Цель

#### Текущий профиль

![Оставшееся время замененного профиля](../images/Home2020_ProfileSwitch.png)

* Текущий профиль отображается на левой панели.
* Короткое нажатие открывает подробности о текущем профиле
* Долгое нажатие позволяет [переключаться между разными профилями](Profiles-profile-switch).
* Если профиль был изменен на время - в скобках отображается оставшееся время его активности в минутах.

#### Целевое значение ГК (Цель)

![Оставшаяся продолжительность временной цели](../images/Home2020_TT.png)

* Текущее целевое значение глюкозы крови (ГК) отображается на правой панели.
* Короткое нажатие позволяет установить [временную цель](../Usage/temptarget.md).
* Если установлена временная цель - панель будет желтой, в скобках отображается оставшееся время ее активности в минутах.

(Screenshots-visualization-of-dynamic-target-adjustment)=

#### Визуализация динамического изменения цели

![Визуализация динамического изменения цели](../images/Home2020_DynamicTargetAdjustment.png)

* AAPS может динамически изменять установленную цель основываясь на чувствительности, если используется алгоритм СМБ (SMB).
* Активируйте одну или обе [настройки](Preferences-openaps-smb-settings): 
   * "чувствительность повышает цель" и/или 
   * "сопротивляемость понижает цель" 
* Если AAPS обнаружит повышенную сопротивляемость или чувствительность - цель будет изменена. 
* При таком изменении панель будет зеленой.

### Раздел C - ГК & статус петли

#### Текущий уровень глюкозы крови

* Последнее значение ГК, переданное вашим НМГ, отображается в левой части экрана.
* Цвет показаний ГК соответствует настроенному [даипазону](Preferences-range-for-visualization): 
   * зеленый = в заданном диапазоне
   * красный = ниже заданного диапазона
   * желтый = выше заданного диапазона
* Серый блок по центру экрана отображает изменение текущего уровня ГК относительно предыдущего показания и изменение за последние 15 и 40 минут.

(Screenshots-loop-status)=

#### Статус цикла

![Статус цикла](../images/Home2020_LoopStatus.png)

* Новые иконки отображают статус цикла:
   
   * зеленый круг = активен замкнутый цикла
   * зеленый круг с пунктирной линией =[приостановка помпы на низкой ГК (LGS)](Objectives-objective-6-starting-to-close-the-loop-with-low-glucose-suspend)
   * красный круг = цикл деактивирован (постоянно отключен)
   * желтый круг = цикл приостановлен (временно приостановлен, но базальный инсулин будет подаваться) - оставшееся время паузы отображается под иконкой
   * серый круг = помпа отключена (временно отключена любая подача инсулина) - оставшееся время остановки отображается под иконкой
   * оранжевый круг = запущен суперболюс - оставшееся время отображаешься под иконкой
   * синий круг с пунктирной линией = активен открытый цикл

* Короткое или длинное нажатие на иконку откроет диалоговое окно для переключения между режимами цикла (Закрытый, Приостановка на низкой ГК, Открытый или Отключен), для отключения / возобновления цикла или отключения / подключения помпы обратно.
   
   * Если диалоговое окно было вызвано коротким нажатием - после смены режима появится запрос на подтверждение. Если долгим нажатием - смена режима применится сразу.
   
   ![Меню состояния цикла](../images/Home2020_Loop_Dialog.png)

(Screenshots-bg-warning-sign)=

#### Восклицательный знак возле ГК

Beginning with Android 3.0, you might get a warning signal beneath your BG number on the main screen.

*Примечание*: AAPS учитывает данные за 30 часов в своих расчетах. Поэтому даже после устранения проблемы нерегулярной передачи данных, может потребоваться до 30 часов, чтобы исчез желтый треугольник.

Чтобы немедленно удалить его, вам нужно вручную удалить несколько записей из вкладки Dexcom/xDrip+.

Однако если задублированных данных много, может быть проще сделать следующее:

* [создать резервную копию настроек](../Usage/ExportImportSettings.md),
* сбросить базу данных в меню обслуживания и
* заново [импортировать настройки](../Usage/ExportImportSettings.md)

##### Красный восклицательный знак: Задублированные данные ГК

Красный предупреждающий знак служит сигналом для немедленных действий: поступают дублирующиеся данные ГК, не позволяющие правильно работать алгоритму цикла. Поэтому замкнутый цикл будет отключен до устранения проблемы.

![Red BG warning](../images/bg_warn_red.png)

Следует выяснить, почему данные ГК дублируются:

* Активирован ли мост Dexcom на вашем сайте NS? Отключите мост, перейдя в Heroku (или к другому провайдеру хостинга), отредактируйте переменную «enable» и удалите "bridge". (Для Heroku [подробности можно найти здесь](https://nightscout.github.io/troubleshoot/troublehoot/#heroku-settings).)
* Данные о ГК передаются в ваш Nightscout (NS) с нескольких источников? Если вы используете самостоятельно собранное приложение BYODA, включите загрузку в AAPS, но не включайте её в xDrip+.
* Есть ли подписчики, фоловеры, которые могут получать вашу ГК и также снова передавать ее на ваш сайт NS?
* Последний вариант: В AAPS перейдите в настройки NS Client выберите настройки синхронизации и отключите опцию "Принимать данные CGM из NS".

##### Желтый восклицательный знак

* Желтый сигнал предупреждения указывает, что значения вашей ГК получены через нерегулярные промежутки времени или имеются пропуски значений.
   
   ![Yellow BG warning](../images/bg_warn_yellow.png)

* Обычно предпринимать никаких действий не требуется. Замкнутый цикл продолжит работать!

* Так как замена сенсора изменяет поток данных, предупреждающий знак после смены - явление нормальное и не должно вызывать беспокойства.
* Специально для пользователей libre:
   
   * Каждый сенсор libre пропускает данные раз или два в несколько часов, а это означает, что идеального потока значений ГК не получится.
   * Непрерывный поток также нарушается скачками данных.
   * Поэтому желтый предупреждающий знак будет «всегда включен» для пользователей libre.

### Раздел D - АктИнс, АктУгл, БС и AS

![Раздел D](../images/Home2020_TBR.png)

* Иконка шприца: инсулин "на борту" (IOB, АктИнс) - количество активного инсулина в теле
   
   * Значение активного инсулина IOB будет равно нулю, если активна только база текущего профиля и нет остаточного инсулина от предыдущих болюсов. 
   * IOB может быть отрицательным если был период с пониженным относительно текущего профиля базалом.
   * Нажмите на иконку (только короткое нажатие), чтобы увидеть как IOB распределяется между базой и болюсом.

* Иконка колоска: [углеводы "на борту"](../Usage/COB-calculation.md) (COB, АктУгл) - количество еще не усвоенных углеводов из тех, чтоб были введены ранее. Иконка мерцает, если необходимо съесть дополнительные углеводы.

* Иконка с фиолетовой линией: базальная скорость (BR, БС) - иконка изменяется в соответствии с текущими настройками базала (прямая линия при базе 100%) 
   * Кратко нажмите на иконку, чтобы увидеть подробности базала (значение текущего базала, время начала, остаток/общая продолжительность в минутах)
* Иконка со стрелками вверх и вниз: отображает статус [Автосенса](Open-APS-features-autosens) (AS) (включен или отключен) и текущий расчет под иконкой

#### Требуются углеводы

![Требуются углеводы](../images/Home2020_CarbsRequired.png)

* Требование углеводов появляется, когда расчеты определяют их недостаток.
* Это происходит, когда алгоритм Oref думает: "Я не спасу тебя отключением всего инсулина и тебе необходимы углеводы, чтобы не загиповать". 
* Уведомления об углеводах значительно сложнее, чем уведомления калькулятора болюса. Вы можете увидеть требование углеводов даже когда калькулятор болюса не показывает их нехватку.
* При желании уведомления об углеводах могут быть переданы в Nightscout. В этом случае сработают стандартные настройки оповещения NS. 

### Раздел E- Индикаторы состояния

![Раздел E](../images/Home2020_StatusLights.png)

* Индикаторы состояния сообщают: 
   * сколько времени прошло с момента установки канюли
   * сколько времени прошло с момента установки резервуара
   * об уровне заполнения резервуара (в единицах)
   * сколько времени отработал сенсор
   * сколько времени прошло с замены батареи и об уровне ее заряда (%)
* Если превышено пороговое значение, данные показываются желтым цветом.
* Если превышено критическое пороговое значение, значения будут показаны красным цветом.
* Установить пороговые значения можно в [настройках](Preferences-status-lights).

(Screenshots-section-f-main-graph)=

### Раздел F - Основной график

![Раздел F](../images/Home2020_MainGraph.png)

* График показывает уровень глюкозы в крови (ГК) считываемый с мониторинга глюкозы (CGM). 
* Здесь показаны заметки, введенные на вкладке действия, такие как калибровка с глюкометра и записи углеводов, а также переключения профиля. 
* Длительное нажатие на графике изменит его масштаб. Можно выбрать отображение последних 6, 8, 12, 18 или 24 часов.
* Зеленая область отражает ваш целевой диапазон. Его можно задать в [настройках](Preferences-range-for-visualization).
* Голубые треугольники показывают [СМБ](Open-APS-features-super-micro-bolus-smb) - если они активированы в [настройках](Preferences-openaps-smb-settings).
* Дополнительная информация:
   
   * Прогнозирование
   * Базал
   * Нагрузка - кривая действия инсулина

#### Активация дополнительной информации

* Щелкните по треугольнику в правой части основного графика, чтобы выбрать, какая информация будет показана на главной диаграмме.
* Для главного графика доступны три варианта выше строки "\---\---- График 1 \---\----".
   
   ![Настройка главного графика](../images/Home2020_MainGraphSetting.png)

(Screenshots-prediction-lines)=

#### Линии прогнозирования

* **Оранжевая** линия: [АктУгл (COB)](../Usage/COB-calculation.md) (цвет используется для представления активных углеводов COB и углеводов в целом)
   
   Линия предсказания показывает, где будет ГК (а не сами активные углеводы COB) на основе текущих настроек помпы с учетом того, что отклонения вследствие усвоения углеводов останутся постоянными. Эта линия появляется только при известном наличии активных углеводов COB.

* **Темно-синяя** линия: активный инсулин IOB (цвет обычно используется для отображения активного инсулина IOB и инсулина)
   
   Линия предсказания показывает, что будет происходить только под воздействием инсулина. Например, если вы ввели инсулин, а потом не ели никаких углеводы.

* **Голубая** линия: нулевой временный базал (предсказанная ГК, если будет установлена временная базальная скорость в 0%)
   
   В строке прогноза показано, как изменится линия траектории активного инсулина IOB, если помпа прекратит подачу инсулина (0% TBR).
   
   *Эта линия появляется только когда используется алгоритм [СМБ](Preferences-advanced-meal-assist-ama-or-super-micro-bolus-smb).*

* **Темно-желтая** линия: [непредвиденный прием пищи UAM](Sensitivity-detection-and-COB-sensitivity-oref1)
   
   Незапланированный прием пищи - обнаружение значительного повышения уровня глюкозы, как следствие приема пищи, выброса адреналина или других факторов. Линия предсказания аналогична оранжевой линии активных углеводов COB, но предполагает, что отклонения будут понижаться с постоянной скоростью (за счет увеличения текущей скорости сокращения).
   
   *Эта линия появляется только когда используется алгоритм [СМБ](Preferences-advanced-meal-assist-ama-or-super-micro-bolus-smb).*

* **Темно-оранжевая** линия: aCOB (ускоренное усвоение углеводов)
   
   Аналогично COB, но скорость усвоения углеводов считается постоянной и равной 10 мг/дл/5м (-0.555 ммоль/л/5м). Устарело и имеет ограниченную полезность.
   
   *Линия появляется только когда используется старый алгоритм [AMA](Preferences-advanced-meal-assist-ama-or-super-micro-bolus-smb).*

Обычно реальная кривая глюкозы находится где-то между этих линий, или близка к той, которая ближе всего описывает вашу текущую ситуацию.

#### Базал

* **Сплошная синяя** линия показывает базальную скорость помпы и отражает фактическую подачу инсулина с течением времени.
* **Пунктирная синяя** линия - это базальная скорость из профиля, если бы не было временных изменений базальной скорости (ВБС).
* При стандартной базальной скорости область под линией показывается в темно-синем цвете.
* Когда базальная скорость временно изменяется (увеличивается или уменьшается), область под линией отображается в светло-синем цвете.

#### Нагрузка

* **Тонкая желтая** линия отображает активность инсулина. 
* Она основана на ожидаемом падении ГК из-за действия инсулина в системе, если не присутствуют другие факторы (например, углеводы).

### Раздел G - Дополнительные графики

* Можно активировать до четырех дополнительных графиков ниже главного графика.
* Чтобы настроить дополнительные графики - щелкните по треугольнику справа от [главного](Screenshots-section-f-main-graph) и прокрутите вниз.

![Дополнительные параметры графика](../images/Home2020_AdditionalGraphSetting.png)

* Для добавления дополнительного графика установите флажок с левой стороны его названия (например, \---\---- Граф 1 \---\----).

#### Абсолютный инсулин

* Активный инсулин, включая болюсный **и базальный**.

#### Активный инсулин (IOB)

* Показывает инсулин, который вы имеете "на борту" (= активный инсулин в вашем теле). Он включает инсулин болюсов и временного базала (**но исключает базальную скорость, установленную в вашем профиле**).
* Если бы не было [СМБ](Open-APS-features-super-micro-bolus-smb), болюсов, и ВБС во время действия инсулина DIA, он равнялся бы нулю.
* Активный инсулин IOB может быть отрицательным, если у не осталось ни болюсов, ни нулевого/низкого временного базала в течение более длительного времени чем DIA.
* Усвоение инсулина зависит от времени его действия [DIA и настроек профиля инсулина](Config-Builder-local-profile). 

#### Активные углеводы (COB)

* Показывает активные углеводы в организме (= еще не усвоенные углеводы). 
* Усвоение активного инсулина зависит от отклонений, замеченных алгоритмом. 
* Если обнаружится более быстрое усвоение углеводов, чем ожидалось, будет подан инсулин, и это увеличит количество активного инсулина IOB (с учетом настроек безопасности). 

#### Отклонения

* **СЕРЫЕ** столбцы показывают отклонение, вызванное углеводами. 
* **ЗЕЛЕНЫЕ** столбцы показывают, что ГК превышает уровень, ожидаемый алгоритмом. Зеленые столбцы используются для увеличения сопротивления в [Autosens](Open-APS-features-autosens).
* **КРАСНЫЕ** столбцы показывают, что ГК ниже величины, ожидаемой алгоритмом. Красные столбцы используются для увеличения чувствительности в [Autosens](Open-APS-features-autosens).
* **ЖЕЛТЫЕ** столбцы показывают отклонение, вызванное непредвиденным приемом пищи UAM.
* **ЧЕРНЫЕ** столбцы показывают небольшие отклонения, не принятые во внимание при расчете чувствительности

#### Чувствительность

* Показывает чувствительность, обнаруженную алгоритмом [Autosens](Open-APS-features-autosens). 
* Чувствительность - это расчет чувствительности к инсулину в результате нагрузки, гормонов и т.д.

#### Нагрузка

* Показывает активность инсулина, рассчитанную на основе профиля инсулина (не производная от активного инсулина). 
* Значение выше ближе к пику времени действия.
* Это будет означать, что при снижении IOB величина будет отрицательной. 

#### Линия отклонения

* Внутреннее значение, используемое в алгоритме.

### Раздел H - Кнопки

![Кнопки главного экрана](../images/Home2020_Buttons.png)

* Кнопки инсулина, углеводов и калькулятора почти 'всегда активны'.
   
   * При потере подключения к помпе кнопка инсулина не видна.

* Отображение других кнопок можно задать в Настройках \[preferences\] (п.м. Начало - Кнопки).

#### Инсулин

![Кнопка инсулина](../images/Home2020_ButtonInsulin.png)

* Подает заданное количество инсулина без использования [калькулятора болюса](Screenshots-bolus-wizard).
* Можно автоматически начать [ВЦ Ожидаемый прием пищи](Preferences-default-temp-targets), поставив флажок рядом с этой опцией.
* Если не хотите подавать болюс с помпы, а только сделать запись о введенном инсулине (например, поданного шприц-ручкой), поставьте флажок рядом с соответствующей опцией.

#### Углеводы

![Кнопка углеводов](../images/Home2020_ButtonCarbs.png)

* Делает запись об углеводах без подачи болюса.
* Можно активировать [заранее настроенную временную цель](Preferences-default-temp-targets) поставив рядом с ней флажок.
* Смещение по времени: сколько минут пройдет до момента начала приема пищи (или уже прошло с этого момента).
* Длительность действия: для ["растягивания" углеводов](../Usage/Extended-Carbs.md)
* Можно использовать кнопки для быстрого приращения количества углеводов.
* Примечания будут загружены в Nightscout - в зависимости от ваших настроек [клиента NS](Preferences-nsclient).

#### Калькулятор

* Смотрите раздел "Мастер Болюса" [ниже](Screenshots-bolus-wizard)

#### Калибровки

* Отправляет калибровку в xDrip+ или открывает диалог калибровки Dexcom.
* Активируется в [настройках](Preferences-buttons).

#### CGM / НМГ

* Открывает xDrip+.
* Кнопка Назад возвращает в AAPS.
* Активируется в [настройках](Preferences-buttons).

#### Мастер быстрых настроек

* Быстрый ввод заранее заданного количества углеводов с предварительно настроенными параметрами расчета дозы.
* Параметры задаются в [настройках](Preferences-quick-wizard).

(Screenshots-bolus-wizard)=

## Мастер Болюса

![Мастер Болюса](../images/Home2020_BolusWizard_v2.png)

Чаще всего вы будете вводить болюс на еду именно отсюда.

### Раздел I

* Поле ГК обычно уже заполнено данными с мониторинга. Если мониторинг ГК не работает, то поле будет пустым. 
* В поле УГЛЕВОДЫ вводим рассчитанное нами количество углеводов - или эквивалент - на которое хотим дать болюс. 
* Поле КОРРЕКЦИЯ - для корректировки, если вы по какой-либо причине хотите изменить конечную дозу.
* Поле CARB TIME предназначено для предварительной подачи болюса, так что вы можете сообщить системе о задержке в приеме углеводов. Вы можете добавить отрицательное число в это поле, если даете болюс на прошлые углеводы.

(Screenshots-eating-reminder)=

#### Напоминание о приеме пищи

* Для напоминания о "будущих" углеводах можно поставить флажок в поле рядом с иконкой будильника (флажок поставится автоматически, если вы указали время в будущем), в этом случае в указанное время сработает оповещение о необходимости начать есть заведенные в AAPS углеводы
   
   ![Мастер болюса с напоминанием о питании](../images/Home2021_BolusWizard_EatingReminder.png)

### Раздел J

* СУПЕРБОЛЮС означает, что к обычной дозе вводимого сейчас болюса будет добавлена база следующих 2 часов, а ВБС на это время будет установлен в ноль, чтобы компенсировать этот дополнительный инсулин. Эта опция появляется только если отмечена опция "активировать [суперболюс](Preferences-superbolus)" в [настройках Начало](Preferences-overview).
* Идея заключается в том, чтобы доставить инсулин по возможности раньше и, желательно, сократить пики.
* Подробная информация находится на сайте [diabetesnet.com](https://www.diabetesnet.com/diabetes-technology/blue-skying/super-bolus/).

### Раздел K

* Показывает рассчитываемый болюс. 
* Если количество активного инсулина превышает рассчитанный болюс, то оно просто покажет количество углеводов, которые еще требуются.
* Примечания будут загружены в Nightscout - в зависимости от ваших настроек [клиента NS](Preferences-nsclient).

### Раздел L

* Подробности расчёта мастера болюса.
* Можно отменить выбор того, что не хотите включить, но обычно это не требуется.
* По соображениям безопасности блок **TT должен быть отмечен вручную**, если вы хотите, чтобы калькулятор болюса отталкивался от действующей временной цели.

#### Комбинации активных углеводов COB и активного инсулина IOB и что они означают

* По соображениям безопасности галочка активного инсулина IOB не может быть снята когда отмечены активные углеводы COB, из-за риска передозировки инсулина, так как AAPS не может заново пересчитать то, что уже дано.
* Если отметить галочками COB и IOB, то будут учтены неусвоенные углеводы которые еще не покрыты инсулином + все инсулины, которые были введены в качестве временного базала или супермикроболюса SMB.
* Если вы нажимаете IOB без COB, AAPS принимает в расчет уже поданный инсулин, но не углеводы, которые предстоит усвоить. Это приводит к уведомлению о "недостатке углеводов".
* Если подается болюс на ** дополнительную еду** вскоре после болюса на прием пищи (напр. дополнительный десерт) полезно **снять все галочки**. Таким образом, добавляются только новые углеводы а поскольку основная еда не еще не усвоена, то IOB не будет точно соответствовать углеводам COB вскоре после болюса на еду.

(Screenshots-wrong-cob-detection)=

#### Неверное обнаружение активных углеводов COB

![Медленное усвоение углеводов](../images/Calculator_SlowCarbAbsorption.png)

* Если после использования мастера болюса вы видите сообщение выше, то AAPS обнаружил, что рассчитанное значение активных углеводов может быть неправильным.
* Так что, если вы хотите повторно подать болюс после предыдущей еды с активными углеводами, учитывайте возможность передозировки! 
* Подробнее см. подсказки на [странице расчета активных углеводов СOB](COB-calculation-detection-of-wrong-cob-values).

(Screenshots-action-tab)=

## Вкладка "Действия"

![Вкладка "Действия"](../images/Home2021_Action.png)

### Действия-раздел M

* Кнопка [переключение профиля](Profiles-profile-switch) является альтернативой нажатию [текущий профиль](Screenshots-section-b-profile-target) на главном экране.
* Кнопка [временная цель](temptarget-temp-targets) - альтернатива [текущей цели](Screenshots-section-b-profile-target) на главном экране.
* Кнопка начала или отмены временного базала. Обратите внимание, что кнопка меняется с “TEMPBASAL” (ВРЕМБАЗАЛ) на “CANCEL x%” (ОТМЕНА х%), после начала действия.
* Несмотря на то, что [пролонгированные болюсы](Extended-Carbs-extended-bolus-and-why-they-wont-work-in-closed-loop-environment) действительно не работают в замкнутом цикле, некоторые всё равно просили оставить эту опцию.
   
   * Эта опция доступна только для помпDana RS и Insight. 
   * Замкнутый цикл автоматически будет остановлен и переключится на режим открытого цикла на время пролонгированных болюсов.
   * Не забудьте прочитать [детали](../Usage/Extended-Carbs.md) перед использованием этой опции.

(Screenshots-careportal-section-n)=

### Портал терапии-раздел N

* Отображает информацию о
   
   * время, отработанное сенсором & уровень заряда (процент заряда батареи)
   * время нахождения инсулина в картридже & уровень (единицы)
   * отработанное время (возраст) катетера помпы
   * время, отработанное батареей (аккумулятором) помпы & уровень заряда (процент

* Будет показано меньше информации, если используется [ низкое разрешение экрана](Preferences-skin).

(Screenshots-sensor-level-battery)=

#### Уровень заряда сенсора (батарея)

* Требуется xDrip+ ночная сборка от декабря 10, 2020 или новее.
* Работает в мониторинге с дополнительным передатчиком, например MiaoMiao 2. (Датчик должен послать информацию об уровне батареи на xDrip+.)
* Пороговые значения могут быть заданы в [настройках](Preferences-status-lights).
* Если уровень батареи сенсора совпадает с уровнем заряда аккумулятора телефона, то версия xDrip+, вероятно, слишком старая и нуждается в обновлении.
   
   ![Уровни сенсоров равны уровню батареи телефона](../images/Home2021_ActionSensorBat.png)

### Портал терапии-раздел О

* Контроль ГК, заполнение инфузионного набора, установка сенсора и замена батареи помпы - основные данные в [разделе N](Screenshots-careportal-section-n).
* Кнопка Заполнение инфузионного набора позволяет регистрировать смену места катетера помпы, а также замену картриджа инсулина.
* Раздел O отражает состояние портала терапии сайта Nightscout. Так что упражнения, объявление и вопрос являются специальными формами заметок.

### Инструменты - раздел P

#### Просмотр логов

* Позволяет перемещаться по журналу AAPS.

#### TDD / общая суточная доза инсулина

* Общая суточная доза = болюс + базал за сутки
* Некоторые врачи рекомендуют - особенно для новых пользователей - соотношение базал-болюс 50:50. 
* Поэтому эта величина рассчитывается как суточная доза TDD / 2 * TBB (общая база = сумма базала в течение 24 часов). 
* Другие принимают за суточную базу TBB диапазон от 32% до 37% от суммарной суточной дозы TDD. 
* Как и большинство подобных подсказок они имеют ограниченное практическое значение. Примечание: Ваш диабет может быть иным!

![Браузер журнала + TDD](../images/Home2021_Action_HB_TDD.png)

(Screenshots-insulin-profile))=

## Профиль Инсулина

![Профиль Инсулина](../images/Screenshot_insulin_profile.png)

* Это профиль активности инсулина, который вы выбрали в [конфигураторе](Config-Builder-insulin). 
* ФИОЛЕТОВАЯ линия показывает, сколько инсулина остается после ввода по мере его усваивания, а СИНЯЯ линия показывает его активность.
* Важно отметить, что усваивание инсулина имеет большую остаточную длительность (хвосты). 
* Если вы раньше управляли помпой вручную, то, вероятно, привыкли считать, что инсулин усваивается примерно за 3,5 часа. 
* Тем не менее, когда вы используете замкнутый цикл длинные хвосты имеют важное значение при расчетах, т. к. все эти незначительные хвостики складываются и становятся значимыми в дальнейших расчетах AAPS.

Более подробное обсуждение различных типов инсулина, их профилей активности и почему это важно, см. здесь [Понимание новых кривых IOB на основе экспоненциальных кривых активности](https://openaps.readthedocs.io/en/latest/docs/While%20You%20Wait%20For%20Gear/understanding-insulin-on-board-calculations.html#understanding-the-new-iob-curves-based-on-exponential-activity-curves)

Отличная статья об этом: [Почему мы регулярно ошибались в определении длительности действия инсулина (DIA) и почему это важно…](https://www.diabettech.com/insulin/why-we-are-regularly-wrong-in-the-duration-of-insulin-action-dia-times-we-use-and-why-it-matters/)

Еще на эту тему: [Экспоненциальные кривые инсулина + Fiasp](https://seemycgm.com/2017/10/21/exponential-insulin-curves-fiasp/)

## Статус помпы

![Статус помпы](../images/Screenshot_PumpStatus.png)

* Разная информация о состоянии помпы. Отображаемая информация зависит от модели помпы.
* Смотрите [страницу помпы](../Hardware/pumps.md).

## Портал терапии

Здесь повторяются функции которые можно найти на экране Nightscout под символом "+", который позволяет добавлять заметки к терапии.

### Просмотреть расчет углеводов

![Посмотреть расчет углеводов на вкладке терапии](../images/Screenshots_TreatCalc.png)

* Если вы использовали [Мастер Болюса](Screenshots-bolus-wizard) (Калькулятор) для вычисления дозы инсулина, этот расчет можно увидеть позже на вкладке терапии.
* Просто нажмите на зеленую ссылку Кальк. (В зависимости от используемой помпы, инсулин и углеводы могут отображаться в одной строчке в записи терапии.)

(Screenshots-carb-correction)=

### Коррекция углеводов

![Терапия в 1 или 2 линии](../images/Treatment_1or2_lines.png)

На вкладке Лечение можно исправить ошибочные записи углеводов (если вы переоцениваете или недооценили углеводы).

1. Проверьте и запомните фактические активные углеводы COB и активный инсулин IOB на главном экране.
2. В зависимости от помпы углеводы на вкладке терапии могут быть показаны одной линией с инсулином или в виде отдельной записи (например, для Dana RS).
3. Удалите запись с неверным количеством углеводов.
4. Убедитесь, что углеводы удалены успешно, повторно проверив активные углеводы COB на главном экране.
5. Сделайте то же для активного инсулина IOB, если на вкладке терапии только одна линия для углеводов и инсулина.
   
   -> Если углеводы не удаляются должным образом, а вы добавили дополнительные углеводы, как описано здесь (6.), активных углеводов COB окажется слишком много, и это может привести к передозировке инсулина.

6. Введите правильное количество углеводов при помощи кнопки углеводов на главном экране и убедитесь, что точное время события также введено.

7. Если на вкладке терапии только одна линия для углеводов и инсулина, следует также добавить и запись о количестве инсулина. Убедитесь в том, чтобы установить правильное время событие и проверить активный инсулин IOB на главном экране после подтверждения новой записи.

## Замкнутый цикл, помощник болюса AMA / микроболюсы SMB

* Эти вкладки показывают подробную информацию о расчетах алгоритма и почему AAPS действует так, а не иначе.
* Расчет производится каждый раз, когда система получает свежее данные мониторинга CGM.
* Дополнительную информацию см. в [разделе APS на вкладке конфигуратора](Config-Builder-aps).

## Профиль

![Профиль](../images/Screenshots_Profile.png)

* Профиль содержит информацию об индивидуальных настройках диабета:
   
   * DIA (продолжительность действия инсулина)
   * IC: соотношение Инсулин - Углеводы
   * ISF: Коэффициент чувствительности к инсулину
   * Скорость базала
   * Цель: Уровень глюкозы крови для AAPS

* Начиная с версии 3.0 возможен только [локальный профиль](Config-Builder-local-profile). Локальный профиль может быть отредактирован на вашем смартфоне и синхронизирован с сайтом Nightscout.

(Screenshots-treatment)=

## Терапия

История следующих терапевтических действий:

* Bolus & Carbs -> возможность [удалить записи](Screenshots-carb-correction) для исправления истории
* [Пролонгированный болюс](Extended-Carbs-extended-bolus-and-switch-to-open-loop-dana-and-insight-pump-only)
* Временная базальная скорость
* [Временная цель](../Usage/temptarget.md)
* [Profile switch/смена профиля](../Usage/Profiles.md)
* [Careportal](CPbefore26-careportal-discontinued) - notes entered through action tab and notes in dialogues

## Источник ГК - xDrip+, BYODA...

![BG Source tab - here xDrip](../images/Screenshots_BGSource.png)

* В зависимости от заданного в параметрах источника ГК эта вкладка называется по-разному.
* Показывает хронологию показаний мониторинга и предлагает возможность удаления данных при сбое (например, при компрессии сенсора).

## клиент NS

![клиент NS](../images/Screenshots_NSClient.png)

* Показывает состояние соединения с сайтом Nightscout.
* Settings are made in [preferences](Preferences-nsclient). Вы можете открыть соответствующий раздел, щелкнув по значку шестеренки в верхней правой части экрана.
* Для устранения неполадок смотрите эту [страницу](../Usage/Troubleshooting-NSClient.md).