## SAP NetWeaver AS ABAP 7.51 SP02 Developer Edition

### Manual Installation

#### 1. Build Docker Image
```bash
docker build -t sapnw751 .
```

#### 2. Run Docker Image
```bash
sudo docker run -P --name sapnw751 -i -t sapnw751 /bin/bash
```

#### 3. Install SAP NetWeaver
```bash
bash /tmp/sapnw/install.sh -s -k
```
