# Tells my docker image is based on below
FROM    docker/whalesay:latest
RUN     apt-get -y update && apt-get install -y fortunes
CMD     /usr/games/fortune -a | cowsay     
