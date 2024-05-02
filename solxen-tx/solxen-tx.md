# solxen-tx User Guide

## SOLANA Devnet

### 1. Download solana wallet

- Open your favorite Terminal application
- Install the Solana release [v1.18.12](https://github.com/solana-labs/solana/releases/tag/v1.18.12) on your machine by running:

```
sh -c "$(curl -sSfL https://release.solana.com/v1.18.12/install)"
```

- The following output indicates a successful update:

```
downloading v1.18.12 installer
Configuration: /home/solana/.config/solana/install/config.yml
Active release directory: /home/solana/.local/share/solana/install/active_release
* Release version: v1.18.12
* Release URL: https://github.com/solana-labs/solana/releases/download/v1.18.12/solana-release-x86_64-unknown-linux-gnu.tar.bz2
Update successful
```

- Depending on your system, the end of the installer messaging may prompt you to

```
Please update your PATH environment variable to include the solana programs:
```

- If you get the above message, copy and paste the recommended command below it to update `PATH` 

You can do this by adding the following line to your $HOME/.profile or /etc/profile (for a system-wide installation):

```
export PATH="/home/ubuntu/.local/share/solana/install/active_release/bin:$PATH"
```

**Note:** Changes made to a profile file may not apply until the next time you log into your computer. To apply the changes immediately, just run the shell commands directly or execute them from the profile using a command such as `source $HOME/.profile`.

- Confirm you have the desired version of `solana` installed by running:

```
solana --version
```

- After a successful install, `solana-install update` may be used to easily update the Solana software to a newer version at any time.



### 2. Get SOL airdrop for testing

* Create a new wallet

```
solana-keygen new
```

* Setup devnet

```
solana config set --url https://api.testnet.solana.com
```

* Get SOL airdrop

```
solana airdrop 1
```

* Check balance

```
solana balance
```



## 3. Get private key for testing

* Get private key from id.json

```
cat ~/.config/solana/id.json
```

* Some strings like this:

```
[125,204,125,4,46,223,194,107,117,50,42,73,200,176,74,74,30,83,239,156,176,207,193,19,123,73,223,128,217,72,17]
```

* Import this strings in Phantom wallet through 'Import Private Key'
* After imported successfully, then 'Menu' -> Manage Accounts' -> choose this account -> 'Show Private Key' -> input password -> get the private key like this:

```
3WssD84uuzqGyuoycsdfsaeytbzt32qP9CyejqbQksqxxxx
```

* This private key will be used in solxen-tx miner tool



### 4. Download solxen-tx miner tool

* Go to https://github.com/mmc-98/solxen-tx/releases
* Download the latest release (Windows/Mac/Linux)
* Decompress the download release file
* Modify the configuration file **solxen-tx.yaml**; you only need to change **Key** to your private key, and **ToAddr** to your xn airdrop address (ETH address format)

```
# sol config
Name: solxen-tx
Sol:
  Url: "https://api.devnet.solana.com"                          # rpc address
  Key: "3WssD84uuzqGyuoycsdfsaeytbzt32qP9CyejqbQksqxxxx"        # private key
  Num: 1                                                        # concurrency
  Fee: 3000                                                     # priority gas fee
  ToAddr: "0x4A7766axxxx"          								# xn airdrop address (eth addr format)
  ProgramID: "64SYet8RCT5ayZpMGbhcpk3vmt8UkwjZq8uy8Sd6V46A"     # solxen contract address
  Time: 1000                                                    # [interval time(ms)]
```

* Also suggest to change **Time** to 30000 (30 seconds) if considering request-limitation of public rpc.
* Run program solxen-tx in terminal/console/command



## SOLANA Mainnet

TODO
