
# solXEN Mining User Guide (Go) 2024.05.12

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
solana-keygen new --derivation-path
```

* It will prompt following information, press ENTER to continue.

```
Generating a new keypair

For added security, enter a BIP39 passphrase

NOTE! This passphrase improves security of the recovery seed phrase NOT the
keypair file itself, which is stored as insecure plain text

BIP39 Passphrase (empty for none): 
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



## 3. Get SOL airdrop for devnet (Optional)

* https://faucet.solana.com/
* https://faucet.quicknode.com/solana/
* https://solfaucet.com/



## 4. Download the latest version of the solxen-tx mining client (Go language version) 

* Download link: https://github.com/mmc-98/solxen-tx/releases
* Windows version: solxen-tx-windows-amd64.zip
* macOS version (Intel CPU): solxen-tx-darwin-amd64.tar.gz
* macOS version (M1/M2/M3 CPU): solxen-tx-darwin-arm64.tar.gz
* Linux version (Intel/AMD CPU): solxen-tx-linux-amd64.tar.gz
* Linux version (ARM embedded CPU): solxen-tx-linux-arm64.tar.gz



## 5. Configuration file solxen-tx.yaml 

* After extracting the downloaded zip file, you will see two files: one is the solxen-tx binary executable file, and the other is the solxen-tx.yaml configuration file.

* Detailed explanation of the development network (devnet) configuration file:

```   
Name: solxen-tx 
Sol: 
    Url: "https://api.devnet.solana.com"                     # RPC address (replaceable) 
    Mnemonic: "leaf jealous olympic later mistake slim oven depth under near very frown" # Mnemonic (replace with your own mnemonic) 
    Num: 1                                                   # Concurrency (number of concurrent wallets) 
    Fee: 3000                                                # Priority fee (in microLamports) 
    ToAddr: "0xrjo23jro342r3ur90ewi0vjq3jr3o4i3por3k4r3"     # ETH-formatted address to receive xn airdrops (replace with your own wallet address) 
    ProgramID: "Contract address on the development network" # solxen contract address 
    Time: 1000                                               # Interval time (in milliseconds) 
    HdPAth: m/44'/501'/0'/0'                                 # Wallet address path (default) 
```

* Main network (mainnet) configuration file detailed explanation:

```   
Name: solxen-tx 
Sol: 
    Url: "https://api.mainnet-beta.solana.com"               # RPC address (replaceable) 
    Mnemonic: "leaf jealous olympic later mistake slim oven depth under near very frown" # Mnemonic (replace with your own mnemonic) 
    Num: 1                                                   # Concurrency (number of concurrent wallets) 
    Fee: 3000                                                # Priority fee (in microLamports) 
    ToAddr: "0xrjo23jro342r3ur90ewi0vjq3jr3o4i3por3k4r3"     # ETH-formatted address to receive xn airdrops (replace with your own wallet address) 
    ProgramID: "Contract address on the main network"        # solxen contract address 
    Time: 1000                                               # Interval time (in milliseconds) 
    HdPAth: m/44'/501'/0'/0'                                 # Wallet address path (default)
```



## 6. solXEN Mining 
* After setting up the configuration file, run the solxen-tx binary executable file to start the program and initialize mining.

* At the beginning of the log, the wallet address being used will be displayed, either one or more (depending on whether the Num value in the configuration file is 1 or >1). Verify the wallet address is the correct one as expected.

* Stop the program, recharge SOL to the mining wallet address.

* After successful recharge, restart the program to officially start mining.

* Check personal mining information on the solXEN mining leaderboard: https://solxen.io/leaderboard



## 7. Other Reference Information 

* solXEN Mining Whitepaper: https://docs.solxen.io/
* solXEN Mining Leaderboard: https://solxen.io/leaderboard
* solXEN Mining English Telegram: https://t.me/+Z5kEez70pyQ5NTAz
* X1/XEN ecosystem wikipedia: [https://x1.wiki](https://x1.wiki/)
