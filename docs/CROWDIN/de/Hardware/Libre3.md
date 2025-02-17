# **Freestyle Libre 3**

Freestyle Libre 3 (FSL3) requires a unique setup to receive BG values in to AAPS. There are two possible ways of getting Freestyle Libre 3 (FSL3) values to AAPS.

![FL3](../images/d912c1d3-06d2-4b58-ad7c-025ca1980fae.jpeg)

!!! Version 3.2.0.1 of AndroidAPS does not support 1-minute values. Acceleration and Smoothing does not work with 1-minute values. !!!

The below methods for achieving this are using the separate app Juggluco. [Link].(https://www.juggluco.nl/Juggluco/download.html) It uses Juggluco to receive raw, 1-minute interval data from the sensor which is then passed to xDrip+ or AAPS. New sensors can be started either with the Libre 3 App or directly in Juggluco. The guide below indicates the process for starting a sensor with the Juggluco app. If the sensor has been started with a Libreview account logged in, it is also possible to switch between Juggluco and the Libre 3 app as receiver.

Juggluco can also pass data to LibreView for sharing with health care providers when the sensor is started with the Libre 3 app.

Within xDrip+ the sensor can be calibrated in the range of -40 mg/dl to +20 mg/dl (-2.2 mmol/l to +1.1 mmol/l) to compensate for differences between a manual meter reading and the sensor readings.

## Methode 1: 1-minute-readings
Version 3.2.0.1 of AndroidAPS does not support 1-minute values. Acceleration and Smoothing does not work with 1-minute values.


## Methode 2: 5-minute-readings
This method uses Juggluco to receive raw, 1-minute interval data from the sensor which is then passed to xDrip+ to be smoothed into 5-minute interval data to be passed to AAPS.

### Step 1: Setup Juggluco
Download and install the Juggluco app from [here](https://www.juggluco.nl/Juggluco/download.html). Follow the instructions [here](https://www.juggluco.nl/Juggluco/libre3/)

Make sure you send the glucose calues to Xdrip+: In Juggluco's settings you can configure Juggluco to send its glucose value to other apps. Juggluco can send three types of such broadcasts: The **Librelink broadcast** was originally used by the patched Librelink app and can be used to send glucose values to xDrip+

### Step 2: Setup xDrip

The blood glucose values are received by the xDrip+ app on the smartphone.

- If not already set up, download the xDrip+ app and install one of the latest nightly builds from [here](https://github.com/NightscoutFoundation/xDrip/releases).
- In xDrip+ select "Libre2 (patched app)" as data source.
- Disable battery optimization and allow background activity for the xDrip+ app.
- If necessary, enter "BgReading:d,xdrip libre_receiver:v" under Less Common Settings->Extra Logging Settings->Extra tags for logging. This will log additional error messages for troubleshooting.
- In xDrip+ go to Settings -> Interapp Compatibility -> Transfer data locally and select ON.
- In xDrip+, go to Settings -> Interapp Compatibility -> Accept Treatments and select OFF.
- To allow AAPS to receive blood glucose values (from version 2.5.x) from xDrip+, please enable Settings -> Interapp Settings -> Identify Receiver "info.nightscout.androidaps".
- If you want to use AndroidAPS for calibration, go to Settings -> Interapp compatibility -> Accept calibrations in xDrip+ and select ON. It's also best to check the options under Settings -> Less General Settings -> Check Advanced Calibration Settings.

### Step 3: Start sensor within xDrip

In xDrip+ den Sensor dann mit „Start Sensor“ und „nicht heute“ starten. It is not necessary to hold the mobile phone onto the sensor. In fact "Start Sensor" will not physically start any Libre 3 sensor or interact with them in any case. This is simply to indicate xDrip+ that a new sensor is delivering blood sugar levels. If available, enter two bloody measured values for the initial calibration. Now the blood glucose values should be displayed in xDrip+ every 5 minutes. Skipped values, e.g. because you were too far away from your phone, will not be backfilled.

Wait at least 15-20 minutes if there is still no data.

After a sensor change xDrip+ will automatically detect the new sensor and will delete all calibration data. You may check you bloody BG after activation and make a new initial calibration.

### Step 4: Configure AndroidAPS

- In AndroidAPS go to Config Builder -> BG Source and check "xDrip+"
- If AndroidAPS does not receive BG values when phone is in airplane mode, use "Identify receiver"
- Turn of Smoothing (done in Xdrip+ already)

As of now, when using Libre 3 as a BG source, the "Always enable SMB" and "Enable SMB by Carbs" options cannot be enabled in the SMB algorithm. The BG values from Libre 3 are not smooth enough to use safely.



## Subsequent sensor changes

1. Open Juggluco and note the serial number of the existing sensor

![Libre serial number](../images/libre3/step\_13.jpg)

2. Now simply scan your new sensor with your phone’s NFC reader. Juggluco will display a notice if the process had been started successfully.
3. When you are ready to deactivate the old sensor, then open the Juggluco menu by clicking anywhere in the empty space in the upper left hand corner of the screen.
4. Select the exired sensor and tap "Terminate"

![Terminate sensor](../images/libre3/step\_14.jpg)

Note: When two sensors are active Juggluco will send the most recent value from either sensor to xDrip+. If the sensors are not calibrated and reading BG similarly, this may result in jumpy BG values being reported to xDrip+. If you terminate the wrong sensor, you can reactivate it by simply scanning the sensor.

## Switch sensor between Libre 3 and Juggluco app

If the sensor has been started with a Libreview account logged in, it is also possible to switch between Juggluco and the Libre 3 app as receiver. This requires the following steps:

1. Install the Libre 3 app from Google Playstore
2. Set up the Libre 3 app with the Libreview account with which the sensor was activated.
3. Force stop the Juggluco app in the Android settings.
4. In the Libre 3 menu, click "Start Sensor", select "Yes", "Next" and scan your sensor.
5. After some minutes, the BG-Values should be visible within Libre 3 App.

In order to switch from the Libre 3 app to Juggluco, you need to force-stop Libre 3 app via Android settings and proceed with Step 1 & 2.

## Erfahrungen und Troubleshooting

### Troubleshooting Libre3 -> Juggluco Connection

- Make sure you are using a current version of the Juggluco app
- Check your settings according to this guide
- You may sometimes have to force stop the Libre 3 app and Juggluco and restart it.
- Disable Bluetooth and enable it again
- Wait some time or try to close Juggluco
- Older versions of Juggluco (below 2.9.6) do not send subsequent data from the Libre3 sensor to connected devices (e.g. Juggluco on WearOS). You may need to click "Resend data" in the patched Libre3 app (Juggluco menu).

### Weitere Hilfe

Original instructions: [jkaltes website](https://www.juggluco.nl/Juggluco/libre3/)

Zusätzliches Github Repository: [Github Link](https://github.com/maheini/FreeStyle-Libre-3-patch)
