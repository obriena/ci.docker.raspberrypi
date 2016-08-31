# ci.docker.raspberrypi
Dockerfiles for building Liberty images to run on Raspberry Pi.

To build an image that can run on the Raspberry Pi you must run the buildfile in the "kernel" directory first, saving it as "websphere-liberty:kernel". You can then run the Dockerfile in the "basicfeatures" directory. In the basic features Dockerfile there is a commented out line which can be un-commented to add a web application to the image - the application needs to be in the same directory as the Dockerfile - just make sure to update the name in the Dockerfile to match that of the app.

You need to run the Docker files on a Raspberry Pi to ensure the OS components can run and install, and that the Java version downloaded will be correct for the ARM CPU in the Pi.

These files have been tested running Docker 1.12 on a Raspberry Pi 3 - it should be compatible on other Raspberry Pi models.

For more info please see this article on WASdev.net: 
