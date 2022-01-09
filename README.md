RPi-scheduler
==========

* Creator: Thiemo Schuff, thiemo@schuff.eu
* Source: https://github.com/Starwhooper/RPi-scheduler
* License: CC-BY-SA-4.0

Based on https://github.com/Starwhooper/RPi-433outlets. The RPi-433outlets used a local 433MHz transmitter. 
The https://github.com/Starwhooper/RPi-scheduler send the commands to a ESP01 with 433 transmitter. The benefit of this solution is, that the stearing RPi could place in your Server-Rack and on any other place in your wlan, your clould place the ESP near your outlets.

The sketch and wiring on ESP01, could you find here: https://alexbloggt.com/funksteckdosensteuerung-mit-esp8266/


Prepare your System
-------------------
```bash
sudo apt-get install python3-pip
cd /opt
sudo git clone https://github.com/Starwhooper/RPi-scheduler
```

First configurtion
------------------
```bash
copy /opt/RPi-outlet433/config.json.example /opt/RPi-outlet433/config.json
sudo nano /opt/RPi-outlet433/config.json
```
Change in config.json:
* set "[outlets][*][name]" to Name that you want to identity the outlet
* set "[outlets][*][cmd_on]" to esp01 url
* set "[outlets][*][cmd_off]" to esp01 url
* set "[outlets][*][operations][*][type] to time or calculate
  * case type = "time"
    * set "[outlets][][operations][][on] to time in 24h format. as example 0600 für 6am, 2205 for 5 minutes after 10pm.
  * case type = "calculate"
    * set "[outlets][][operations][][on] to command and offset in mins. As example "sunset;+45" means 45minutes after local sunset. "sunrise;-120" means 2hours before sunrise.

Start service
-----
```bash
/opt/RPi-scheduler/service.py
```
