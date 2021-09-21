
# Block.one: Getting Started with the EOSIO Blockchain


```
my-vm-1
```

- [ ] SSH Add ProID fter projects/***/
    ```
    https://ssh.cloud.google.com/projects//zones/us-central1-a/instances/my-vm-1
    ```



```
wget https://github.com/EOSIO/eos/releases/download/v2.0.9/eosio_2.0.9-1-ubuntu-18.04_amd64.deb

sudo apt install ./eosio_2.0.9-1-ubuntu-18.04_amd64.deb

nodeos -e -p eosio --plugin eosio::chain_api_plugin --plugin eosio::history_api_plugin --contracts-console >> nodeos.log 2>&1 &

cleos wallet create --name my_wallet --file my_wallet_password

cleos wallet open --name my_wallet

cleos wallet unlock --name my_wallet --password YOUR_PASSWORD

cleos wallet import --name my_wallet --private-key 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3

wget https://github.com/eosio/eosio.cdt/releases/download/v1.7.0/eosio.cdt_1.7.0-1-ubuntu-18.04_amd64.deb

sudo apt install ./eosio.cdt_1.7.0-1-ubuntu-18.04_amd64.deb

cleos wallet open --name my_wallet

export wallet_password=$(cat my_wallet_password)

cleos wallet unlock --name my_wallet --password $wallet_password

cleos create key --file my_keypair1

cat my_keypair1


```

- Enter the private key after command
```
cleos wallet import --name my_wallet --private-key 
```

- Enter the public key after command
```
cleos create account eosio bob 
```


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