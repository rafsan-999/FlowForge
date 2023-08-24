# FlowForge
FlowForge helps Node-RED developers deliver applications in a more reliable, collaborative and secure manner. Node-RED’s intuitive, low-code development environment is great for connecting together hardware devices, APIs and online services. FlowForge adds to Node-RED, collaborative development, management of remote deployments, support for DevOps deliver pipelines and the ability to host Node-RED applications on FlowForge Cloud. FlowForge is the devops platform for Node-RED application development and delivery.
#### Official Documentation site
https://flowfuse.com/docs/install/local/
## Local Install
This version of the FlowForge platform is intended for running on a single machine for a smaller deployment (e.g. evaluation or home user).

## Prerequisites
# Operating System
The install script has been tested against the following operating systems:

* Raspbian/Raspberry Pi OS versions Buster/Bullseye [1]
* Debian Buster/Bullseye
* Fedora 35
* Ubuntu 20.04
* CentOS 8/RHEL 8/Amazon Linux 2
* MacOS Big Sur & Monterey on Intel & Apple M processors
* Windows 10 & 11
## Node.js
FlowForge requires Node.js v16.

## Linux
The install script will check to see if it can find a suitable version of Node.js. If not, it will offer to install it for you. It will also ensure you have the appropriate build tools installed that are often needed by Node.js modules to build native components.

## Windows/MacOS
If the install script cannot find a suitable version of Node.js, it will exit. 

You will need to manually install it before proceeding. Information about how to do this can be found on the Node.js website here: https://nodejs.org/en/download

You will also need to install the appropriate build tools.

* Windows: the standard Node.js installer will offer to do that for you.
* MacOS: you will need the XCode Command Line Tools to be installed. This can be done by running the following
#### command:
        xcode-select --install

# Installing FlowForge
1. Create a directory to be the base of your FlowForge install. For example: /opt/flowforge or c:\flowforge

For Linux/MacOS:

        sudo mkdir /opt/flowforge
        sudo chown $USER /opt/flowforge

For Windows:

        mkdir c:\flowforge

2. Download the latest Installer zip file into a temporary location.
3. Unzip the downloaded zip file and copy its contents to the FlowForge directory

# For Linux/MacOS:
Assumes /tmp/ is the directory where you downloaded flowforge-installer.zip

        cd /tmp/
        unzip flowforge-installer.zip
        cp -R flowforge-installer/* /opt/flowforge

# For Windows:
Assumes c:\temp is the directory where you downloaded flowforge-installer.zip

        cd c:\temp
        tar -xf flowforge-installer.zip
        xcopy /E /I flowforge-installer c:\flowforge

##### 4.Run the installer and follow the prompts

# For Linux/MacOS:

        cd /opt/flowforge
        ./install.sh

# For Windows:

        cd c:\flowforge
        install.bat

### Installing as a service (optional)
On Linux, the installer will ask if you want to run FlowForge as a service. This will mean it starts automatically whenever you restart your device.

If you select this option, it will ask if you want to run the service as the current user, or create a new flowforge user. If you choose to create the user, it will also change the ownership of the FlowForge directory to that user.

# Configuring FlowForge
The default FlowForge configuration is provided in the file flowforge.yml

* Linux/MacOS:

        /opt/flowforge/etc/flowforge.yml
  
* Windows:

        c:\flowforge\etc\flowforge.yml

The default configuration file already contains everything you need to get started with FlowForge.
It will allow you to access FlowForge and the Node-RED instances you create, from the same server running the platform. If you want to allow access from other devices on the network, you must edit the configuration file and change the host setting to 0.0.0.0 and change base_url to contain the IP address of the server.

NOTE: We do not support changing the host and base_url values once you have created an instance. For more information on all of the options available, see the configuration guide.

Running FlowForge
To run it manually, you can use:

# Linux/MacOS:

        /opt/flowforge/bin/flowforge.sh

# Windows:

        c:\flowforge\bin\flowforge.bat

Or to run as a service:

# Linux

        service flowforge start
        
## Check Flowforge status

        systemctl status flowforge

# First Run Setup

Once FlowForge is started, you will be ready to perform the first run setup.
Following a successful install, you will be able to access the platform to go through the initial setup.

1. Start setup
Open FlowForge in your browser http://localhost:3000.


# Uninstall FlowForge
Type the following command and press Enter to uninstall FlowForge:

        sudo apt remove flowforge
This command will remove the FlowForge package from your system.

### Remove Configuration Files
If you want to remove the configuration files associated with FlowForge, you can use the following command:

        sudo apt purge flowforge
This will remove the package as well as its configuration files.

## Update Package List
After uninstalling FlowForge, it's a good idea to update your package list to ensure your system is up-to-date:

        sudo apt update






