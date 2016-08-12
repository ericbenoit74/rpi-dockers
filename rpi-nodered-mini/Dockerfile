# DOCKER-VERSION 1.0.0
FROM resin/rpi-raspbian

# install required packages, in one command
RUN apt-get update  && \
    apt-get install -y  python-dev

ENV PYTHON /usr/bin/python2

# install nodejs for rpi
RUN apt-get install -y wget && \
    wget http://node-arm.herokuapp.com/node_latest_armhf.deb && \
    dpkg -i node_latest_armhf.deb && \
    rm node_latest_armhf.deb && \
    apt-get autoremove -y wget

# install node-red
RUN apt-get install -y build-essential && \
    npm install -g --unsafe-perm  node-red && \
    apt-get autoremove -y build-essential

# install RPI.GPIO python libs
RUN apt-get install -y wget && \
     wget 'http://downloads.sourceforge.net/project/raspberry-gpio-python/raspbian-jessie/python-rpi.gpio_0.6.2%7Ejessie-1_armhf.deb?r=https%3A%2F%2Fsourceforge.net%2Fprojects%2Fraspberry-gpio-python%2Ffiles%2Fraspbian-jessie%2F&ts=1470999819&use_mirror=freefr' && \
     mv 'python-rpi.gpio_0.6.2~jessie-1_armhf.deb?r=https%3A%2F%2Fsourceforge.net%2Fprojects%2Fraspberry-gpio-python%2Ffiles%2Fraspbian-jessie%2F&ts=1470999819&use_mirror=freefr' python-rpi.gpio_0.6.2~jessie-1_armhf.deb && \
     dpkg -i python-rpi.gpio_0.6.2~jessie-1_armhf.deb && \
     rm python-rpi.gpio_0.6.2~jessie-1_armhf.deb && \
     apt-get autoremove -y wget

WORKDIR /root/bin
RUN ln -s /usr/bin/python2 ~/bin/python
RUN ln -s /usr/bin/python2-config ~/bin/python-config
env PATH ~/bin:$PATH

# install other nodes
RUN npm install -g \
    node-red-node-mongodb \
    node-red-node-mysql

# expose port 
EXPOSE 1880

ADD settings.js /usr/local/lib/node_modules/node-red/
ADD start.sh /root/

# Set the default command to execute 
# when creating a new container 
CMD ["/root/start.sh"]

