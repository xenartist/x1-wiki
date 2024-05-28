
# solXEN Mining User Guide (Go) 2024.05.28

Document maintained by [xen_artist](https://twitter.com/xen_artist)



## 1. Download Solana Wallet

### Mac & Linux

### 1.1 Download solana wallet

* Open your favorite Terminal application
* Install the Solana release [v1.18.12](https://github.com/solana-labs/solana/releases/tag/v1.18.12) on your machine by running:

  ```
  sh -c "$(curl -sSfL https://release.solana.com/v1.18.12/install)"
  ```

* The following output indicates a successful update:

  ```
  downloading v1.18.12 installer
  Configuration: /home/solana/.config/solana/install/config.yml
  Active release directory: /home/solana/.local/share/solana/install/active_release
  * Release version: v1.18.12
  * Release URL: https://github.com/solana-labs/solana/releases/download/v1.18.12/solana-release-x86_64-unknown-linux-gnu.tar.bz2
  Update successful
  ```

* Depending on your system, the end of the installer messaging may prompt you to

  ```
  Please update your PATH environment variable to include the solana programs:
  ```

* If you get the above message, copy and paste the recommended command below it to update `PATH` 

  You can do this by adding the following line to your $HOME/.profile or /etc/profile (for a system-wide installation):

  ```
  export PATH="/home/ubuntu/.local/share/solana/install/active_release/bin:$PATH"
  ```

**Note:** Changes made to a profile file may not apply until the next time you log into your computer. To apply the changes immediately, just run the shell commands directly or execute them from the profile using a command such as `source $HOME/.profile`.

* Confirm you have the desired version of `solana` installed by running:

  ```
  solana --version
  ```

* After a successful install, `solana-install update` may be used to easily update the Solana software to a newer version at any time.

  

### Windows

### 1.2 Download solana wallet

* Open a Command Prompt (`cmd.exe`) as an Administrator
* Search for Command Prompt in the Windows search bar. When the Command Prompt app appears, right-click and select “Open as Administrator”. If you are prompted by a pop-up window asking “Do you want to allow this app to make changes to your device?”, click Yes.
* Copy and paste the following command, then press Enter to download the Solana installer into a temporary directory:

  ```
  cmd /c "curl https://release.solana.com/v1.18.12/solana-install-init-x86_64-pc-windows-msvc.exe --output C:\solana-install-tmp\solana-install-init.exe --create-dirs"
  ```

* Copy and paste the following command, then press Enter to install the latest version of Solana. If you see a security pop-up by your system, please select to allow the program to run.

  ```
  C:\solana-install-tmp\solana-install-init.exe v1.18.12
  ```

* When the installer is finished, press Enter.
* Close the command prompt window and re-open a new command prompt window as a normal user
* Search for "Command Prompt" in the search bar, then left click on the Command Prompt app icon, no need to run as Administrator)
* Confirm you have the desired version of `solana` installed by entering:

  ```
  solana --version
  ```

* After a successful install, `solana-install update` may be used to easily update the Solana software to a newer version at any time.

  

## 2. Create a new wallet

* Using command solana-keygen to generate a new wallet (**Note**: please add **--derivation-path** as the parameter).

```
solana-keygen new --derivation-path --no-passphrase
```

* Then it will generate a 12-word seed (aka. mnemonic, or recovery) phrase (eg. *leaf jealous olympic later mistake slim oven depth under near very frown*), save it at a **SAFE** place as it will be used as **Mnemonic** in solxen-tx.yaml.

```
Wrote new keypair to id.json
================================================================================
pubkey: 4tf7QSWxYFzmvicRimtJwCtuWfnPq43ZQxjkooCKKUJf
================================================================================
Save this seed phrase and your BIP39 passphrase to recover your new keypair:
leaf jealous olympic later mistake slim oven depth under near very frown
================================================================================
```

* The generated pubkey above (eg. *4tf7QSWxYFzmvicRimtJwCtuWfnPq43ZQxjkooCKKUJf*) is the public master wallet address (usually the 1st. one) will be used to recharge SOL for running solxen-tx.



## 3. Download the latest version of the solxen-tx mining client (Go language version) 

* Download link: https://github.com/mmc-98/solxen-tx/releases
* Windows version: solxen-tx-windows-amd64.zip
* macOS version (Intel CPU): solxen-tx-darwin-amd64.tar.gz
* macOS version (M1/M2/M3 CPU): solxen-tx-darwin-arm64.tar.gz
* Linux version (Intel/AMD CPU): solxen-tx-linux-amd64.tar.gz
* Linux version (ARM embedded CPU): solxen-tx-linux-arm64.tar.gz



## 4. Configuration file solxen-tx.yaml 

* After extracting the downloaded zip file, you will see two files: one is the solxen-tx binary executable file, and the other is the solxen-tx.yaml configuration file.

* Detailed explanation of the xolana network (xolana) configuration file:

```   
Name: solxen-tx 
Sol: 
    HdPAth: m/44'/501'/0'/0'                                 # Wallet address path (default) 
    Url: "http://69.10.34.226:8899"                     # RPC address (replaceable) 
    Mnemonic: "leaf jealous olympic later mistake slim oven depth under near very frown" # Mnemonic (replace with your own mnemonic) 
    Num: 1                                                   # Concurrency (number of concurrent wallets, recommend 4) 
    Fee: 3000                                                # Priority fee (in microLamports) 
    ToAddr: "<ETH_ADDRESS>"     # ETH-formatted address to receive xn airdrops (uppercase & lowercase; replace with your own wallet address) 
    ProgramID: "Contract address on the development network" # solxen contract address 
    Time: 1000                                               # Interval time (in milliseconds) 
    
```

* Main network (mainnet) configuration file detailed explanation:

```   
Name: solxen-tx 
Sol: 
    HdPAth: m/44'/501'/0'/0'                                 # Wallet address path (default)
    Url: "https://api.mainnet-beta.solana.com"               # RPC address (replaceable) 
    Mnemonic: "leaf jealous olympic later mistake slim oven depth under near very frown" # Mnemonic (replace with your own mnemonic) 
    Num: 1                                                   # Concurrency (number of concurrent wallets, recommend 4) 
    Fee: 3000                                                # Priority fee (in microLamports) 
    ToAddr: "<ETH_ADDRESS>"     # ETH-formatted address to receive xn airdrops (uppercase & lowercase; replace with your own wallet address) 
    ProgramID: "7A5q3Cw4oN5w1UXfsRTJbxGDXmVhXL2PLhL1Hp7gGCmj" # solxen contract address 
    Time: 1000                                               # Interval time (in milliseconds) 
    
```



## 5. Check mining wallet balance (MUST)

Do this before any mining operation, to get the mining wallet public addresses, SOL balance, etc.

```
./solxen-tx balance
```



## 6. Get SOL airdrop on XOLANA network (Optional)

```
./solxen-tx airdrop
```



## 7. solXEN Mining 

* In **Step 5. Check mining wallet balance (MUST)**, the wallet address being used will be displayed, either one or more (depending on whether the Num value in the configuration file is 1 or >1, recommend 4). Verify the wallet addresses are the correct ones as expected.

* Fund SOL to the mining wallet address:
	* If it is the **XOLANA devnet** network, you can follow **Step 6** to receive the XOLANA network's test SOL token airdrop;
	* If it is the **mainnet-beta** network, you can deposit SOL to the mining wallet address (one or more mining wallet addresses). 

* After successful recharge, restart the program to officially start mining.

```
./solxen-tx miner
```

* Check personal mining information on the solXEN mining leaderboard: https://solxen.io/leaderboard



## 8. Use mined point to mint solXEN token

```
./solxen-tx minter
```



## 9. Other Reference Information 

* solXEN Mining Whitepaper: https://docs.solxen.io/
* solXEN Mining Leaderboard: https://solxen.io/leaderboard
* solXEN Mining English Telegram: https://t.me/+Z5kEez70pyQ5NTAz
* X1/XEN ecosystem wikipedia: [https://x1.wiki](https://x1.wiki/)
