FROM selenium-node-base:latest
LABEL authors="Selenium <selenium-developers@googlegroups.com>, Xavier-Alexandre BROCHARD <xavier.alexandre.brochard@gmail.com>"

USER 0

#========
# GTK package required for FireFox
#========
RUN yum -y install gtk3

#=========
# bzip2 package to extract Firefox
#=========
RUN yum -y update \
  && yum -y --setopt=tsflags=nodocs install bzip2 \
  && yum -y clean all \
  && rm -rf /var/cache/yum

#=========
# Firefox
#=========
ADD https://download-installer.cdn.mozilla.net/pub/firefox/releases/80.0.1/linux-x86_64/en-US/firefox-80.0.1.tar.bz2 firefox.tar.bz2
RUN  tar -xvjf firefox.tar.bz2 --directory=/opt \
  && rm firefox.tar.bz2 \
  && ln -fs /opt/firefox/firefox /usr/bin/firefox

#============
# GeckoDriver
#============
ADD https://github.com/mozilla/geckodriver/releases/download/v0.27.0/geckodriver-v0.27.0-linux64.tar.gz geckodriver.tar.gz
RUN  tar -xvf geckodriver.tar.gz --directory=/opt \
  && rm geckodriver.tar.gz \
  && ln -fs /opt/geckodriver /usr/bin/geckodriver

#============
# pulseaudio package to support WebRTC audio streams
#============
RUN yum -y --setopt=tsflags=nodocs install pulseaudio \
  && yum -y clean all \
  && rm -rf /var/cache/yum

COPY generate_config /opt/bin/generate_config
RUN chmod g+x /opt/bin/generate_config

#============
# Generate a default config during build time
#============
RUN /opt/bin/generate_config > /opt/selenium/config.json \
  && chmod 777 /opt/selenium/config.json

CMD ["/opt/bin/entry_point.sh"]