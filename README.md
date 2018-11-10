## SAP NetWeaver AS ABAP 7.51 SP02 Developer Edition

### I. Preparations

#### 1. Clone Git Repository
+ Clone this git repository: SAPNetWeaverDevEnv

#### 2. Download SAP NetWeaver
+ download the SAP NetWeaver: [https://tools.hana.ondemand.com/#abap](https://tools.hana.ondemand.com/#abap "https://tools.hana.ondemand.com/#abap")
+ unpack the downloaded RAR files
+ copy the unpacked files/folders into the following directory: docker.sap.netweaver/7.51.SP02.opensuse.man/source

### II. Docker

#### 1. Build Docker Image
```bash
sudo docker build -t sapnw:7.51 .
```

#### 2. Run Docker Image
```bash
# --rm  (automatically remove the container when it exits)
sudo docker run -p 8000:8000 -p 44300:44300 -p 3300:3300 -p 3200:3200 -p 8443:8443 -h vhcalnplci --name sapnw751 -it sapnw:7.51 /bin/bash
```

### III. Install SAP NetWeaver
#### 1. Start installation
```bash
# start uuid daemon
/usr/sbin/uuidd

# start installation
vhcalnplci:/tmp/sapnw # ./install.sh
```

#### 2. During the installation
+ agree the license terms > yes
+ enter/re-enter a password
+ installation process... take a while...
+ installation success message: "Installation of NPL successful"

+ remove the installation files:
```bash
vhcalnplci:/ # rm -R /tmp/sapnw
```

### IV. Start/Stop SAP NetWeaver

#### 1. Start
```bash
# start docker
sudo docker start -i sapnw751
```

```bash
# start uuid daemon
/usr/sbin/uuidd

# start SAP NetWeaver
su npladm
startsap ALL
```

#### 2. Stop
```bash
su npladm
stopsap ALL
exit

# exit docker
exit
```

### V. Setup SAP Netweaver

#### 1. License
