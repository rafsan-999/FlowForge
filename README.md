# FlowForge

## Local Install
This version of the FlowForge platform is intended for running on a single machine for a smaller deployment (e.g. evaluation or home user).

## Prerequisites
# Operating System
The install script has been tested against the following operating systems:

*Raspbian/Raspberry Pi OS versions Buster/Bullseye [1]
*Debian Buster/Bullseye
*Fedora 35
*Ubuntu 20.04
*CentOS 8/RHEL 8/Amazon Linux 2
*MacOS Big Sur & Monterey on Intel & Apple M processors
*Windows 10 & 11
*Node.js
*FlowForge requires Node.js v16.

## Linux
The install script will check to see if it can find a suitable version of Node.js. If not, it will offer to install it for you. It will also ensure you have the appropriate build tools installed that are often needed by Node.js modules to build native components.

## Windows/MacOS
If the install script cannot find a suitable version of Node.js, it will exit. You will need to manually install it before proceeding. Information about how to do this can be found on the Node.js website here: https://nodejs.org/en/download

You will also need to install the appropriate build tools.

Windows: the standard Node.js installer will offer to do that for you.
MacOS: you will need the XCode Command Line Tools to be installed. This can be done by running the following 
command:
xcode-select --install

Installing FlowForge
Create a directory to be the base of your FlowForge install. For example: /opt/flowforge or c:\flowforge

For Linux/MacOS:

sudo mkdir /opt/flowforge
sudo chown $USER /opt/flowforge

For Windows:

    mkdir c:\flowforge

Download the latest Installer zip file into a temporary location.

Unzip the downloaded zip file and copy its contents to the FlowForge directory

For Linux/MacOS:
Assumes /tmp/ is the directory where you downloaded flowforge-installer.zip

cd /tmp/
unzip flowforge-installer.zip
cp -R flowforge-installer/* /opt/flowforge

For Windows:
Assumes c:\temp is the directory where you downloaded flowforge-installer.zip

cd c:\temp
tar -xf flowforge-installer.zip
xcopy /E /I flowforge-installer c:\flowforge

Run the installer and follow the prompts

For Linux/MacOS:

cd /opt/flowforge
./install.sh

For Windows:

cd c:\flowforge
install.bat

Installing as a service (optional)
On Linux, the installer will ask if you want to run FlowForge as a service. This will mean it starts automatically whenever you restart your device.

If you select this option, it will ask if you want to run the service as the current user, or create a new flowforge user. If you choose to create the user, it will also change the ownership of the FlowForge directory to that user.

Configuring FlowForge
The default FlowForge configuration is provided in the file flowforge.yml

Linux/MacOS: /opt/flowforge/etc/flowforge.yml
Windows: c:\flowforge\etc\flowforge.yml
The default configuration file already contains everything you need to get started with FlowForge.

It will allow you to access FlowForge and the Node-RED instances you create, from the same server running the platform. If you want to allow access from other devices on the network, you must edit the configuration file and change the host setting to 0.0.0.0 and change base_url to contain the IP address of the server.

NOTE: We do not support changing the host and base_url values once you have created an instance. For more information on all of the options available, see the configuration guide.

Running FlowForge
To run it manually, you can use:

Linux/MacOS:

/opt/flowforge/bin/flowforge.sh

Windows:

c:\flowforge\bin\flowforge.bat

Or to run as a service:

Linux

service flowforge start

First Run Setup
Once FlowForge is started, you will be ready to perform the first run setup.

Follow this guide to continue.

Setting up Mosquitto (optional)
The platform depends on the Mosquitto MQTT Broker to provide real-time messaging between devices and the platform.

This is currently an optional component - the platform will work without the broker, but some features will not be available.

We do not support sharing a broker with other non-FlowForge applications. If you already have mosquitto installed and running, you will need to run a second instance dedicated to FlowForge.

You can either follow the manual install steps, which involve building the authentication plugin from scratch, or make use of the Docker install.

Manual install
Note: if you are running on Windows, you will need to follow the Docker install instructions below due to a limitation of the authentication plugin we use.

Follow the appropriate install instructions for your operating system.

Once installed, you can download pre-built binaries for Linux platforms from here and then jump to step 4 below.

On MacOS you will need to build and install the authentication plugin.

Clone the plugin repository

git clone https://github.com/iegomez/mosquitto-go-auth.git

Follow the instructions on building the plugin

This should result in a file called go-auth.so being generated

Run mosquitto with the configuration file found in the broker directory

You will need to customise the values to match your local configuration:

auth_plugin - set to the path of the go-auth.so file built in the previous step
listener 1883/1884 - if you already have mosquitto running locally, you'll need to change these ports to something else.
auth_opt_http_host / auth_opt_http_port - if you plan to run the platform on a different port, change these settings to match.
mosquitto -c broker/mosquitto.conf
