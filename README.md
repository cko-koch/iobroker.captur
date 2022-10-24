![Logo](admin/captur.jpg)
# iobroker.captur
=================

If this adapter is not available on the ioBroker-Admin-View, please use the following command to install it (from command-line on your ioBroker-Server):

```npm install https://github.com/cko-koch/iobroker.captur/tarball/master/```

Or you can use the GitHub-Button (labeled: install from own URL) in the Adapter-View and enter this URL on the "other"-Tab. This can also be used to update to the current adapter-version:

```https://github.com/cko-koch/iobroker.captur/tarball/master/```

You can use the method to update the adapter to the most recent version.


After that the adapter should show up in the ioBroker-Admin-View.

### Configuration

- You have to set username, password and VIN as you have done in my renault app
- This locales ("Laenderversionen") currently do work: de_DE
- Maybe you need a My-Z.E.Connect or similar services from Renault to use this
- After saving it took around 15 minutes to create the objects (zoe.0 and so on)

### Features

- Read this parameters from Zoe:
   - charge_level in percent
   - charging as boolean
   - plugged on as boolean
   - remaining range in kilometer
   - remaining time of charging
   - calculated endPoint of charing (charging_finished_at)
   - battery temperature
   - external temperature (not that accurate)
   - chargingPower
   - batteryCapacity
   - batteryAvailableEnergy
   - gpsLatitude and gpsLongitude, works only on newer ZOEs
- Write this parameters:
   - preconNow: starts precon/hvac (write true to that node, or press the button)
   - chargeCancel: stops charging
   - chargeEnable: enables charging
   

Control Charging:

With the two buttons chargeCancel and chargeEnable charging functionality can be controlled. If chargeCancel is pressed
(or true is written to this parameter), the charging function is disabled. ZOE should not charge if the power cord is
connected. On my 1st Gen ZOE this has no effect, so maybe it works on newer ZOEs?

As soon as chargeEnable is pressed (or true is written to this parameter), the charging function should work again.

How is this done: chargeEnable creates a charging-schedule that starts at the given hour you defined in the setup screen 
every day and lasts for 15 minutes. That looks as it is the shortest amount to be set. Turning charging off complete is 
not possible with the current API (or that parts of the current API that are known).


Some parameters only work on newer ZOEs.

### Testet with the folowing ZOEs:
- Zoe Phase 2 (Thanks Jack-RK-24)
- Zoe R210 (1st Generation, tested by fungus75)
- Zoe R90 (Thanks arturwolf)

### Please Note!!

Communication with ZOE or Renault-Services is done only during the interval-times with is 10 Minutes.
So if you press preconNow or chargeNow, it will take up to the next interval to send it to ZOE and it will take up to the
very next interval to get the status back.

The new ZOE API from Renault seems to be very lacy. That means that it only shows new values when there is something important.
As far as I found out, the most important thing is battery-level. That means i.E. the external temperature is not updated,
if the car stands at home. Only if i.E. the ZOE charges, the external temperature will be updated. If charging is finished,
still no new update. When driving, the battery level gets lower and lower and therefore it should update very regulary.

### Thanks  

https://michael-heck.net/index.php/elektromobilitaet/renault-zoe-ins-smarthome-integrieren, 
https://michael-heck.net/index.php/elektromobilitaet/renault-zoe-im-smarthome-neue-api-2020,
https://muscatoxblog.blogspot.com/2019/07/delving-into-renaults-new-api.html,
https://github.com/edent/Renault-Zoe-API,
https://github.com/jamesremuscat/pyze and 
https://github.com/hacf-fr/renault-api
for your great documentation and work.




## Changelog

### 0.2.6 (2022-07-22)
- API Timeout configurable via config-screen
- Improved stability

### 0.2.5 (2022-03-30)
- Better error messages if kameronapikey changed
- Link to github-wiki added to admin-screen
- updated dependencies

### 0.2.4 (2022-02-16)
- Replaced obsolete Request-Library by axios
- Code-Adjustments

### 0.2.3 (2021-07-29)
- Code Adjustments, Error-Handling

## License
The MIT License (MIT)

Copyright (c) 2021 RenePilz <rene@pilz.cc>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.


