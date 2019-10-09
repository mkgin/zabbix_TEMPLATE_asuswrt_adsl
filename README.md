# Zabbix Asuswrt xDSL

Zabbix template for monitoring Asus ADSL Modem router running asuswrt.

* works with VDSL, some parameter are diffierent
* Requires zabbix-agent running on the modem.
  * tested using zabbix packages from Entware-ng.
* Most information is parsed from /tmp/adsl/info_adsl.txt
  * The zabbix-agent needs to be able to read the file ( chmod 755 /tmp/adsl ) if zabbix-agent is not running as the admin user
  * this file might not always be present or not always contain a line with the parameter being checked so at times a value may be empty. Possibly zabbix is tring collect information when the file is being updated.
  * Check the Asus wrt firmware version need a user parameter
     * `UserParameter=nvram.get[*],nvram get $1`  #monitor other parameters 
	 * `UserParameter=nvram.get.innerver,nvram get innerver` #more secure

Some of the items collected:

* Line Status
* DSL Connection Standard and mode info
* SNR
* Data rate
* Error counts UP and down: 
  * FEC (forward error checksum)
  * CRC
  * HEC (header error checksum)

###Notes:
Restaring zabbix:
```
cd /opt/etc/init.d/
./S07zabbix_agentd restart
```

###TODO:
* Collect some DSL configuration information (help correlate configuration changes with measurements)
* calculate increases in errors over a period of time.
* more alerts
* version
  * this... with nvram get ```./state.js:FWString = firmver+"."+buildno;
  ./state.js:FWString += "_"+extendno.split("-g")[0]```
* proper DSL uptime.
* calculate errors, over uptime ? hourly?
* change in errors, per 10 minutes?
