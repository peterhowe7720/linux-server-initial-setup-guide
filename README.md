Linux Server Initial Setup Guide
================================

# Overview

This guide is designed to be used after the initial installation of Linux has been completed.  The installation of Linux can be carried out using the [Linux Server Installation Guide](https://github.com/freewayprojects/linux-server-installation-guide).

So, this guide should be used to pick up from where [Linux Server Installation Guide](https://github.com/freewayprojects/linux-server-installation-guide) finished.

For the purposes of this guide we are going to carry out the initial set up on a server which has the FQDN of server1.example.com

# Prerequisites

The initial Linux server installation should have been completed.  This could be any distribution or version of Linux - this guide is intended to be generic as well as having distribution/version specific code snippets.

The main points about the server which should already have been set up are:

* Linux base operating system installed.
* BIOS clock set correctly.
* SSH server installed and available
* Initial administration user created.  This user will be used to login to the server and is separate from the root user.
* Network address configured.
* The hostname and domain should be set up so that the server has a FQDN available.

Basically, the administrator should be able to login to the server over SSH to carry out the intial setup.  This is normally the point at which a hardware server has been put into a rack or located at its permanent location - or when a VM has been built and is available over a network.

# Setup steps

## Checking the operating system datetime

In the server installation the server BIOS clock should have been set correctly.  It is very important that the server operating system is reporting the correct datetime and timezone as well.  The package managers, logging tools, certificates etc rely on the server time clock being correct.

### Reading the current datetime

To start with the server datetime should be checked.  On most Linux servers the date and time can be checked by running the date command.

| Disttribution | Versions |
| --- | --- |
| Debian | All versions |
| Ubuntu | All versions |
| SLES | All versions |
| RH | All versions |
| Centos | All versions |

~~~
server1admin@server1:~$ date
Thu Jul  4 13:38:36 BST 2013
~~~

### Correcting timezone

If the timezone is not correct then this should be corrected.

| Disttribution | Versions |
| --- | --- |
| Debian | All versions |
| Ubuntu | All versions |

~~~
# dpkg-reconfigure tzdata
~~~

Then follow the onscreen prompts.

### Changing the server datetime

Obviously, the server BIOS datetime should have been set correctly during the operating system installation.  This should mean that the time reported by the operating system should be roughly correct and take into account any adjustments such as timezone and summer time adjustments.

NB - The server BIOS time should be set to UTC.  In Linux it is the operating system which adjusts datetime for time zones and Daylight Saving Time adjustments.

Later in this set up guide the server will be set up to use internet time servers to keep the server times correct.

If necessary the server datetime can be corrected.

| Disttribution | Versions |
| --- | --- |
| Debian | All versions |
| Ubuntu | All versions |

~~~
# date 070413462013
~~~

will set the date time to 1:46pm, 4th July, 2013.

##  Install screen

The tool [Screen](http://www.gnu.org/software/screen/) means that commands can be run under a remote session on the server.  This means that if your connection to the server is lost whilst you are carrying out commands then you can log back in to the server and pick up the session again.  This makes it much safer to carry out tasks remotely such as installing software.

| Disttribution | Versions |
| --- | --- |
| Debian | All versions |
| Ubuntu | All versions |

~~~
# apt-get install screen
~~~
