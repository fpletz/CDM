# CDM plugin
CDM is an Euroscope plugin based on the real life CDM tool that allows us to improve the departure flows at airports.
CDM includes the following times:
- EOBT: Estimated off block time.
- TOBT: Target off block time.
- TSAT: Target Start-Up Approval Time.
- TTOT: Target Take Off Time.
- TSAC: Target Start-Up Approval Communicated.
- ASRT: Actual Start-Up Request Time.


## How to use:
- Load up the plugin.
- Add The following items to the departure list with their actions:

- A

![image](https://i.gyazo.com/2a15bf80068f46e01f48fee6b3ef97e0.png)

- EOBT

![image](https://i.gyazo.com/83cebfb8543e58eca823b7a5a92fa3fa.png)

- E

![image](https://i.gyazo.com/3c65d71bc812ccf6966c4694c9fa425d.png)

- TOBT

![image](https://i.gyazo.com/754f328e3d0fb087077cd2bfc89c1a54.png)

- TSAT

![image](https://i.gyazo.com/f4de2894de5f5b12733ad94896d9cdbb.png)

- TTOT

![image](https://i.gyazo.com/bfc39b46e67f53683236020c8fe57ea2.png)

- TSAC

![image](https://i.gyazo.com/1d3792af2947ddae6bcde5075abb9582.png)

- ASRT

![image](https://i.gyazo.com/47ca5006438009d4fa573ba328cc0abb.png)

- CTOT

![image](https://i.gyazo.com/d6561232afdc79d7bdaa28901dec95e4.png)


## MASTER AND SLAVE:
- Master: The master is the "admin" of the CDM and is the only controller who calculates the times.
  - Use ``.cdm master`` command (**TO LET THE CDM DO IT'S JOB, ONLY 1 CONTROLLER CAN BE THE MASTER AT THE SAME TIME**).
- Slave: The Slave Monitors the CDM and is unable to add/edit CTOTs.
  - Default type, so, you don't need to change anything unless you are now a master, where you can use ``.cdm slave`` command.

## HOW TO DO A CONTROLLER CHANGE CORRECTLY:
1. Check to have the same *CDMconfig.xml* and *taxizones.txt* configuration.
2. The **Old controller**, which is the Master, uses the command ``.cdm save`` to get the *savedData.txt*.
3. Once the **Old Controller** has this *savedData.txt* file, he send it to the **new controller**.
4. The **new controller** adds this file to the Plugin .dll location and uses ``.cdm load`` command to have the same times.
5. Then, the **Old controller** changes to Slave with command ``.cdm slave``.
6. Once there are no master controllers, the **new controlles** gets the master "rol" the command ``.cdm master``.
8. That's it!

### Define configurations
- CDMconfig.xml
  - Add icao (ex. apt icao="LEAL").
  - Rate/hour (ex. rate ops="40").
  - ReaMsg (ex. minutes="0"). - It sets the time to add for the *"Send Rea Message"* function.
- ctot.txt
  - Add CTOTs which will be imported on Euroscope start-up or with the command ".cdm ctot". Add CTOTs with the following format: ``CALLSIGN,CTOT``, ex:``VLG11P,1745`` (Each line has an aircraft)
- taxizones.txt
  - You can define a zone with an specific taxiTime with the following specifications ``AIRPORT:RUNWAY:BOTTOM_LEFT_LAT:BOTTOM_LEFT_LON:TOP_RIGHT_LAT:TOP_RIGHT_LON:TAXITIME``, ex:``LEPA:24R:39.543504:2.712383:39.548777:2.719502:10``, if no taxizone defined, the default taxi time is set to 15 min.

*Examples can be found in the given CDMconfig.xml and taxizones.txt file.*

### Commands
- ``.cdm reload`` - Reloads all CDM plugin.
- ``.cdm rate`` - Reloads rate from the CDMconfig.xml file.
- ``.cdm airport`` - Reloads airport from the CDMconfig.xml file.
- ``.cdm ctot`` - Loads ctot.txt data.
- ``.cdm save`` - Saves data to savedData.txt to sync times with other controllers.
- ``.cdm load`` - Loads savedData.txt to sync times with other controllers.

## Functions and colors:
- Column A: It toggles an A to remember the controller that the plane is waiting for something.
  - ![#f5ef0d](https://via.placeholder.com/15/f5ef0d/000000?text=+) `YELLOW`: Always this color.

- Column EOBT: It gets the EOBT set by the pilot in the flightplan.
  - ![#b6b6b6](https://via.placeholder.com/15/b6b6b6/000000?text=+) `GREY`: Always this color.

- Column TOBT: We can not simulate it, so it gets the EOBT and the colors is green.
  - ![#8fd894](https://via.placeholder.com/15/8fd894/000000?text=+) `LIGHT GREEN`: From EOBT-35 to EOBT-5.
  - ![#00c000](https://via.placeholder.com/15/00c000/000000?text=+) `DARK GREEN`: After EOBT-5.

- Column E: It shows a letter depending on the plane timmings:
  - P: EOBT is farther than the Actual Time - 35min.
  - C: EOBT is less than 35min and TSAT hasn't expired (TSAT+6).
  - I: TSAT has expired.

- Column TSAT: It is the TTOT - the taxi time defined in the taxizones.txt, otherwise it sets 15min.
  - ![#8fd894](https://via.placeholder.com/15/8fd894/000000?text=+) `LIGHT GREEN`: From EOBT-35 to TSAT-5 and after TSAT+6 if not expired.
  - ![#00c000](https://via.placeholder.com/15/00c000/000000?text=+) `DARK GREEN`: From TSAT-5 to TSAT+5.
  - ![#f5ef0d](https://via.placeholder.com/15/f5ef0d/000000?text=+) `YELLOW`: From TSAT+5 to TSAT+6.

- Column TTOT: The plugin calculates a TSAT based on this column, the TTOT, you can't have planes with same TTOT, the time between departures is calculated from the rate/hour. So if you need 40 departures/hour, the plugin will calculate it for you with no equal TTOTs.
  - ![#00c000](https://via.placeholder.com/15/00c000/000000?text=+) `DARK GREEN`: Always this color.

- Column TSAC: With the left click you can directly set the tsat and with the right click you can remove it or set the time you want. If this field is +/- 5min that the TSAT, the color change to orange to indicate that his TSAT has changed more than 5min.
  - ![#00c000](https://via.placeholder.com/15/00c000/000000?text=+) `DARK GREEN`: If between +/- 5min of TSAT.
  - ![#ed852e](https://via.placeholder.com/15/ed852e/000000?text=+) `ORANGE`: If +/- 5min of TSAT.

- Column ASRT: It sets the time when ST-UP, TAXI or DEPA state is set on the first time.
  - ![#00c000](https://via.placeholder.com/15/00c000/000000?text=+) `DARK GREEN`: Always this color.

- Column CTOT: It shows aircraft's CTOT which can be added, modified or removed.
  - ![#00c000](https://via.placeholder.com/15/00c000/000000?text=+) `DARK GREEN`: Always this color.