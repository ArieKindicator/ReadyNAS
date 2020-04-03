# Package for ReadyNAS

Required firmware version: ReadyNAS OS 6, all architectures.

Tested on: ReadyNAS OS6, version 6.10.3, amd64, RN426

## Application: Medusa

### Package info
This package acts as a *wrapper* and installs Medusa from [source](https://github.com/pymedusa/Medusa/) and adds the required ReadyNAS package files, such as logo.png, config.xml, etc.

This package installs a *stock release* of the latest available Medusa release.

Medusa runs as daemon, and uses a pidfile to gracefully shutdown all processes.

Medusa starts with these parameters: `-d --pidfile=/apps/medusa/medusa.pid` All other options are fully customizable. Note: the pidfile is required,  to be able to toggle Medusa on or off.

#### How to update Medusa
Use the update option of Medusa (`Check For Updates`)

### Additional information
Medusa requires

* Python 2 – 2.7.10 and above, or
* Python 3 – 3.5.0 and above (Note: Python 3.5.0 or higher is n't available on ReadyNAS OS6, yet; April 2, 2020)

Medusa runs as daemon, and uses a pidfile to gracefully shutdown all processes.


  File: fvapp-medusa.service
  
  `Type=forking`
  
  `PIDFile=/apps/medusa/medusa.pid`
  
  `KillMode=process`


These parameters are necessary to use the PIDfile [PID files of services vs. systemd](https://lists.debian.org/debian-user/2016/10/msg00422.html)

Medusa starts with these parameters: `-d --pidfile=/apps/medusa/medusa.pid` All other options are fully customizable. Note: the pidfile is required,  to be able to toggle Medusa on or off.

## FAQ
* Migrate from Python2 to Python3

  * Make a backup of the main database file and configuration using the build-in backup and restore option of Medusa. Deinstall and reinstall Medusa for Python3.

Or
    * Shutdown Medusa and edit the `fvapp-medusa.service` file in `/apps/medusa`.
Change `/usb/bin/phython2` to `/usb/bin/phython3` in `ExecStart=/usr/bin/python2 /apps/medusa/start.py -d --pidfile=/apps/medusa/medusa.pid`
