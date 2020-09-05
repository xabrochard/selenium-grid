FROM selenium-node-base:latest
LABEL authors="Selenium <selenium-developers@googlegroups.com>, Xavier-Alexandre BROCHARD <xavier.alexandre.brochard@gmail.com>"

USER 0

#============================================
# Fix the rights issues described here
# https://github.com/electron/electron/issues/2778
#============================================
RUN chmod -R 777 /home/jboss

#============================================
# Google Chrome
#============================================
ADD https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm chrome.rpm
RUN  yum install -y --setopt=tsflags=nodocs chrome.rpm \
  && rm chrome.rpm \
  && yum -y clean all \
  && rm -rf /var/cache/yum

#=================================
# Chrome Launch Script Wrapper
#=================================
COPY wrap_chrome_binary /opt/bin/wrap_chrome_binary
RUN  chmod g+x /opt/bin/wrap_chrome_binary \
  && /opt/bin/wrap_chrome_binary

#============================================
# Chrome webdriver
#============================================
ADD https://chromedriver.storage.googleapis.com/${CHROMEDRIVER_VERSION}/chromedriver_linux64.zip chromedriver_linux64.zip
RUN  rm -rf /opt/selenium/chromedriver \
  && unzip chromedriver_linux64.zip -d /opt/selenium \
  && rm chromedriver_linux64.zip \
  && chmod g+x /opt/selenium/chromedriver \
  && ln -fs /opt/selenium/chromedriver /usr/bin/chromedriver

COPY generate_config /opt/bin/generate_config
RUN chmod g+x /opt/bin/generate_config

# Generating a default config during build time
RUN /opt/bin/generate_config > /opt/selenium/config.json \
  && chmod 777 /opt/selenium/config.json

CMD ["/opt/bin/entry_point.sh"]
