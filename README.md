## SAP NetWeaver AS ABAP 7.51 SP02 Developer Edition

### I. Preparations

#### 1. Clone Git Repository
    Clone this git repository: SAPNetWeaverDevEnv

#### 2. Download SAP NetWeaver
    + Download the SAP NetWeaver

    + unpack the downloaded RAR files
    + copy the unpacked files/folders into the following directory:docker.sap.netweaver/7.51.SP02.opensuse.man/source

### II. Docker

#### 1. Build Docker Image
```bash
sudo docker build -t sapnw:7.51 .
```

#### 2. Run Docker Image
```bash
sudo docker run -P -h vhcalnplci --rm --name sapnw751 -it sapnw:7.51 /bin/bash
```

### III. Install SAP NetWeaver
#### 1. Start installation
```
vhcalnplci:/tmp/sapnw # ./install.sh
```

#### 2. During the installation
    + agree the license terms > yes
    + enter/re-enter a password
    + installation process... take a while...
    + installation success message: "Installation of NPL successful"

### IV. Start/Stop SAP NetWeaver

#### 1. Start

#### 2. Stop

### V. Setup SAP Netweaver

#### 1. License

#### 2.
