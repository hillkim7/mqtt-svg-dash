This repository is revised version from Jan-Piet Men's [mqtt-svg-dash][1].  
Original project uses three S/W components:
MQTT broker + nodejs websocket + HTML5 code

Up-to-date version of mosquitto MQTT broker supports websockets natively.
The nodejs websocket is no longer needed for the demo.
Here it uses native websockets to connect to MQTT broker using a Paho.MQTT client JavaScript library.

First to use the mosquitto with websockets support I need to have recent mosquitto program,
So I deleted old mosquitto package from my Ubuntu 14.04.1 LTS server.
```
sudo apt-get remove mosquitto
sudo apt-get remove libmosquitto1
```

Second, download the newest mosquitto source code and compile it with "WITH_WEBSOCKETS:=yes".
```
wget http://mosquitto.org/files/source/mosquitto-1.4.2.tar.gz
sudo apt-get install uuid-dev libwebsockets-dev	# install mosquitto required packages
cd mosquitto-1.4.2
make WITH_WEBSOCKETS:=yes
sudo make install
```

Setting websocket bind address and port number through configuration file.
```
 # mosquitto conf 
listener 9001 0.0.0.0
protocol websockets
bind_address 0.0.0.0
port 1883
```

Run mosquitto broker and start MQTT publishing.
```
/usr/local/sbin/mosquitto -d -c mosquitto.conf
python randpub.py
```

Open corp.html file with web browser.

[1]: https://github.com/jpmens/mqtt-svg-dash
