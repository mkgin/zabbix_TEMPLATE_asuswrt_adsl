# Zabbix Asuswrt xDSL

Zabbix template for monitoring Asus ADSL Modem router running asuswrt.

* Used and tested on an Asus DSL-AC68U 
* works with ADSL and VDSL, some parameters are different
* Requires zabbix-agent running on the modem.
  * tested using zabbix packages from Entware-ng.
* Most information is parsed from /tmp/adsl/info_adsl.txt
  * The zabbix-agent needs to be able to read the file ( chmod 755 /tmp/adsl ) if zabbix-agent is not running as the admin user
  * this file might not always be present or not always contain a line with the parameter being checked so at times a value may be empty. Possibly zabbix is tring collect information when the file is being updated.
  * Checking the Asus wrt firmware version needs a user parameter
    `UserParameter=nvram.get_version,echo "$(nvram get firmver).$(nvram get buildno)_$(nvram get extendno)"`

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

### Update

* Many of the items changed to Dependent items and take advantage of preprocessing
* proper DSL uptime calculated with some regex and javascript
  * but likely needs testing
* I'm unlikely to develop this much more as I decided to switch to simpler DSL modem that could operate in bridged mode
