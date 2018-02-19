# AxH Thermostat

## V 1.0.0 - 2018.02.19
  First stable release

  Added SSID selection

## V 0.3.9 - 2018.02.15
  Double reverse flipped sommersault

## V 0.3.8 - 2018.02.15
  Top secret implementations.

## V 0.3.7 - 2018.02.15
  Fixed push of last regulation duration to TS.

  Added COMPRESSOR_PIN and COOLING_PIN to BSThermConstants.
    - User can now use any free pin.

  Modified custom_config inclusion following Rekhyt's hint and code.

## V 0.3.6 - 2018.02.15
  Added clear log button on UI
  Implemented new Cooling and heating logic.
  Implemented Rekhyt's configuration system
    - Defining CUSTOM_CONFIG pulls in, during compilation, custom_config.h
    custom_config.h is not under GIT.
    A default_config.h is provided with a default (mostly empty) configuration

## V 0.3.5 - 2018.02.14
  Refactored WiFi connection code.
  Added connection status checks in elapsedSeconds.
  Added reconnection code in case of connection lost.
  Added benchmarks for readTemperatures and logTemperatures.

  Restored ThingSpeak connection.

## V 0.3.4 - 2018.02.13
  ThingSpeak push is not working due to the switch to AsyncClient.
  As of now I am not able to build with SSL enabled.

## V 0.3.3 - 2018.02.13
  Switched to AsyncClient for ThingSpeak push.

## V 0.3.2 - 2018.02.13
  Fixed display bug in UI logger.

## V 0.3.1 - 2018.02.13
  Added OLED visualisation for WiFi Strength.
  Implemented UI log viewer with export to clipboard in CSV format

## V 0.2.11 - 2018.02.12

  Added UI signal strength to web UI.
  Same code can be used to show signal strength on OLED, we just need
  to add 2 more icons.

  Notes for log:

  Michele Antonecchia, [12.02.18 15:59]
  il secondo con
  <timestamp> S1: val S2: val S3:val D6:ON/OFF D8:ON/OFF WiFi:Level
  oppure qualcosa del tipo

  2018-02-15T16:22:30.956 SP:21 S1:22.125 S2:12.675 S3:0 ST:ON WiFi:5

  manca solo la tolleranza e direi che è completo
  poi se è possibile recuperare i buffer da web ancora meglio
  tipo http://192.168.1.20/#/bufferCFG e /bufferLOG (nomi a cazzo)

## V 0.2.10 - 2018.02.12
  Changed temperature read code.
  Now one request is sent on the bus and then temperature are
  collected individually.

  This should reduce delay by about 1/3rd.

## V 0.2.9 - 2018.02.12
  Temperature reads are now happening once each 60 seconds

  Fixed bug in UI that could lead to confusion while setting up
  probes' ids.

  Fixed UI bug that prevented the display of readings from S3.

  Removed some unused leftover code.

  Rounded temperature reads to the first decimal place.

  There's probably and issue with websocket reconnections.
  I haven't been able to reproduce it.
  This needs further investigation.

## V 0.2.8 - 2018.02.09
  Fixed configuration bug.
  On first run (whenever there's no configuration) the system
  saves the default one.
  If on that occasion there are no probes attached, the probe
  ids array saved with the default config remains empty ... forever.

  Shame, shame, shame.

## V 0.2.7 - 2018.02.09

  Added temperature correction terms for all three probes.
  Removed some unused code.

## V 0.2.6 - 2018.02.07

  Removed Telegram code.
  Implemented basic websocket client <-> server comunication.

  Code needs cleanup and refactoring

## V 0.2.5 - 2018.02.07

  Added mDNS responder.
  The system is reachable with the local name of:

  axhtherm.local


## V 0.2.4 - 2018.02.07

  Fixed UI bug that prevented the display of system's status while
  in regluating mode.

  In S1 box the icons showing the status are not displayed correctly
  if at all.

  Added TelegramBot library and some basic code.
  Unfortunately, due to what appears like a library bug TELEGRAM
  integration has been disabled for further investigation.

## V 0.2.2 - 2018.02.06
  New Implementations
  - Push of system status to ThingSpeak (field5)
   - 0 Relay is off
   - 1 Compressor protection is ON
   - 2 Relay is On

  - System is now reachable via LAN IP address

## V 0.2.1 - 2018.02.06

  Fixed a bug that kept the temperature upload countdown RUNNING
  even if upload was not enabled.

## V 0.2.0 - 2018.02.06

  Changed the UI for probes configuration.
  Following the need for an easier way to let the users
  setup the probes, and the advices of @Rekhyt, the UI
  has changed replacing input boxes for probe's Id with a select field.

  The user now has the chance of selecting the appropriate ID with
  visual indication of whether a given ID has been already selected
  or not.

  The "Scan" button has been removed too.

  An user can now pick an Id from the available list and test it
  by means of the usual "Test" button.

## V 0.1.9 - 2018.02.05

  Bug Fix
  Regulation got triggered even if the temperature was within tolerance
  bounds.
  This happened because of ABS function.
  Delta = abs(s1LastRead - s1SetPoint)
  Apparently Delta was coherced to an int by abs.

  Moved delta calculation outside of isRegulationNeeded.
  It was computed very, very often and since it wouldn't
  have changed unless there was a change in read temperature,
  it seemed more sensible to put it in temperature reading code.

## V 0.1.8 - 2018.02.01

  Fixed cooling bug that kept compressor protection countdown running and
  wind down below 0.
  That happened when switching from running to pause state while in cooling
  mode, and compressor protection delay was required.

## V 0.1.7 - 2017.12.13

  * BACKEND:
  * Added a counter to measure the time the relay output is on
  before temperature falls within the desired setpoint.

  * Minor refactorings to accomodate for above mentioned changes.

## V 0.1.6 - 2017.12.12
<<<<<<< HEAD

=======

>>>>>>> 072e0e3e75f75f3955910a850a801ee2bcab007d
  * BACKEND:
  * Minor refactorings:
   * Separated temperature reading code from upload.
   * Temperatures read has it's own unmodifiable interval.
     By default it is set to 5 seconds.
   * Temperature statistics are now computed on the backend.
    * Min, Max and mean temperatures are computed while the system is running
      and transferred to frontend upon polling.

  * FRONTEND
    * Fixed a bug that prevented S2 and S3 statistics to be shown.
    * Minor refactorings to match the backend changes.


  * DOCUMENTATION
    * Added BOM draft to the users' manual.



## Future plans

  - Allow up to 4 probes to be used (1 active and 3 monitors)
    - Need to change display layout and frontend configuration page

  - Implement temperature profile with multiple steps
    - Need to review display layout and frontend configuration page

  - Allow for setpoint to be changed via physical buttons
    - Increment/Decrement current setpoint by given tolerance

  - Add a physical reset button

  - Telegram norifications (?)
  - Smart display communication
  - OpenHAB integration
