FROM ubuntu:latest

RUN apt-get update && apt-get install -y firefox

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
CMD /usr/bin/firefox


# This is based on http://fabiorehm.com/blog/2014/09/11/running-gui-apps-with-docker/
# running GUI app inside of docker.  Trick is to 
# 1. Install X11Quartz for X11 support on MacOS.  Start X11Quartz native OS app
# 2. Run in terminal : socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"
# 3. Run in another terminal : docker run -ti --rm  -e DISPLAY=$(ipconfig getifaddr en0):0 \
#                                -v /tmp/.X11-unix:/tmp/.X11-unix  firefox

# apt-get install default-jdk 
