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

FROM websphere-liberty:kernel
#you should pre-build this for the pi from the kernel Docker files (in same Git repo)

ARG REPOSITORIES_PROPERTIES=""

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
