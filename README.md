# Install Netbox on Docker 

## Step 1 Setup Netbox
```bash
git clone https://github.com/mhdhaidarah/NetBox-Docker.git
cd NetBox-Docker
docker compose pull
```
## Step 2 Create Super User for Web GUI
```bash
docker compose exec netbox /opt/netbox/netbox/manage.py createsuperuser
```

## Step 3 Test and Browse
```bash
http://<Server-IP>:8000
```
## To make it start after reboot
```bash
docker update --restart=always netbox-docker-netbox-1
docker update --restart=always netbox-docker-netbox-worker-1
docker update --restart=always netbox-docker-postgres-1
docker update --restart=always netbox-docker-redis-1
docker update --restart=always netbox-docker-redis-cache-1
```

# Optional
## Import Devices Library
```bash
sudo apt update && sudo apt install -y python3 python3-pip python3-venv python3-dev build-essential libssl-dev libffi-dev libsqlite3-dev wget curl git
git clone https://github.com/netbox-community/Device-Type-Library-Import.git
cd Device-Type-Library-Import
python3 -m venv venv
source venv/bin/activate

pip install -r requirements.txt
cp .env.example .env
```

## Now Setup URL to the NetBox Server & Token the token can be generated from GUI Users and select V1
## EXAMPLE
```bash
NETBOX_URL=https://192.168.0.100:8000
NETBOX_TOKEN=LE0GCreKBP0v3jbXauWLVqbmzKtH3BnhI1Z184TV
REPO_URL=https://github.com/netbox-community/devicetype-library.git
REPO_BRANCH=master
IGNORE_SSL_ERRORS=True
#REQUESTS_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt # you should enable this if you are running on a linux sys>
#SLUGS=c9300-48u isr4431 isr4331
```
## Update Here
```bash
sudo nano .env
```
## Install Device Library Importer
```bash
git clone https://github.com/netbox-community/devicetype-library.git ~/Device-Type-Library-Import/repo
```

## Select Vendors or download all
```bash
./nb-dt-import.py
```
## OR
```bash
./nb-dt-import.py --vendors mikrotik,ubiquiti
```




