# OpenDroneID receiver and spoofer

## Installation
```bash
./setup.sh
```

## Run

### 1. Bluetooth receiver (using Sonoff Dongle)
1. Get sniffle from [here](https://github.com/bkerler/sniffle) and install
2. Run 
```bash
./sniff_receiver.py -b 2000000 -z --zmqsetting 127.0.0.1:4222 -l -e -s /dev/ttyUSB1
```
```
Argument description:
---------------------
-b is Baudrate (only use 2000000 for newer Sonoff devices, otherwise leave away)
-s is the serial port of the bluetooth dongle
-e we want extended advertising packets
-l we want longrange packets
-z spawn a zmq server
--zmqsetting zmq server addr is 127.0.0.1 with Port 4222
```

### 2. Wifi receiver (using Wifi card in monitoring mode)
#### For pcap replay
```
./wifi_receiver.py --pcap examples/odid_wifi_sample.pcap -z --zmqsetting 127.0.0.1:4223
```

#### Using a wifi interface
```
./wifi_receiver.py --interface wlan0 -z --zmqsetting 127.0.0.1:4223
```

### 3. Decode and spawn zmq server
```bash
./zmq_decoder.py -z --zmqsetting 127.0.0.1:4224 --zmqclients 127.0.0.1:4222,127.0.0.1:4223
```
```
Argument description:
---------------------
-z spawn a zmq server
--zmqsetting zmq server addr is 127.0.0.1 with Port 4224
--zmqclients listen to bluetooth receiver at 127.0.0.1:4222 and wifi receiver at 127.0.0.1:4223
```