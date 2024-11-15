# Nillion Verifier Node

You need to have a VPS with
* 2Core / 4Ram / 50GBSSD

## Docker
```
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

docker --version
```

# Install Verifier
### Pull Verifier's image from Docker
```
docker pull nillion/verifier:v1.0.1
```

### Create a Directory 
```
mkdir -p nillion/verifier
```

### Initialize Verifier
```
docker run -v ./nillion/verifier:/var/tmp nillion/verifier:v1.0.1 initialise
```
This outputs registration details. Copy Them.

İf you lose it, you can retrieve with ```cat ~/nillion/verifier/credentials.json```

### Faucet
> faucet for your "*own*" and "*new(Copied)*" [keplr](https://chromewebstore.google.com/detail/keplr/dmkamcknogkgcdfhhbddcghachkejeap) nillion address [faucet](https://faucet.testnet.nillion.com/) 

## Nillion Dashboard
> Go to Dashboard > https://verifier.nillion.com
> Select "Verifier" then choose "Linux", navigate to step 5 and fill in the ```Verifier Account ID```and ```Verifier Public Key``` with your node credentials.

If you did everything correctly, you will see the following image. 
<img width="877" alt="Screenshot 2024-11-15 at 19 05 51" src="https://github.com/user-attachments/assets/df9338d0-06f8-4228-8c79-e002b2482a0d">

### Open a Screen and Run
```
screen -S nillion

docker run -v ./nillion/verifier:/var/tmp nillion/verifier:v1.0.1 verify --rpc-endpoint "https://testnet-nillion-rpc.lavenderfive.com"
```
<img width="1467" alt="Screenshot 2024-11-15 at 19 09 57" src="https://github.com/user-attachments/assets/74334453-0460-4dce-8227-59915da14cb7">

You can exit the screen with this command: ```Ctrl + A + D``` If you want to re-enter use: ```screen -r nillion```

## Backup
Backup the file located in the nillion/verifier/credentials.json directory to your computer using SFTP.

## Optional
You can increase your Verifier staking impact by staking 0.05 $ETH on Dashboard but it's not mandatory.

