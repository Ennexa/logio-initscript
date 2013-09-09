logio-initscript
================

Log.io server and harvester init scripts for CentOS 6.4


Installation
------------

Create the directories for the log and pid files

    mkdir -p /var/log/logio/
    mkdir -p /var/run/logio/
    
Change the ownership of the newly created directories to the user running Log.io. (Change logio:logio, with your username and group).

    chown logio:logio /var/log/logio
    chown logio:logio /var/run/logio

Edit the wrapper scripts (available in `wrapper-scripts` directory) and update the `COMMAND` variable to point to the log.io scripts. 

Copy the files to `/usr/local/bin` or any other location of your choice.

Edit the init scripts (available under `init.d` directory) and update the `WRAPPERSCRIPT` variable to point to the location of the corresponding wrapper script.

To start the server, run

    service logio-server start
    
To start the harvester, run

    service logio-harvester start