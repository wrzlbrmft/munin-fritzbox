# munin-fritzbox

This [Munin](http://munin-monitoring.org/) plugin lets you monitor the daily web
traffic of an [AVM FRITZ!Box](http://avm.de/produkte/fritzbox/) DSL router.

**IMPORTANT NOTE:** I wrote this plugin for my FRITZ!Box Fon 7170, which runs
the classic firmware version 29.04.81. Therefore, this plugin does not yet
support FRITZ!Box models running FRITZ!OS. For more information see this AVM
Technical Note: 
[Session-IDs im FRITZ!Box Webinterface](http://avm.de/fileadmin/user_upload/Global/Service/Schnittstellen/AVM_Technical_Note_-_Session_ID.pdf)
(PDF, German).

## Requirements

* A FRITZ!Box model running firmware version xx.04.74+ (FRITZ!OS is not yet
supported)
* ```/bin/bash```
* [cURL](http://curl.haxx.se/)
* [iconv](https://www.gnu.org/software/libiconv/)
* md5sum
* [Munin](http://munin-monitoring.org/) ;-)

## Setup

To install the required software under Ubuntu or any other Debian-based Linux,
simply run:

```
apt-get install curl munin munin-node
```

Next, download *munin-fritzbox* either as a
[ZIP file](https://github.com/wrzlbrmft/munin-fritzbox/archive/master.zip) or use
Git:

```
git clone https://github.com/wrzlbrmft/munin-fritzbox.git
```

## Configuration

*munin-fritzbox* consists of a single script file named ```fritzbox_```. To set
the URL and password of your FRITZ!Box, edit the config section at the beginnign
of the script:

```bash
# --- config ---
HOSTNAME="fritz.box"
PASSWORD="*****"
# --- /config ---
```

The script can generate three different Munin graphs:

* Downloaded traffic
* Uploaded traffic
* Both downloaded/uploaded traffic combined in one graph

Munin plugins are activated by symlinking them from the plugins directory,
usually located at ```/etc/munin/plugins```.

To activate the combined graph, symlink the script with its original file name:

```
cd /etc/munin/plugins
ln -s /path/to/munin-fritzbox/fritzbox_
```

To activate the download graph, create a symlink with ```down``` appended to the
file name:

```
cd /etc/munin/plugins
ln -s /path/to/munin-fritzbox/fritzbox_ fritzbox_down
```

To activate the upload graph, create a symlink with ```up``` appended to the
file name:

```
cd /etc/munin/plugins
ln -s /path/to/munin-fritzbox/fritzbox_ fritzbox_up
```

Finally, restart Munin:

```
/etc/init.d/munin-node restart
```

