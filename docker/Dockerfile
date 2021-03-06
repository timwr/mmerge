# To build the dev environment.
# docker build -t meterpreter .

FROM ubuntu:14.04.2
MAINTAINER Brent Cook <bcook@rapid7.com> (@busterbcook)

RUN apt-get update
RUN apt-get dist-upgrade -y

ENV DEBIAN_FRONTEND noninteractive

#RUN echo "debconf shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
#RUN echo "debconf shared/accepted-oracle-license-v1-1 seen true" | debconf-set-selections
#RUN apt-get -y install python-software-properties

# Posix meterpreter requirements
RUN apt-get install -y bison flex gcc gcc-multilib jam make wget

# Java requirements
RUN apt-get install -y maven openjdk-7-jdk

# Android sdk
RUN wget http://dl.google.com/android/android-sdk_r24-linux.tgz
RUN tar xf android-sdk_r24-linux.tgz
RUN rm android-sdk_r24-linux.tgz
RUN mv android-sdk-linux /usr/local/android-sdk
RUN echo y | /usr/local/android-sdk/tools/android update sdk --filter tools --no-ui -a
RUN echo y | /usr/local/android-sdk/tools/android update sdk --filter platform-tools --no-ui -a
RUN echo y | /usr/local/android-sdk/tools/android update sdk --filter android-3 --no-ui -a

RUN wget http://dl.google.com/android/ndk/android-ndk-r9d-linux-x86_64.tar.bz2
RUN tar xf android-ndk-r9d-linux-x86_64.tar.bz2
RUN mv android-ndk-r9d /usr/local/android-ndk
RUN rm android-ndk-r9d-linux-x86_64.tar.bz2

#RUN mvn package -Dandroid.sdk.path=/usr/local/android-sdk -Dandroid.ndk.path=/usr/local/android-ndk -Dandroid.release=true -P deploy

#ADD deps/android-ndk-r10d-linux-x86_64.bin /tmp
#RUN chmod 755 /tmp/android-ndk-r10d-linux-x86_64.bin
#RUN cd /tmp && ./android-ndk-r10d-linux-x86_64.bin
#RUN mv android-ndk-r10d android-ndk /opt && rm android-ndk-r10d-linux-x86_64.bin

RUN apt-get install -y ruby rake bundler git

ENV ANDROID_HOME /usr/local/android-sdk
ENV ANDROID_NDK_HOME /usr/local/android-ndk
ENV PATH $PATH:$ANDROID_HOME/tools
ENV PATH $PATH:$ANDROID_HOME/platform-tools
ENV PATH $PATH:$ANDROID_NDK_HOME

RUN apt-get -y install software-properties-common
RUN dpkg --add-architecture i386
RUN apt-add-repository ppa:ubuntu-wine
RUN apt-get update
RUN apt-get -y install wine php5-cli python python3

RUN apt-get clean

ENV JENKINS_HOME /var/jenkins_home
RUN useradd -d "$JENKINS_HOME" -u 1001 -m -s /bin/sh jenkins
VOLUME "$JENKINS_HOME"
RUN chown -R jenkins "$JENKINS_HOME"
