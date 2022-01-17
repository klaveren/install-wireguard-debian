# How to Install Wireguard  on Debian 10

## Install Dependecies 
```
sudo apt -y install linux-headers-cloud-amd64 linux-image-amd64 linux-headers-amd64 wireguard
```

# Configure Server Side
## Generating Private and Public Keys
``` 
wg genkey > server_private_key
wg pubkey < server_private_key > server_public_key
wg genkey | tee server_private_key | wg pubkey > server_public_key
```

## Create Server Configuration File (wg0.conf)

```
[Interface]
PrivateKey = <private key of the server (the content of the server_private_key file)>
Address = 10.0.0.1/24
ListenPort = 51820
```

## Move Config Files 
```
$ chmod 600 server_public_key server_private_key wg0.conf
$ sudo mv server_private_key server_public_key wg0.conf /etc/wireguard
```

## Enable Server
```
systemctl enable --now wg-quick@wg0
```












