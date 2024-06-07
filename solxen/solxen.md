# solXEN Mining User Guide (Rust/Nodejs) 2024.06.07

Document maintained by [xen_artist](https://twitter.com/xen_artist)



# Install From Binaries



Download the package for your OS. Extract and run.

### https://github.com/FairCrypto/sol-xen/releases/latest



## Windows
```shell
# Download
https://github.com/FairCrypto/sol-xen/releases/latest/download/sol-xen-windows-x86_64.zip

# Extract
Unzip the sol-xen-windows-x86_64.zip file

# Run the miner
.\sol-xen-windows-x86_64\sol-xen-multiminer.exe --help
```



## MacOS

```shell
# Download
wget https://github.com/faircrypto/sol-xen/releases/latest/download/sol-xen-macos-universal.tar.gz

# Extract
tar xf sol-xen-macos-universal.tar.gz

# Run the miner
./sol-xen-macos-universal/sol-xen-multiminer --help
```



## Linux (x86_64)

```shell
# Download
wget https://github.com/faircrypto/sol-xen/releases/latest/download/sol-xen-linux-x86_64.tar.gz

# Extract
tar xf sol-xen-linux-x86_64.tar.gz

# Run the miner
./sol-xen-linux-x86_64/sol-xen-multiminer --help
```



## Linux (arm64)

```shell
# Download
wget https://github.com/faircrypto/sol-xen/releases/latest/download/sol-xen-linux-arm64.tar.gz

# Extract
tar xf sol-xen-linux-arm64.tar.gz

# Run the miner
./sol-xen-linux-arm64/sol-xen-multiminer --help
```



# Install From Source



## 1. Download Solana Wallet



### Mac & Linux

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

**Please use WSL (Windows Subsystem for Linux) on Windows 10 & 11 to execute all the Linux based instructions provided.**






## 2. Create 4 new wallets

* Using command solana-keygen to generate a new wallet (**Note**: please add **--derivation-path** and **--no-passphrase** as the parameter).

```
solana-keygen new --derivation-path --no-passphrase -o ~/.config/solana/id0.json
```

* Then it will generate a 12-word seed (aka. mnemonic, or recovery) phrase (eg. *leaf jealous olympic later mistake slim oven depth under near very frown*), save it at a **SAFE** place..

```
Wrote new keypair to id0.json
================================================================================
pubkey: 4tf7QSWxYFzmvicRimtJwCtuWfnPq43ZQxjkooCKKUJf
================================================================================
Save this seed phrase and your BIP39 passphrase to recover your new keypair:
leaf jealous olympic later mistake slim oven depth under near very frown
================================================================================
```

* Use the same command to generate id1.json, id2.json, and id3.json

```
solana-keygen new --derivation-path --no-passphrase -o ~/.config/solana/id1.json
```
```
solana-keygen new --derivation-path --no-passphrase -o ~/.config/solana/id2.json
```
```
solana-keygen new --derivation-path --no-passphrase -o ~/.config/solana/id3.json
```




## 3. Recharge mining wallet

### 3.1 Get SOL airdrop for 4 wallets (XOLANA devnet ONLY)

**If you plan to run the sol-xen mining program on the Xolana development network:**

* Config 

```
solana config set -u http://69.10.34.226:8899
```

* Check Public Address of mining wallets

```
solana address -k ~/.config/solana/id0.json # shown <PUBKEY_OF_ID0>

solana address -k ~/.config/solana/id1.json # shown <PUBKEY_OF_ID1>

solana address -k ~/.config/solana/id2.json # shown <PUBKEY_OF_ID2>

solana address -k ~/.config/solana/id3.json # shown <PUBKEY_OF_ID3>
```

* Do airdrop

```
solana airdrop 100 <PUBKEY_OF_ID0>
```
```
solana airdrop 100 <PUBKEY_OF_ID1>
```
```
solana airdrop 100 <PUBKEY_OF_ID2>
```
```
solana airdrop 100 <PUBKEY_OF_ID3>
```

* Check balance

```
solana balance <PUBKEY_OF_ID0>

solana balance <PUBKEY_OF_ID1>

solana balance <PUBKEY_OF_ID2>

solana balance <PUBKEY_OF_ID3>
```



### 3.2 Fund SOL to mining wallets (Solana mainnet-beta ONLY)

**If you plan to run the sol-xen mining program on the Solana mainnet-beta network:**

* Config 

```
solana config set -u https://api.mainnet-beta.solana.com
```

* Check Public Address of mining wallets

```
solana address -k ~/.config/solana/id0.json # shown <PUBKEY_OF_ID0>

solana address -k ~/.config/solana/id1.json # shown <PUBKEY_OF_ID1>

solana address -k ~/.config/solana/id2.json # shown <PUBKEY_OF_ID2>

solana address -k ~/.config/solana/id3.json # shown <PUBKEY_OF_ID3>
```

* Please fund SOL to the mining wallets, such as <PUBKEY_OF_ID0>, <PUBKEY_OF_ID1>, <PUBKEY_OF_ID2>, <PUBKEY_OF_ID3>.

* Check balance

```
solana balance <PUBKEY_OF_ID0>

solana balance <PUBKEY_OF_ID1>

solana balance <PUBKEY_OF_ID2>

solana balance <PUBKEY_OF_ID3>
```



## 4. Install Rust/Nodejs



Just choose one way to run the mining client, Rust or Nodejs. 

**No need to install both of them.**



### 4.1 Install rustc, cargo (if you run rust mining client)

* Install build-essential:

```bash
sudo apt update
sudo apt install build-essential
```

* Install rust and cargo:

```bash
curl https://sh.rustup.rs -sSf | sh
source $HOME/.cargo/env
```

* Using the latest stable rust version by running:

```bash
rustup update
```



### 4.2 Install nodejs (if you run nodejs mining client)

* Install build-essential:

```bash
sudo apt update
sudo apt install build-essential
```

* Install nvm

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```
or 
```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

* Running either of the above commands downloads a script and runs it. The script clones the nvm repository to ~/.nvm, and attempts to add the source lines from the snippet below to the correct profile file (~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc).

```
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

* To verify that nvm has been installed, do:

```
command -v nvm
```
which should output nvm if the installation was successful. Please note that which nvm will not work, since nvm is a sourced shell function, not an executable binary.

Note: On Linux, after running the install script, if you get nvm: command not found or see no feedback from your terminal after you type command -v nvm, simply close your current terminal, open a new terminal, and try verifying again.

* Install nodejs v22.2.0

```
nvm install 22.2.0
```

* Check nodejs version

```
node -v
```

Output as following:

```
v22.2.0
```





## 5. Get solXEN Miner code 

### 5.1 For XOLANA devnet (epsilon branch)

```
git clone https://github.com/FairCrypto/sol-xen.git
cd sol-xen
git checkout epsilon
git pull
```

### 5.2 For Solana mainnet-beta (master branch)

```
git clone https://github.com/FairCrypto/sol-xen.git
cd sol-xen
git checkout master
git pull
```




## 6. Config .env file



### 6.1 Add/Edit the .env file

* Add/Edit .env

```
nano .env
```
or 

```
vim .env
```


### 6.2.1 For XOLANA devnet

* Config it as following:

```
USER_WALLET_PATH=/home/ubuntu/.config/solana/
ANCHOR_PROVIDER_URL=http://69.10.34.226:8899
PROGRAM_ID_MINTER=8HTvrqZT1JP279DMLT5SfNfGHxUeznem4Bh7zy92sWWx
DEBUG=*
```

### 6.2.2 For Solana mainnet-beta

* Config it as following:

** make sure you have the right user wallet path (where you keypairs are) **

```
USER_WALLET_PATH=/home/ubuntu/.config/solana/
ANCHOR_PROVIDER_URL=https://api.mainnet-beta.solana.com # or any other mainnet-beta rpc
```



## 7. Run miners 



### 7.1 Nodejs miner - 4-in-1 box

* Install dependencies first

```
npm install
```


**Please remember to replace the <ETH ADDRESS> to your ETH format address for further receiving XN airdrop purposes. (Self-Custody Crypto Wallet)**

* Run mint command without auto mint

```
# adjust the fee or delay if necessary

node ./client/multiminer.js mine --address <ETH ADDRESS> --fee 1 --delay 1 --units 1150000 
```

* Run mint command with auto mint enabled (Auto mint every N [default: 1000] slots )

```
# adjust the fee or delay if necessary

node ./client/multiminer.js mine --address <ETH ADDRESS> --fee 1 --delay 1 --units 1150000 --autoMint 1000 
```



### 7.2 Rust miner - Run 4 miners one by one 

**Please remember to replace the <ETH ADDRESS> to your ETH format address for further receiving XN airdrop purposes. (Self-Custody Crypto Wallet)**

* Open a new terminal or session. Miner 0:

```
# adjust the fee or delay if necessary

cargo run --package sol-xen-client -- --address <ETH ADDRESS> --command mine --kind 0 --fee 1 --delay 1 --units 1150000 --runs 65535 
```

* Open a new terminal or session. Miner 1:

```
# adjust the fee or delay if necessary

cargo run --package sol-xen-client -- --address <ETH ADDRESS> --command mine --kind 1 --fee 1 --delay 1 --units 1150000 --runs 65535
```

* Open a new terminal or session. Miner 2:

```
# adjust the fee or delay if necessary

cargo run --package sol-xen-client -- --address <ETH ADDRESS> --command mine --kind 2 --fee 1 --delay 1 --units 1150000 --runs 65535
```

* Open a new terminal or session. Miner 3:

```
# adjust the fee or delay if necessary

cargo run --package sol-xen-client -- --address <ETH ADDRESS> --command mine --kind 3 --fee 1 --delay 1 --units 1150000 --runs 65535
```





## 8. Mint Token (solXEN)



### 8.1 Nodejs client Mint Token


* Miner 0:
```
# change the path if necessary

export USER_WALLET=/home/ubuntu/.config/solana/id0.json 

# adjust the fee if necessary

node client/minter.js mint --kind 0 --fee 1 
```

* Miner 1:
```
# change the path if necessary

export USER_WALLET=/home/ubuntu/.config/solana/id1.json 

# adjust the fee if necessary

node client/minter.js mint --kind 1 --fee 1 
```

* Miner 2:
```
# change the path if necessary

export USER_WALLET=/home/ubuntu/.config/solana/id2.json 

# adjust the fee if necessary

node client/minter.js mint --kind 2 --fee 1 
```

* Miner 3:
```
# change the path if necessary

export USER_WALLET=/home/ubuntu/.config/solana/id3.json 

# adjust the fee if necessary

node client/minter.js mint --kind 3 --fee 1 
```



### 8.2 Rust client Mint Token 

**Please remember to replace the example <ETH ADDRESS> to your ETH format address for further receiving XN airdrop purposes. (Self-Custody Crypto Wallet)**

* Miner 0:
```
# change the path if necessary

export USER_WALLET=/home/ubuntu/.config/solana/id0.json 

# adjust the fee if necessary

cargo run --package sol-xen-client -- --address <ETH ADDRESS> --command mint --kind 0 --fee 1 
```

* Miner 1:
```
# change the path if necessary

export USER_WALLET=/home/ubuntu/.config/solana/id1.json 

# adjust the fee if necessary

cargo run --package sol-xen-client -- --address <ETH ADDRESS> --command mint --kind 1 --fee 1 
```

* Miner 2:
```
# change the path if necessary

export USER_WALLET=/home/ubuntu/.config/solana/id2.json 

# adjust the fee if necessary

cargo run --package sol-xen-client -- --address <ETH ADDRESS> --command mint --kind 2 --fee 1 
```

* Miner 3:
```
# change the path if necessary

export USER_WALLET=/home/ubuntu/.config/solana/id3.json 

# adjust the fee if necessary

cargo run --package sol-xen-client -- --address <ETH ADDRESS> --command mint --kind 3 --fee 1 
```





## 9. Check minted Token Balance

* Miner 0:
```
solana config set --keypair ~/.config/solana/id0.json

spl-token accounts
```

* Miner 1:
```
solana config set --keypair ~/.config/solana/id1.json

spl-token accounts
```

* Miner 2:
```
solana config set --keypair ~/.config/solana/id2.json

spl-token accounts
```

* Miner 3:
```
solana config set --keypair ~/.config/solana/id3.json

spl-token accounts
```