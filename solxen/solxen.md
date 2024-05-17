# solXEN Mining User Guide (Rust)

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

## 3. Get SOL airdrop for 4 wallets

* Config 

```
solana config set -u http://69.10.34.226:8899
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


## 4. Install rustc, cargo.

```bash
$ curl https://sh.rustup.rs -sSf | sh
$ source $HOME/.cargo/env
```

Using the latest stable rust version by running:

```bash
$ rustup update
```

## 5. Get solXEN Miner code 

```
git clone https://github.com/FairCrypto/sol-xen.git
cd sol-xen
git checkout epsilon
```

## 6. Config .env file

Copy .env.example to .env

```
cp .env.example .env
```

Config it as following:

```
USER_WALLET=/home/ubuntu/.config/solana/id0.json
ANCHOR_PROVIDER_URL=http://69.10.34.226:8899
PROGRAM_ID=Dx7zjkWZbUStmhjo8BrhbprtQCcMByJgCTEC6TLgkH8n
PROGRAM_ID_MINTER=3JSyo6R489DcXedDYQUY7XbGXsmCz4mQH7sWeK5VE8vA
DEBUG=*
```

## Run 4 miners one by one (Mining hash/superhash/point)

* Open a new terminal or session. Miner 0:

```
export USER_WALLET=/home/ubuntu/.config/solana/id0.json # change the path if necessary

while true; do cargo run --package sol-xen-client -- --address 0x970Ce544847B0E314eA357e609A0C0cA4D9fD823 --command mine --kind 0; sleep 10; done
```

* Open a new terminal or session. Miner 1:

```
export USER_WALLET=/home/ubuntu/.config/solana/id1.json # change the path if necessary

while true; do cargo run --package sol-xen-client -- --address 0x970Ce544847B0E314eA357e609A0C0cA4D9fD823 --command mine --kind 1; sleep 10; done
```

* Open a new terminal or session. Miner 2:

```
export USER_WALLET=/home/ubuntu/.config/solana/id2.json # change the path if necessary

while true; do cargo run --package sol-xen-client -- --address 0x970Ce544847B0E314eA357e609A0C0cA4D9fD823 --command mine --kind 2; sleep 10; done
```

* Open a new terminal or session. Miner 3:

```
export USER_WALLET=/home/ubuntu/.config/solana/id3.json # change the path if necessary

while true; do cargo run --package sol-xen-client -- --address 0x970Ce544847B0E314eA357e609A0C0cA4D9fD823 --command mine --kind 3; sleep 10; done
```

## Mint Token

* Miner 0:
```
export USER_WALLET=/home/ubuntu/.config/solana/id0.json # change the path if necessary

cargo run --package sol-xen-client -- --address 0x970Ce544847B0E314eA357e609A0C0cA4D9fD823 --command mint --kind 0
```

* Miner 1:
```
export USER_WALLET=/home/ubuntu/.config/solana/id1.json # change the path if necessary

cargo run --package sol-xen-client -- --address 0x970Ce544847B0E314eA357e609A0C0cA4D9fD823 --command mint --kind 1
```

* Miner 2:
```
export USER_WALLET=/home/ubuntu/.config/solana/id2.json # change the path if necessary

cargo run --package sol-xen-client -- --address 0x970Ce544847B0E314eA357e609A0C0cA4D9fD823 --command mint --kind 2
```

* Miner 3:
```
export USER_WALLET=/home/ubuntu/.config/solana/id3.json # change the path if necessary

cargo run --package sol-xen-client -- --address 0x970Ce544847B0E314eA357e609A0C0cA4D9fD823 --command mint --kind 3
```

* Check system level token amount

```
spl-token accounts
```