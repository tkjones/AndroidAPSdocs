# Dexcom G7


## Grundlegendes im Voraus

Seit Ende Oktober 2022 ist der Dexcom G7, nachdem er die CE-Zertifizierung im Frühjahr 2022 erhalten hatte, verfügbar.

Der G7 glättet weder in der (Dexcom) App noch im Lesegerät die Glukosewerte. Dies ist anders als es beim G6 war. Mehr Details dazu findest Du [hier](https://www.dexcom.com/en-us/faqs/why-does-past-cgm-data-look-different-from-past-data-on-receiver-and-follow-app). Um die Messwerte des G7 in AAPS sinnvoll nutzen zu können, müssen diese geglättet werden.

![G7 english](../images/6fe30b84-227a-4bae-a9a5-527cee341dbf.png)

## 1.  Patched Dexcom G7 App (DiAKEM)

**Note: AAPS 3.2.0.0 or higher is required!**

### Installiere eine neue gepatchte (!) G7-App und starte den Sensor

A patched Dexcom G7 app (DiAKEM) gives acess to the Dexcom G7 data. Dies ist nicht die BYODA-App. BYODA kann derzeit keine Daten direkt vom G7 empfangen.

Wenn Du bisher die originale Dexcom-App genutzt hast, musst Du diese im ersten Schritt nun deinstallieren. Wenn Du den Sensor-Kopplungscode noch kennst, kannst Du eine laufende Sensorsitzung weiterführen. Bitte merke ihn Dir daher, bevor Du die originale G7-App deinstallierst.

Lade die gepatchte App (.apk-Datei) [hier](https://github.com/authorgambel/g7/releases) herunter und installiere sie.

Gebe den Sensor Code (Kopplungscode) in der gepatchten App ein.

Beachte die allgemeinen Empfehlungen zur CGM-Hygiene und den empfohlenen Sensor-Tragestellen [hier](../Hardware/GeneralCGMRecommendation.md).

Nach der Aufwärmphase werden die Glukosewerte wie üblich in der G7-App angezeigt.

### Configuration in AAPS

Zur Konfiguration von AAPS
- Wähle 'BYODA' in der Konfiguration als BZ-Quelle (auch wenn es tatsächlich die gepatchte G7-App ist!)
- Sollte AAPS keine Werte empfangen, wechsel auf eine andere BZ-Quelle und dann wieder zurück auf 'BYODA'. Damit löst Du Berechtigungsabfrage zum Datenaustausch zwischen AAPS und BYODA aus.

Mit der Auswahl von "Average Smoothing" oder "Exponential Smoothing", kannst Du die Glättung der empfangenen Glukosewerte aktivieren. Wenn Du die Funktion deaktivieren möchtest, wähle "Keine Glättung" aus. "Exponential smoothing" ist aggressiver und schreibt die letzten Glukosewerte neu, und hilft dabei mit verrauschten Werten umgehen zu können. "Average smoothing" verhält sich ähnlich wie die nachträgliche Glättung (back smoothing) in BYODA G6 und schreibt die älteren Werte nicht aber den aktuellen Wert neu. Damit kann schneller reagiert werden.

**'Exponential Smoothing'** **MUSS** aktiviert sein, um G7-Sensorwerte sinnvoll nutzen zu können.

## 2. Xdrip+ (direct connection to G7)

- Follow the instructions here: [Xdrip+ G7](https://navid200.github.io/xDrip/docs/Dexcom/G7.html)
- Wähle in AAPS unter Konfiguration > BZ-Quelle > "xDrip+" aus. Passe die Einstellungen in xDrip+ so an, wie es unter  [xDrip+ Einstellungen](../Configuration/xdrip.md) beschrieben ist.

## 3. xDrip+ (Companion App)

-   Lade xDrip+ herunter und installiere es: [xDrip+](https://github.com/NightscoutFoundation/xDrip)
- Wähle in xDrip+ "Companion App" als Datenquelle aus. Zusätzlich muss in den Bluetootheinstellungen (Einstellungen > Erweiterte Einstellungen > Bluetootheinstellungen) "Companion Bluetooth" aktiviert werden.
- Wähle in AAPS unter Konfiguration > BZ-Quelle > "xDrip+" aus. Passe die Einstellungen in xDrip+ so an, wie es unter  [xDrip+ Einstellungen](../Configuration/xdrip.md) beschrieben ist. 
