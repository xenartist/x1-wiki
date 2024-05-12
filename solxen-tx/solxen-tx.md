
# solXEN Mining User Guide 2024.05.11 

Document maintained by [xen_artist](https://twitter.com/xen_artist)

## 1. Install the Phantom web wallet (or any Web3 wallet that supports Solana, such as OKX/SolFlare, etc.) 

* If it's the first time creating an account, a 12-word mnemonic will be generated. Save it, as it will be used in the solxen-tx configuration file.

* If it's not the first time creating an account, export the 12-word mnemonic from the existing account.

* For easy understanding, here is an example of a 12-word mnemonic: leaf jealous olympic later mistake slim oven depth under near very frown 

* Note: The master wallet is generally the first wallet address.

## 2. Download the latest version of the solxen-tx mining client (Go language version) 

* Download link: https://github.com/mmc-98/solxen-tx/releases
* Windows version: solxen-tx-windows-amd64.zip
* macOS version (Intel CPU): solxen-tx-darwin-amd64.tar.gz
* macOS version (M1/M2/M3 CPU): solxen-tx-darwin-arm64.tar.gz
* Linux version (Intel/AMD CPU): solxen-tx-linux-amd64.tar.gz
* Linux version (ARM embedded CPU): solxen-tx-linux-arm64.tar.gz

## 3. Configuration file solxen-tx.yaml 

* After extracting the downloaded zip file, you will see two files: one is the solxen-tx binary executable file, and the other is the solxen-tx.yaml configuration file.

* Detailed explanation of the development network (devnet) configuration file:

```   
Name: solxen-tx 
Sol: 
    Url: "[https://api.devnet.solana.com](https://api.devnet.solana.com/)"               # RPC address (replaceable) 
    Mnemonic: "leaf jealous olympic later mistake slim oven depth under near very frown" # Mnemonic (replace with your own mnemonic) 
    Num: 1                                                                               # Concurrency (number of concurrent wallets) 
    Fee: 3000                                                                            # Priority fee (in microLamports) 
    ToAddr: "0xrjo23jro342r3ur90ewi0vjq3jr3o4i3por3k4r3"                                 # ETH-formatted address to receive xn airdrops (replace with your own wallet address) 
    ProgramID: "Contract address on the development network"                             # solxen contract address 
    Time: 1000                                                                           # Interval time (in milliseconds) 
    HdPAth: m/44'/501'/0'/0'                                                             # Wallet address path (default web3 wallet) 
```

* Main network (mainnet) configuration file detailed explanation:

```   
Name: solxen-tx 
Sol: 
    Url: "[https://api.mainnet-beta.solana.com](https://api.mainnet-beta.solana.com/)"   # RPC address (replaceable) 
    Mnemonic: "leaf jealous olympic later mistake slim oven depth under near very frown" # Mnemonic (replace with your own mnemonic) 
    Num: 1                                                                               # Concurrency (number of concurrent wallets) 
    Fee: 3000                                                                            # Priority fee (in microLamports) 
    ToAddr: "0xrjo23jro342r3ur90ewi0vjq3jr3o4i3por3k4r3"                                 # ETH-formatted address to receive xn airdrops (replace with your own wallet address) 
    ProgramID: "Contract address on the main network"                                    # solxen contract address 
    Time: 1000                                                                           # Interval time (in milliseconds) 
    HdPAth: m/44'/501'/0'/0'                                                             # Wallet address path (default web3 wallet)
```



## 4. solXEN Mining 
* After setting up the configuration file, run the solxen-tx binary executable file to start the program and initialize mining.

* At the beginning of the log, the wallet address being used will be displayed, either one or more (depending on whether the Num value in the configuration file is 1 or >1). Verify the wallet address in the web3 wallet to ensure that the recharged wallet address matches correctly.

* Stop the program, recharge SOL to the mining wallet address.

* After successful recharge, restart the program to officially start mining.

* Check personal mining information on the solXEN mining leaderboard: https://sol-xen-app.infrafc.org/leaderboard

## 5. Other Reference Information 

* solXEN Mining Whitepaper: https://docs.solxen.io/
* solXEN Mining Leaderboard: https://sol-xen-app.infrafc.org/leaderboard
* solXEN Mining English Telegram: https://t.me/+Z5kEez70pyQ5NTAz
* X1/XEN ecosystem wikipedia: [https://x1.wiki](https://x1.wiki/)
