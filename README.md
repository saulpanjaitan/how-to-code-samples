# Earthquake Detector


## Introduction

This earthquake detector application is part of a series of how-to Intel� IoT code sample exercises using the Intel� IoT Developer Kit, Intel� Edison development platform, cloud platforms, APIs, and other technologies.

From this exercise, developers will learn how to:
- Connect the Intel� Edison development platform, a�computing platform designed for prototyping and producing IoT and wearable computing products.
- Interface with the Intel� Edison platform IO and sensor repository using MRAA and UPM from the Intel� IoT Developer Kit, a complete hardware and software solution to help developers explore the IoT and implement innovative projects.
- Run this code sample in Intel� XDK IoT Edition, an IDE for�creating new applications that interact with sensors, actuators, and so on, enabling you to get a quick start on developing software for your Intel� Edison or Galileo board.
- Invoke the services of the United States Geological Survey* API for accessing earthquake data.

## What It Is

Using an Intel� Edison board, this project lets you create a earthquake detector that:
- senses motion using the digital accellerometer;
- checks live earthquake data, using the USGS* API.
- displays the earthquake on the LCD;

## How It Works

This earthquake detector will listen for vibrations using the accelerometer.

When it thinks it detects an earthquake, it will attempt to verify with the USGS API that an earthquake occurred

It will then use the LCD Display to either warn of the quake, or let you know it was  a false alarm.


## Hardware requirements

Grove* Starter Kit containing:

1. Intel� Edison with an Arduino* breakout board
2. [Grove* 3-Axis Digital Accelerometer](http://iotdk.intel.com/docs/master/upm/node/classes/mma7660.html)
3. [Grove* RGB LCD](http://iotdk.intel.com/docs/master/upm/node/classes/jhd1313m1.html)

## Software requirements

1. [Eclipse* Iot version](https://software.intel.com/en-us/eclipse-getting-started-guide)

## How To Setup

To begin, clone the Intel IoT Examples with git on your computer:

    $ git clone https://github.com/hybridgroup/intel-iot-examples.git

Not sure how to do that? [Here is an excellent guide from Github on how to get started](https://help.github.com/desktop/guides/getting-started/).

Just want to download a ZIP file? Just point your web browser to the Github repo at [https://github.com/hybridgroup/intel-iot-examples](https://github.com/hybridgroup/intel-iot-examples) and click on the "Download ZIP" button at the lower right. Once the ZIP file has finished downloading, uncompress it, and then use the files in the directory for this example.

### Adding The Code To Eclipse IoT

You use the Eclipse "Import Wizard" to import an existing project into the workspace as follows:

- From the main menu bar, select "File > Import..."
![](./../../../images/cpp/cpp-eclipse-menu.png)

- The "Import wizard" dialog will open.
![](./../../../images/cpp/cpp-eclipse-menu-select-epiw.png)

- Select "General > Existing Project into Workspace" and click on the "Next" button.
![](./../../../images/cpp/cpp-eclipse-menue-epiw-rootdir.png)

- Choose "Select root directory", then click on the associated "Browse" button to locate the directory that contains the project files.
![](./../../../images/cpp/cpp-eclipse-menu-select-rootdir.png)

- Under "Projects" select the directory with the project files which you would like to import.
![](./../../../images/cpp/cpp-eclipse-menue-epiw-rootdir.png)
- Click on the "Finish" button to import the files into Eclipse.

![](./../../../images/cpp/cpp-eclipse-menu-src-loc.png)
- Your main .cpp program will now be in your workspace under the src folder.

### Connecting The Grove* Sensors

![](./../../../images/js/earthquake-detector.jpg)

You will need to have the Grove* Shield connected to the Arduino-compatible breakout board, in order to plug in all the various Grove* devices into the Grove* shield. Make sure you have the tiny VCC switch on the Grove* Shield set to the "5V" position.

Plug one end of a Grove* cable into the "Accelerometer", then connect the other end to any of the "I2C" ports on the Grove* Shield.

Plug one end of a Grove* cable into the "RGB LCD", then connect the other end into any of the "I2C" ports on the Grove* Shield.

### Intel Edison Setup

This example uses the `restclient-cpp` library to perform REST calls to the server. The code for `restclient-cpp` can be found in the `lib` directory. The `restclient-cpp` library requires the `libcurl` package, which is already installed on the Intel Edison by default.

Update the opkg base feeds, so you can install the needed dependencies. Instructions on how to do this are located here: http://alextgalileo.altervista.org/edison-package-repo-configuration-instructions.html
If you've already done this, you can skip to the next step.

Now, install the boost libraries onto the Edison, by running:
```
opkg update
opkg install boost-dev
```

## Copy the Libraries
Next, you need to copy the libraries and include files from the Edison to your machine where you run Eclipse, so the G++ Cross Compiler and G++ Cross Linker can find them. The easiest way to do this is by running the `scp` command from your computer (NOT the Edison).

```
scp -r USERNAME@xxx.xxx.x.xxx:/usr/include/boost ~/Downloads/iotdk-ide-linux/devkit-x86/sysroots/i586-poky-linux/usr/include
scp USERNAME@xxx.xxx.x.xxx:/usr/lib/libboost* ~/Downloads/iotdk-ide-linux/devkit-x86/sysroots/i586-poky-linux/usr/lib
```
Change the `USERNAME@xxx.xxx.x.xxx` to match whatever username and IP address that you have set your Edison to.

Change `~/Downloads/iotdk-ide-linux` to match the location on your machine where you have installed the Eclipse IoT Development Kit.

## Copy the Libraries on Windows

We have a helpful link to get this set up here. https://github.com/hybridgroup/intel-iot-examples/blob/master/cpp/docs/using-winscp.md

### Running The Code On Edison

When you're ready to run the example, you can click on the "Run" icon located in the menubar at the top of the Eclipse editor.
This will compile the program using the Cross G++ Compiler, link it using the Cross G++ Linker, transfer the binary to the Edison, and then execute it on the Edison itself.

## Data Store Server Setup

You can optionally store the data generated by this example program in a backend database deployed using Node.js, and the Redis datastore. You use your own account on a hosted service such as Microsoft Azure or IBM Bluemix.

For information on how to setup your own cloud data server, go to:

https://github.com/hybridgroup/intel-iot-examples-datastore

### Connecting Your Edison to the Eclipse IDE

![](./../../../images/cpp/cpp-connection-eclipse-ide-win.png)
1. In the bottom left corner right-click in the area "Target SSH Conections" select "New..." then select "Connection..." and a new screen will appear. 

![](./../../../images/cpp/cpp-connection-eclipse-ide-win2.png)
2. In the "filter box" type the name of your edison. In the example mine is JustinEdison.

![](./../../../images/cpp/cpp-connection-eclipse-ide-win3.png)
3. In the "Select one of the found connections list; click on your device name. Then Ok. 

![](./../../../images/cpp/cpp-connection-eclipse-ide-win4.png)
4. Your device will now appear in the "Target SSH Connections" area. Right-clickt it and select connect. 
(If promted for a username and password the user is 'root' and password is whatever you set it up as when configuring the Edison board)

### Running The Example With The Cloud Server

To run the example with the optional backend datastore you need to set the `SERVER` and `AUTH_TOKEN` environment variables. You can do this in Eclipse by:

1. Select the "Run" menu and choose "Run Configurations". The "Run Configurations" dialog will be displayed.
2. Click on "earthquake-detector" under "C/C++ Remote Application". This will display the information for your application.
3. Add the environment variables to the field for "Commands to execute before application" so it ends up looking like this, except using the server and auth token that correspond to your own setup:

```
chmod 755 /tmp/earthquake-detector; export SERVER="http://intel-examples.azurewebsites.net/counter/earthquake-detector/inc"; export AUTH_TOKEN="YOURTOKEN"
```

4. Click on the "Apply" button to save your new environment variables.

Now when you run your program using the "Run" button, it should be able to call your server to save the data right from the Edison.

### Running The Code On Edison

![](./../../../images/cpp/cpp-run-eclipse.png)

When you're ready to run the example, you can click on the "Run" icon located in the menubar at the top of the Eclipse editor.
This will compile the program using the Cross G++ Compiler, link it using the Cross G++ Linker, transfer the binary to the Edison, and then execute it on the Edison itself.

![](./../../../images/cpp/cpp-run-eclipse-successful-build.png)

After running the program you should have a similar output as in the image above. 

![](./../../../images/cpp/cpp-run-eclipse-successful-output.png)

When the the program loads correctly your RGB-LCD screen will display "quakebot ready."

If you shake the accelerometer it will check to see if there really was an earthquake!




