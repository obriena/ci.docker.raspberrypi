# ci.docker.raspberrypi
Dockerfiles for building Liberty images to run on Raspberry Pi.

To build an image that can run on the Raspberry Pi you must:
1. run the buildfile in the "kernel" directory, saving it as "websphere-liberty:kernel". 
2. Run the Dockerfile in the "basicfeatures" directory. 
 
In the basicfeatures Dockerfile there is a commented-out line which can be un-commented to add a web application to the image - the application needs to be in the same directory as the Dockerfile - just make sure to update the name in the Dockerfile to match that of the app and it will be added when the image is built.

You need to run the Docker files on a Raspberry Pi to ensure the OS components can run and install, and that the Java version downloaded will be correct for the ARM CPU in the Pi.

These files have been tested running Docker 1.12 on a Raspberry Pi 3 - it should be compatible on other Raspberry Pi models.

Any questions/issues/comments please email tom.banks@uk.ibm.com
