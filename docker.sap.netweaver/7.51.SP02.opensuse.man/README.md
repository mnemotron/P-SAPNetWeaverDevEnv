## SAP NetWeaver 7.51 SP02 AS ABAP Developer Edition

### I. Preparations

#### 1. Clone Git Repository
+ Clone this git repository: SAPNetWeaverDevEnv

#### 2. Download SAP NetWeaver
+ download the SAP NetWeaver: [https://tools.hana.ondemand.com/#abap](https://tools.hana.ondemand.com/#abap "https://tools.hana.ondemand.com/#abap")
+ unpack the downloaded RAR files
+ copy the unpacked files/folders into the following directory: docker.sap.netweaver/7.51.SP02.opensuse.man/source

### II. Docker

#### 1. Workdirectory
```bash
# <SAPNetWeaverDevEnv>: change to your repository directory
cd <SAPNetWeaverDevEnv>/docker.sap.netweaver/7.51.SP02.opensuse.man
```

#### 2. Build Docker Image
```bash
sudo docker build -t sapnw:7.51 .
```

#### 3. Run Docker Image
```bash
# --rm  (parameter automatically remove the container when it exits)
sudo docker run --privileged -p 8000:8000 -p 44300:44300 -p 3300:3300 -p 3200:3200 -p 8443:8443 -h vhcalnplci --name sapnw751 -it sapnw:7.51 /bin/bash
```

### III. Install SAP NetWeaver

#### 1. Start installation
```bash
# start uuid daemon (and wait a second)
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
# start docker container
sudo docker start -i sapnw751
```

```bash
# start uuid daemon (and wait a second)
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

#### 1. User
The following users are available to logon:

User | Password | Description
--- | --- | ---
SAP* | Appl1ance | Administrator
DEVELOPER | Appl1ance | Developer
BWDEVELOPER | Appl1ance | Developer
DDIC | Appl1ance | Data Dictionary

#### 2. Clients

Client | Description
--- | ---
000 | golden reference client for administrative activities
001 | configuration client, can be used for developments

#### 2. License
Currently a developer license is valid for half a year.

For an update, do the following steps:

+ open the SAP GUI and logon with user: **SAP*** and client: **000**
+ open transaction: **SLICENSE**
+ copy the active hardware key
+ open the SAP license page: [https://go.support.sap.com/minisap/#/minisap](https://go.support.sap.com/minisap/#/minisap "https://go.support.sap.com/minisap/#/minisap")
+ choose: **NPL - SAP NetWeaver 7.x (Sybase ASE)**
+ fill out all fields and use the copied active hardware key
+ save the generated license file: **NPL.txt**
+ go back to transaction: **SLICENSE**
+ delete the installed license from the table
+ install the new license and use the downloaded file: **NPL.txt**
