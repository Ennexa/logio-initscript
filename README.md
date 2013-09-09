logio-initscript
================

Log.io server and harvester init scripts for CentOS 6.4


Installation
------------

## Log.io ##

Add a new user for log.io. Run the following commands as root.

    useradd logio
    usermod -Glogio,adm,compiler logio

Install nodejs and npm, if not already installed

    yum install nodejs npm
	
Login as user logio and install log.io

    su - logio
	npm install log.io

You can now remove user logio from compiler group

    exit # to go back to root shell
	usermod -Glogio,adm logio
	
## Init Script ##

Create the directories for the log and pid files (Run as root).

    mkdir -p /var/log/logio/
    mkdir -p /var/run/logio/
    
Change the ownership of the newly created directories to the user running Log.io. (Change logio:logio, with your username and group).

    chown logio:logio /var/log/logio
    chown logio:logio /var/run/logio

Edit the wrapper scripts (available in `wrapper-scripts` directory) and update the `COMMAND` variable to point to the log.io scripts. 
If you followed the above steps for installing log.io, then this step is not required.

Copy the files to `/usr/local/bin` or any other location of your choice.

Edit the init scripts (available under `init.d` directory) and update the `WRAPPERSCRIPT` variable 
to point to the location of the corresponding wrapper script. If you copied the files to /usr/local/bin, then this step is not required.

Copy the init scripts to `/etc/init.d`

Your configuration files will be under `~log.io/.log.io/` directory. Update the harvester.conf file to add a new harvester.

To start the server, run

    service logio-server start
    
To start the harvester, run

    service logio-harvester start
