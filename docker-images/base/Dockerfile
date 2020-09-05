FROM registry.access.redhat.com/ubi8/ubi
LABEL authors="Selenium <selenium-developers@googlegroups.com>, Xavier-Alexandre BROCHARD <xavier.alexandre.brochard@gmail.com>"

USER 0

# Prepare install folders
RUN  mkdir -p /opt/selenium \
  && mkdir -p /opt/bin

# Install the OpenJDK Headless Runtime Environment 11
RUN REPO_LIST="ubi-8-baseos,ubi-8-appstream,ubi-8-codeready-builder" && \
    # Define the packages needed
    INSTALL_PKGS="net-tools java-11-openjdk-headless.x86_64" && \
    # Install the packages
    yum install -y --setopt=tsflags=nodocs --disablerepo "*" --enablerepo $REPO_LIST $INSTALL_PKGS && \
    # Verify the packages
    rpm -V $INSTALL_PKGS && \
    # Clean all packages
    yum -y clean all && \
    # Delete all repo files
    rm /etc/yum.repos.d/*.repo && \
    # Delete the cache  
    rm -rf /var/cache/yum && \
    # Issue with .pki dir in ${HOME} dir 
    rm -rf ${HOME}/.pki

# Install Selenium
ADD https://selenium-release.storage.googleapis.com/${SELENIUM_MAJOR}.${SELENIUM_MINOR}/selenium-server-standalone-${SELENIUM_MAJOR}.${SELENIUM_MINOR}.${SELENIUM_REVISION}.jar /opt/selenium/selenium-server-standalone.jar
RUN chmod +x /opt/selenium/selenium-server-standalone.jar