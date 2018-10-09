## SAP NetWeaver AS ABAP 7.51 SP02 Developer Edition

### Manual Installation

#### 1. Build Docker Image
```bash
docker build -t sapnw751sp02 .
```

#### 2. Run Docker Image
```bash
sudo docker run -P --name sapnw751sp02 -i -t sapnw751sp02 /bin/bash
```

#### 3. Install SAP NetWeaver
```bash
bash /tmp/sapnw/install.sh -s -k
```
### Automatic Installation

#### 1. Build Docker Image
```bash
docker build -t sapnw751sp02 .
```

#### 2. Run Docker Image
```bash
sudo docker run -P --name sapnw751sp02 -d -t sapnw751sp02
```
