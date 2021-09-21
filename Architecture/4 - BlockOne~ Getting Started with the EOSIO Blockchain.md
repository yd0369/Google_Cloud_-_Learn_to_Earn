
# Block.one: Getting Started with the EOSIO Blockchain


```
my-vm-1
```


```
gcloud beta compute instances create my-vm-1 --zone=us-central1-a --machine-type=n1-standard-2 --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --image=ubuntu-1804-bionic-v20210825 --image-project=ubuntu-os-cloud --boot-disk-size=10GB --boot-disk-type=pd-balanced --boot-disk-device-name=my-vm-1 --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any

```

- [ ] SSH Add ProID fter projects/***/
    ```
    https://ssh.cloud.google.com/projects//zones/us-central1-a/instances/my-vm-1
    ```





```
wget https://github.com/EOSIO/eos/releases/download/v2.0.9/eosio_2.0.9-1-ubuntu-18.04_amd64.deb
wget https://github.com/eosio/eosio.cdt/releases/download/v1.7.0/eosio.cdt_1.7.0-1-ubuntu-18.04_amd64.deb
sudo apt install ./eosio_2.0.9-1-ubuntu-18.04_amd64.deb -y
sudo apt install ./eosio.cdt_1.7.0-1-ubuntu-18.04_amd64.deb -y


nodeos -e -p eosio --plugin eosio::chain_api_plugin --plugin eosio::history_api_plugin --contracts-console >> nodeos.log 2>&1 &

cleos wallet create --name my_wallet --file my_wallet_password

export wallet_password=$(cat my_wallet_password)

cleos wallet open --name my_wallet

cleos wallet unlock --name my_wallet --password $wallet_password

cleos wallet import --name my_wallet --private-key 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3


cleos wallet open --name my_wallet

export wallet_password=$(cat my_wallet_password)

cleos wallet unlock --name my_wallet --password $wallet_password

cleos create key --file my_keypair1

cat my_keypair1

cleos wallet import --name my_wallet --private-key 


```

- Enter the public key after command
```
cleos create account eosio bob 
```













---
---



---
---
---

# Overall Checks : 6




- [ ] Create a virtual machine using the Google Cloud Console
- [ ] Install the EOSIO platform
- [ ] Run a local single node blockchain
- [ ] Create wallet
- [ ] Add the eosio system account private key to the new wallet
- [ ] Install the EOSIO Contract Development Toolkit (CDT)