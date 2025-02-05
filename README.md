# CDM plugin V2.2
CDM is an Euroscope plugin based on the real life CDM tool that allows us to improve the departure flows at airports.
CDM includes the following times:
- EOBT: Estimated off block time.
- TOBT: Target off block time.
- TSAT: Target Start-Up Approval Time.
- TTOT: Target Take Off Time.
- TSAC: Target Start-Up Approval Communicated.
- ASAT: Actual Start-Up Approval Time.
- ASRT: Actual Start-Up Request Time.
- CTOT: Calculated Take Off Time.


## How to use:
- Load up the plugin.
- If there is no master controller, you should use the command ``.cdm master {airport}`` of the airport you want to become the master. You can have as many airport as you want, but there can ony be **1 MASTER at the same time** (The MASTER should be DELIVERY or the lowest ATC position to have access to all CDM actions).
- Add The following items to the departure list with their actions:

- EOBT

  - ![image](https://user-images.githubusercontent.com/68125167/210136450-3b4b7fea-8f80-441a-ba3f-b95e3d8ca5d1.png)

    or

  - ![image](https://i.gyazo.com/928f2e35f0a4248e17442bba552d72e0.png)

- E

  - ![image](https://i.gyazo.com/436e8eb7b20b00d2c39a483319d03425.png)

- TOBT

  - ![image](https://user-images.githubusercontent.com/68125167/210136458-86422bb9-d3cc-4ac1-a8a1-0c25d5ac9f7b.png)

    or

  - ![image](https://i.gyazo.com/ad6344055e7de91ab8a386f7153d19e1.png)

- TSAT

  - ![image](https://i.gyazo.com/37b0ad531fc4a32dfaffbf7db83c5546.png)

- TTOT

  - ![image](https://i.gyazo.com/4533873ef8d8342cb5b35ed381bb0f47.png)

- TSAC

  - ![image](https://user-images.githubusercontent.com/68125167/210136465-21a3d004-38a0-4261-8055-c22ca424d7b1.png)

    or

  - ![image](https://i.gyazo.com/8f9d55ec477a8c21ddb63df3b4da15a1.png)

- ASAT

  - ![image](https://i.gyazo.com/cf08823153ce9e99e1936659c07ad67d.png)

- ASRT

  - ![image](https://user-images.githubusercontent.com/68125167/210136468-33b8384a-aa92-47dc-9512-ae7dbe8eaed0.png)

- CTOT

  - ![image](https://user-images.githubusercontent.com/68125167/210136480-babb9ec2-6989-4302-91ac-a82de59ecadf.png)

    or

  - ![image](https://i.gyazo.com/775e1bf69fac29e2e3a776d35e67952a.png)

- Ready Start-up

  - ![image](https://i.gyazo.com/842144f7bddf11f3c9165c42ef0f940e.png)

- Extra (All CDM Option in one Menu)

  - ![image](https://user-images.githubusercontent.com/68125167/210136505-9b46b673-537d-4e2c-86aa-be36add431dd.png)



## MASTER AND SLAVE:
- Master: The master is the "admin" of the CDM and is the only controller who calculates the times (TSAT, TTOT and ASRT)
  - Use ``.cdm master {airport}`` command (**TO LET THE CDM DO IT'S JOB, ONLY 1 CONTROLLER CAN BE THE MASTER AT THE SAME TIME**).
- Slave: The Slave Monitors the CDM and has some limited actions.
  - Default type, so, you don't need to change anything unless you are now a master, where you can use ``.cdm slave {airport}`` command.

### HOW TO DO A CONTROLLER CHANGE CORRECTLY:
1. Check to have the same *CDMconfig.xml* and *taxizones.txt* configuration, otherwise it won't work correctly.
2. The **Old controller** changes to Slave with command ``.cdm slave``.
3. Once there are no master controllers, the **new controlles** gets the master "rol" with the command ``.cdm master {airport}``.
4. That's it!

## Define configurations

### Colors.txt
  - color1 = DARK GREEN
  - color2 = LIGHT GREEN
  - color3 = GREY
  - color4 = ORANGE
  - color5 = YELLOW
  - color6 = DARKYELLOW
  - color7 = RED
  - color8 = EOBT STATIC COLOR
  - color9 = TTOT STATIC COLOR
  - color10 = ASRT STATIC COLOR
  - color11 = CTOT STATIC COLOR
  - color12 = CHANGES TOBT, TSAT and ASAT to the defined color WHEN S/U STATUS IS SET
 
### CDMconfig.xml
  - Select CTOT option (``Ctot code="<VATCAN_CODE>"``), if not using CTOTs, please leave it empty (``Ctot code=""``).
  - Normal Visibility Operations Rate/hour (ex. rate ops="40").
  - Low Visibility Operations Rate/hour (ex. rateLvo ops="10").
  - Expired CTOT time, it selects the time before expire the CTOT if the pilot is not connected (ex. expiredCtot time="15").
  - Real Mode to calculate times automatically from the sent EOBT (**DISABLED:** realMode mode="false" and **ENABLED:** realMode mode="true")
  - ReaMsg (ex. minutes="0"). - It sets the time to add for the *"Send Rea Message"* function.
  - [OPTIONAL] Rates URL (ex. Rates url="https://........"), if no URL needed, just leave it blank (ex. Rates url="") and the file will be used.
  - [OPTIONAL] Taxizones URL (ex. Taxizones url="https://........"), if no URL needed, just leave it blank (ex. Taxizones url="") and the file will be used.
  - [OPTIONAL] Ctots URL (ex. Ctot url="https://........"), if no URL needed, just leave it blank (ex. Ctot url="") and the file will be used.
  - Default Taxi time in minutes if taxi time not found in the taxizones.txt file (ex. DefaultTaxiTime minutes="15").
  - Refresh Time in seconds (ex. RefreshTime seconds="20").
  - Debug mode activated (true) or desactivated (false) (ex. Debug mode="false" or Debug mode="true").
  - [OPTIONAL] FlowRestrictions URL to the JSON file - Format is defined below (ex. FlowRestrictions url:"https://...."), if no URL needed, just leave it blank (ex. FlowRestrictions url="").
  - [OPTIONAL] FTP host to push CDM Data (ex. ftpHost host:"ftp.aaaaaa.com") - leave it blank if not in use "".
  - [OPTIONAL] FTP user to push CDM Data (ex. ftpUser user:"username") - leave it blank if not in use "".
  - [OPTIONAL] FTP password to push CDM Data (ex. ftpPassword password:"&&&&&&") - leave it blank if not in use "".
 
### taxizones.txt
  - You can define a zone with an specific taxiTime with the following specifications ``AIRPORT:RUNWAY:BOTTOM_LEFT_LAT:BOTTOM_LEFT_LON:TOP_LEFT_LAT:TOP_LEFT_LON:TOP_RIGHT_LAT:TOP_RIGHT_LON:BOTTOM_RIGHT_LAT:BOTTOM_RIGHT_LON:TAXITIME``, ex:``LEBL:25L:41.286876:2.067318:41.290236:2.065955:41.295688:2.082523:41.292662:2.084613:10``, if no taxizone defined, the default taxi time is set to 15 min.

### rate.txt

  Format:
  `AIRPORT:A:ArrRwyList:NotArrRwyList:D:DepRwyList:NotDepRwyList:DependentRwyList:Rate_RateLvo`

    - ArrRwyList -> Comma-separated list of runways (If more than 1, it will use if one, other or all selected). Enter * to disregard.

    - NotArrRwyList -> Comma-separated list of runways. Enter * to disregard.

    - DepRwyList -> Comma-separated list of runways (If more than 1, it will use if one, other or all selected). Enter * to disregard.

    - NotDepRwyList -> Comma-separated list of runways. Enter * to disregard.

    - DependentRwyList -> Comma-separated list of runways (it will use the same sequence order for runways selected here). Enter * to disregard.

    - Rate_RateLvo -> Normal Rate and LVO Rate. If more than one departure runways, you can define more than one rate separated by comma.


  Examples:

    - `LEPA:A:24L:*:D:24R,24L:*:24L,24R:30_12` (1 arr runway, 1 dep runway, 24R/L as dependant. 1 rate defined for all departures).

    - `LEPA:A:24L:24R:D:24R,24L:*:*:30_12,20_7` (1 arr runway, 1 non-arrival runway, 2 dep runway, dep runways as independant, different rates defined for both dep runways).

    - `LEPA:A:*:*:D:*:*:*:30_12` (All departures would have the same rate, doesn't matter the selected runways).

  Internal Checks:
  
  A line will be "activated" based on:

   - Runway assigned to the plane. (This runway should be in the `DepRwyList` list of the line. Which must comply with the below point).

   - Runways selected in Euroscope's Runway selector dialog (if the selected runways are in the line. If more runways in the line than selected in ES, but the selected are as `DepRwyList` in the line, it will be activated too).
   
<br>

  Important points
  - **Order of the configurations/rates is important (first line more important than last).**
  - **AIRPORTS NOT DEFINED, WILL NOT BE CONSIDERED A CDM AIRPORT.**
  - **Examples can be found in the givenfiles.**
  
  
  <br>

*Examples can be found in the givenfiles.*



## Flow Restriction
### How does it work?
Flow restrictions create CTOTs to planes afected with published MDIs from ECFMP.
If we want to change the TOBT, we must recalculate the CTOT by pressing with "left click" the CTOT time and selecting "reload CTOT".
The data from the API will be refreshed every 5 minutes.

### How to use them?
https://ecfmp.vatsim.net/api/v1/plugin should be set in the Flow Measure field of the CDMconfig.xml.

## FTP files and format
### Files
Every airport will have a different txt file (ex. LEBL airport: CDM_data_LEBL.txt)

### Format
``CALLSIGN,TOBT,TSAT,TTOT,CTOT,FlowRestrictionMessage,``
```
BAW224,183600,183600,184400,ctot,flowRestriction,
RYR22GV,183600,183700,184600,ctot,flowRestriction,
MON562,183600,183700,184800,ctot,flowRestriction,
IBE73RT,183600,184000,185000,ctot,flowRestriction,
IBE51D,183600,184200,185200,ctot,flowRestriction,
IBE3540,183600,184400,185400,ctot,flowRestriction,
EXS15G,183600,184900,185600,ctot,flowRestriction,
EXS12,183600,184700,185800,1922,London Event,
MON837,183600,185200,190000,ctot,flowRestriction,
RYR33P,183600,185200,190200,ctot,flowRestriction,
MON235N,183600,185300,190400,ctot,flowRestriction,
EZY12JM,183600,185600,190600,ctot,flowRestriction,
RYR42TQ,183600,185700,190800,ctot,flowRestriction,
BEE154A,183600,190000,191000,1924,London Event,
```
## CAD - Capacity Availability Document
On this Document (https://raw.githubusercontent.com/rpuig2001/Capacity-Availability-Document-CDM/main/CAD.txt) there are the capacities for the arrival airports.
The CDM will separate aircrafts with the same destination by the rate specified in the CAD creating a CTOT with the Flow Message (FM) of "ARR CAP" (If the arrival rate is less than the departure airport and NO Flow Measures are in force)).
The data from the CAD will be refreshed every 5 minutes (Same as the Flow Measures).

For more information, check the CAD GitHub Repository.
https://github.com/rpuig2001/Capacity-Availability-Document-CDM

## Commands
- ``.cdm reload`` - Reloads all CDM plugin configs and taxizones file.
- ``.cdm refresh`` - Force the refresh phase to do it now.
- ``.cdm save`` - Saves data to savedData.txt.
- ``.cdm load`` - Loads savedData.txt.
- ``.cdm master {airport}`` - Become the master of the selected airport.
- ``.cdm slave {airport}`` - Turn back to slave of the selected airport.
- ``.cdm refreshtime {seconds}`` - It changes the refresh rate time in seconds (Default 30, MAX 99 Seconds).
- ``.cdm delay {minutes}`` - Adds delay minutes to all traffics that have a TSAT greater then now. (it doesn't apply if TSAT has already passed) - WAIT SOME SECONDS TO UPDATE AFTER APPLIED.
- ``.cdm lvo`` - Toggle lvo ON or OFF.
- ``.cdm realmode`` - Toggle realmode ON or OFF.
- ``.cdm remarks`` - Toggle set TSAT to Euroscope scratchpad ON or OFF.
- ``.cdm rates`` - Updates rates values from rate.txt.
- ``.cdm help`` - Sends a message with the available commands.

## Functions and colors:

- Column EOBT: It gets the EOBT set by the pilot in the flightplan.
  - NOTES:
    - If **RealMode** is enabled, when the pilot send a new EOBT, then it will show with ``color4`` (Default ORANGE) when **EOBT is different than TOBT**.
  - Functions
    - ``Edit EOBT`` -> Sets EOBT to the specified time (4 digits).
  - Colors:
    - ``color8`` -> Default.

- Column TOBT: If realMode is disabled, TOBT will calculate TSAT and TTOT from the TOBT time. To delete it simple edit the time and press enter deleting the content.
  - NOTES:
    - If there is no ASRT or "Ready Start-up GREEN", at TOBT+5, TSAT and other times will be invalidated.
    - To add a TOBT while realMode is DISABLED, use the Ready TOBT Function to set the actual time as a TOBT or the Edit TOBT to set a 4 digits time.
    - If realMode is enable it will ONLY set the EOBT as TOBT when the first flightplan is recived, if the EOBT is changed the TOBT will not change automatically and you can use other functions such as the EOBT to TOBT Function to move it through. (EOBT will have a different color to say you that there's a new time sent by the pilot).
  - Functions:
    - ``Ready TOBT`` -> Sets TOBT to the actual time.
    - ``Edit TOBT`` -> Sets TOBT to the specified time (4 digits).
  - Colors:
    - ![#8fd894](https://img.shields.io/badge/-8fd894) `LIGHT GREEN` -> 
    - ![#00c000](https://img.shields.io/badge/-00c000) `DARK GREEN` -> After EOBT-5.

- Column E: It shows a letter depending on the plane timmings:
  - Functions:
    - NO FUNCTIONS.
  - Colors:
    - ![#00c000](https://img.shields.io/badge/-00c000) `DARK GREEN` -> Default.
  - TEXT SHOWING:
    - P: EOBT is farther than the Actual Time - 35min. TSAT, TTOT and TOBT will be showing the following character "~~" (To order them to the end of the list).
    - C: EOBT is less than 35min and TOBT hasn't expired (TOBT+6) or TSAT hasn't expired (TSAT+6).
    - I: TSAT has expired.

- Column TSAT: It is the TTOT - the taxi time defined in the taxizones.txt, otherwise it sets 15min.
  - Functions:
    - NO FUNCTIONS.
  - Colors:
    - ![#8fd894](https://img.shields.io/badge/-8fd894) `LIGHT GREEN` -> From EOBT-35 to TSAT-5 and after TSAT+6 if not expired.
    - ![#00c000](https://img.shields.io/badge/-00c000) `DARK GREEN`  -> From TSAT-5 to TSAT+5.
    - ![#f5ef0d](https://img.shields.io/badge/-f5ef0d) `YELLOW` -> From TSAT+5 to TSAT+6.

- Column TTOT: The plugin calculates a TSAT based on this column, the TTOT, you can't have planes with same TTOT, the time between departures is calculated from the rate/hour. So if you need 40 departures/hour, the plugin will calculate it for you with no equal TTOTs.
  - Functions:
    - ``Set actual TTOT as CDT`` -> Sets TTOT as CDT.
    - ``Edit/Set custom CDT`` -> Sets CDT as desired.
  - Colors:
    - ``color9`` -> Default.

- Column TSAC: With the left click you can directly set the tsat and with the right click you can remove it or set the time you want. If this field is +/- 5min that the TSAT, the color change to orange to indicate that his TSAT has changed more than 5min.
  - Functions:
    - NO FUNCTIONS.
  - Colors:
    - ![#00c000](https://img.shields.io/badge/-00c000) `DARK GREEN` -> If between +/- 5min of TSAT.
    - ![#ed852e](https://img.shields.io/badge/-ed852e) `ORANGE` -> If +/- 5min of TSAT.

- Column ASAT: It sets the time when ST-UP, TAXI or DEPA state is set on the first time.
  - Functions:
    - NO FUNCTIONS.
  - Colors:
    - ![#00c000](https://img.shields.io/badge/-00c000) `DARK GREEN` -> If actual time < ASAT - 5min.
    - ![#f5ef0d](https://img.shields.io/badge/-f5ef0d) `YELLOW` -> From ASAT+5 to always.

- Column ASRT: It shows the requested StartUp time, It can be added to the list with the toggle function or sending a REA Msg.
  - Functions:
    - ``Toggle ASRT`` -> Sets RSTUP/ASRT or removes it if already set.
  - Colors:
    - ``color10`` -> Default.
  
- Column Ready Start-up: It shows if the plane is Ready for Start-up or not together with the ASRT. (ASRT and Ready Start-up do the same, but this column is a way to represent the real "ready start-up" state from IRL because Euroscope doesn't have this state).
  - Functions:
    - ``Toggle Ready Start-up function`` -> Sets RSTUP/ASRT or removes it if already set.
  - Colors:
    - ![#00c000](https://img.shields.io/badge/-00c000) ``GREEN`` -> RSTUP is set.
    - ![#BE0000](https://img.shields.io/badge/-BE0000) ``RED`` -> RSUP is NOT set.

- Column CTOT: It shows aircraft's CTOT which can be added, modified, removed or reloaded.
  - Functions:
    - ``Send REA Msg`` -> It will be contarntly looking for a better CTOT every refreshtime when this is checked.
    - ``Remove from REA Msg`` -> It will keep ctot and will not look for a better CTOT anymore.
  - Colors:
    - ``color11`` -> Default.
    - ![#f5ef0d](https://img.shields.io/badge/-f5ef0d) `YELLOW` -> REA Msg is sent.
