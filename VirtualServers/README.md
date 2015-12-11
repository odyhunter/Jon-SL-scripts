**Jon-SL-scripts/VirtualServers**
==============

Script | Description
------ | -----------
PowerOffVirtualServers.py| Soft Shutdown, then power off virtual servers listed in order contained in CSV file
PowerOnVirtualServers.py| Power on virtual server in controlled fasion listed in order contained in CSV file
ShowVirtualServerPowerState.py| Show power state for all Virtual Server in specified datacenter
DeprovisionVirtualServer.py| Deprovision a virtual server
ProvisionVirtualServer.py| Provision a virtual server

The *PowerOffVirtualServers.py* script can be used to systematically power off VSI's after an OS soft shutdown 
is completed and leaves the VSI permenently in the poweroff state in preparation for a SoftLayer maintenance window. 
The *PowerOnVirtualServers.py* script can be used to systematically power on VSI's after a SoftLayer maintenance window.

Both scripts require a CSV file with the list of VSI's to be powered on or off and their order.   The CSV filename
can be passed as a paramenter using the follwing command line parameter

```
script.py -i filename.csv
```

*CSV Requirements*

Field | Required |Field Description
----- | -------- |-----------------
Order | Optional |field for tracking or sorting.  Not used by script
ID    | Optional |VSI ID (found via SLCLI VS LIST). If specified it will used instead of hostName (prefered). 
HOSTNAME|Required|SL Hostname. Must be unique if you don't specify the correct VSI ID.  Script will it look up.
WAIT  | Required |Number of seconds to wait after powering on or off VM before moving to next VSI

Example CSV file
```
Order,id,hostname,wait
1,13405579,centos02,60
2,13405577,centos01,30
3,13405581,centos03,30
```
The *ShowVirtualServerPowerState.py* script can be used to verify status after running script.  This script does not
require input and instead lists all VSI's in a Datacenter.


**Installation of SL API**

Install via pip:
```
$ pip install softlayer
```
Or you can install from source. Download source and run:

```
$ python setup.py install
```
The most up to date version of this library can be found on the SoftLayer GitHub public repositories: http://github.com/softlayer. Please post to the SoftLayer forums http://forums.softlayer.com/ or open a support ticket in the SoftLayer customer portal if you have any questions regarding use of this library.

**Installation of Jon-SL-scripts**

Download scripts into directory.

**Configuration of Jon-SL-scripts**
There are two methods to configure the USERNAME and API key to use with these scripts.


Create a config.ini file with your username and API key.  If you have not already generated a SoftLayer APIKEY log into http://control.softlayer.com, select Account - Users, click on Generate, then click View to view the API Key.  This value along with your username should be included in the config.ini file.  By default the script will read the config.ini file in the same directory as the script.   You can specify and alternate file or location with the -c argument.
```
[api]
username=  <== SoftLayer Username goes here.
apikey=   <== Softlayer APIKEY goes here.
```

Pass your username and APIKEY via command line argument
```
usage: script.py [-h] [-u USERNAME] [-k APIKEY] [-c CONFIG]

optional arguments:
  -h, --help            show this help message and exit
  -u USERNAME, --username USERNAME
                        SoftLayer API Username
  -k APIKEY, --apikey APIKEY
                        SoftLayer APIKEY
  -c CONFIG, --config CONFIG
                        config.ini file to load
```