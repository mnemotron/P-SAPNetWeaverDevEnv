## SAP NetWeaver AS ABAP 7.51 SP02 Developer Edition

### Manual Installation

#### 1. Build Docker Image
```bash
docker build -t sapnw751sp02 .
```

#### 2. Run Docker Image
```bash
sudo docker run -i -t sapnw751sp02 /bin/bash
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
sudo docker run -d -t sapnw751sp02
```
