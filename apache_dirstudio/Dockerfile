FROM ubuntu:latest

RUN apt-get update && apt-get install -y wget default-jdk
RUN mkdir -p /opt
RUN wget -qO- http://ftp.wayne.edu/apache/directory/studio/2.0.0.v20161101-M12/ApacheDirectoryStudio-2.0.0.v20161101-M12-linux.gtk.x86_64.tar.gz | tar xvz -C /opt

# Replace 1000 with your user / group id
RUN export uid=501 gid=20 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \ 
    mkdir /etc/sudoers.d && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown ${uid}:${gid} -R /home/developer


USER developer
ENV HOME /home/developer
CMD /opt/ApacheDirectoryStudio/ApacheDirectoryStudio


# This is based on http://fabiorehm.com/blog/2014/09/11/running-gui-apps-with-docker/
# running GUI app inside of docker.  Trick is to 
# 1. Install X11Quartz for X11 support on MacOS.  Start X11Quartz native OS app
# 1.5 Run brew install socat, if socat is not already installed
# 2. Run in terminal : socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"
# 3. Run in another terminal : docker run -ti --rm  -e DISPLAY=$(ipconfig getifaddr en0):0 \
#                                -v /tmp/.X11-unix:/tmp/.X11-unix apachestudio 

# apt-get install default-jdk 
