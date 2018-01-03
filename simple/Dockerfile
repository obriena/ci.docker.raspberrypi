# (C) Copyright IBM Corporation 2015, 2016.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

#download Raspberry Pi compatible OS components.
FROM ioft/armhf-ubuntu:14.04

MAINTAINER Thomas Banks <tom.banks@uk.ibm.com> (@tom_will_banks)

RUN apt-get update \
    && apt-get install -y --no-install-recommends unzip \
    && apt-get -y install openjdk-7-jre \
    && apt-get -y install wget

#can optionally delete the apt-get update files to save on image size at this point

# Install WebSphere Liberty
ENV LIBERTY_VERSION 17.0.0.4
ARG LIBERTY_URL
ARG DOWNLOAD_OPTIONS=""

RUN wget https://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/17.0.0.4/wlp-kernel-17.0.0.4.zip -O /tmp/wlp.zip
RUN unzip /tmp/wlp.zip -d /opt/ibm
RUN rm /tmp/wlp.zip

ENV PATH=/opt/ibm/wlp/bin:$PATH

# Set Path Shortcuts
ENV LOG_DIR=/logs \
    WLP_OUTPUT_DIR=/opt/ibm/wlp/output
RUN mkdir /logs \
    && ln -s $WLP_OUTPUT_DIR/defaultServer /output \
    && ln -s /opt/ibm/wlp/usr/servers/defaultServer /config

# Configure WebSphere Liberty
RUN /opt/ibm/wlp/bin/server create \
    && rm -rf $WLP_OUTPUT_DIR/.classCache /output/workarea
EXPOSE 9080 9443

#Added from the basicfeatures folder
#copy a server.xml over from same directory as this dockerfile - customize your server config there first
COPY server.xml /config/

RUN if [ ! -z $REPOSITORIES_PROPERTIES ]; then mkdir /opt/ibm/wlp/etc/ \
    && echo $REPOSITORIES_PROPERTIES > /opt/ibm/wlp/etc/repositories.properties; fi \
    && installUtility install --acceptLicense \
    servlet-3.1 jsp-2.3 websocket-1.1 localConnector-1.0 \
    && if [ ! -z $REPOSITORIES_PROPERTIES ]; then rm /opt/ibm/wlp/etc/repositories.properties; fi \
    && rm -rf /output/workarea /output/logs

#uncomment the below line and the change app name to match that of an app in same dir as this Dockerfile to
#install the app into your image
#COPY appname.war /opt/ibm/wlp/usr/servers/defaultServer/dropins/

CMD ["/opt/ibm/wlp/bin/server", "run", "defaultServer"]
