FROM selenium-base
LABEL authors="Selenium <selenium-developers@googlegroups.com>, Xavier-Alexandre BROCHARD <xavier.alexandre.brochard@gmail.com>"

USER 0

#==============
# Xvfb
#==============
RUN  yum install -y --setopt=tsflags=nodocs xorg-x11-server-Xvfb \
  && yum -y clean all \
  && rm -rf /var/cache/yum

#==============================
# Scripts to run Selenium Node
#==============================
COPY entry_point.sh \
  functions.sh \
  /opt/bin/
RUN chmod g+x /opt/bin/entry_point.sh /opt/bin/functions.sh

#============================
# Some configuration options
#============================
ENV SCREEN_WIDTH 1360
ENV SCREEN_HEIGHT 1020
ENV SCREEN_DEPTH 24
ENV DISPLAY :99.0

#========================
# Selenium Configuration
#========================
# As integer, maps to "maxInstances"
ENV NODE_MAX_INSTANCES 1
# As integer, maps to "maxSession"
ENV NODE_MAX_SESSION 1
# As integer, maps to "port"
ENV NODE_PORT 5555
# In milliseconds, maps to "registerCycle"
ENV NODE_REGISTER_CYCLE 5000
# In milliseconds, maps to "nodePolling"
ENV NODE_POLLING 5000
# In milliseconds, maps to "unregisterIfStillDownAfter"
ENV NODE_UNREGISTER_IF_STILL_DOWN_AFTER 60000
# As integer, maps to "downPollingLimit"
ENV NODE_DOWN_POLLING_LIMIT 2
# As string, maps to "applicationName"
ENV NODE_APPLICATION_NAME ""

# Following line fixes https://github.com/SeleniumHQ/docker-selenium/issues/87
ENV DBUS_SESSION_BUS_ADDRESS=/dev/null
