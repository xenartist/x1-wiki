# XOLANA Validator Guide

# Install The Solana CLI (Linux)


* Open your favorite Terminal application
* Install the Solana release [v1.18.15](https://github.com/solana-labs/solana/releases/tag/v1.18.15) on your machine by running:

  ```
  sh -c "$(curl -sSfL https://release.solana.com/v1.18.15/install)"
  ```

* The following output indicates a successful update:

  ```
  downloading v1.18.15 installer
  Configuration: /home/solana/.config/solana/install/config.yml
  Active release directory: /home/solana/.local/share/solana/install/active_release
  * Release version: v1.18.15
  * Release URL: https://github.com/solana-labs/solana/releases/download/v1.18.15/solana-release-x86_64-unknown-linux-gnu.tar.bz2
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



# System Tuning (Linux)

Your system will need to be tuned in order to run properly. Your validator may not start without the settings below.

Optimize sysctl knobs

```
sudo bash -c "cat >/etc/sysctl.d/21-solana-validator.conf <<EOF
# Increase UDP buffer sizes
net.core.rmem_default = 134217728
net.core.rmem_max = 134217728
net.core.wmem_default = 134217728
net.core.wmem_max = 134217728

# Increase memory mapped files limit
vm.max_map_count = 1000000

# Increase number of allowed open file descriptors
fs.nr_open = 1000000
EOF"
```

```
sudo sysctl -p /etc/sysctl.d/21-solana-validator.conf
```

* Increase systemd and session file limits

Add
```
LimitNOFILE=1000000
```
to the [Service] section of your systemd service file, if you use one, otherwise add
```
DefaultLimitNOFILE=1000000
```
to the [Manager] section of /etc/systemd/system.conf.
```
sudo systemctl daemon-reload

sudo bash -c "cat >/etc/security/limits.d/90-solana-nofiles.conf <<EOF
# Increase process file descriptor count limit
* - nofile 1000000
EOF"
```

* Close all open sessions (log out then, in again) ###



# Building (Optional)

### (If not trying to run solana-validator from the source code, then just skip the following building steps)

## **1. Install rustc, cargo and rustfmt.**

```bash
curl https://sh.rustup.rs -sSf | sh
source $HOME/.cargo/env
rustup component add rustfmt
```

When building the master branch, please make sure you are using the latest stable rust version by running:

```bash
rustup update
```

On Linux systems you may need to install libssl-dev, pkg-config, zlib1g-dev, protobuf etc.

On Ubuntu:
```bash
sudo apt-get update
sudo apt-get install libssl-dev libudev-dev pkg-config zlib1g-dev llvm clang cmake make libprotobuf-dev protobuf-compiler
```

## **2. Download the source code.**

```bash
git clone https://github.com/jacklevin74/xolana.git
cd xolana
git checkout xolana
```

## **3. Build.**

```bash
cargo build --release
```

* Check version

```
./target/release/solana-validator -V
```
It should be shown like this:
```
solana-validator 1.18.15 (src:00000000; feat:4215500110, client:SolanaLabs)
```



# Running

## **4. Create key-pairs**

* Create a new wallet

```
solana-keygen new --no-passphrase
```

* Create identity.json

```
solana-keygen new --no-passphrase -o identity.json
```

* Create vote.json

```
solana-keygen new --no-passphrase -o vote.json
```

* Create withdrawer.json

```
solana-keygen new --no-passphrase -o  withdrawer.json
```

* Create stake.json

```
solana-keygen new --no-passphrase -o stake.json
```

## **5. Airdrop testing SOL**

* Config 

```
solana config set -u http://xolana.xen.network:8899
```

* Airdrop SOL

```
solana airdrop 100
```

## **6. Run Validator**

* **If running solana-validator from installed solana cli directly:**

```
nohup solana-validator --identity identity.json --limit-ledger-size 50000000 --rpc-port 8899 --entrypoint xolana.xen.network:8001 --full-rpc-api --log - --vote-account vote.json --max-genesis-archive-unpacked-size 1073741824 --no-incremental-snapshots --require-tower --enable-rpc-transaction-history --enable-extended-tx-metadata-storage --skip-startup-ledger-verification &
```

* **If running solana-validator from the bianry built through xolana source code:**

```
nohup ./target/release/solana-validator --identity identity.json --limit-ledger-size 50000000 --rpc-port 8899 --entrypoint xolana.xen.network:8001 --full-rpc-api --log - --vote-account vote.json --max-genesis-archive-unpacked-size 1073741824 --no-incremental-snapshots --require-tower --enable-rpc-transaction-history --enable-extended-tx-metadata-storage --skip-startup-ledger-verification &
```

Check normal logs
```
tail -f nohup.out
```

Check catch up status

```
solana catchup --our-localhost
```

Should be shown info like this:

```
<IDENTITY_PUBKEY> has caught up (us: 74487 them: 74488)
```

Check validator status

```
solana gossip
```
and 

```
solana validators
```

Check ledger status

```
./target/release/solana-validator --ledger ./ledger monitor
```

## **7. Transfer 100 SOL to identity account**

```
solana transfer <IDENTITY_PUBKEY> 100
```

## **8. Create Stake Account**

```
solana create-stake-account stake.json 10
```

## **9. Create Vote Account**

```
solana create-vote-account vote.json identity.json  <WITHDRAWER_PUBKEY> --commission 10
```

## **10. Stake**

Transfer some SOL (eg. 50000) to public address of stake.

```
solana transfer <STAKE_PUBKEY> 50000
```

Do delegate stake operation.

```
solana delegate-stake stake.json vote.json
```

Do stake operation.

```
solana stake-account stake.json
```

## **11. Check status**

Normal logs
```
tail -f log.txt
```

Check leader schedule
```
solana leader-schedule | grep <IDENTITY_PUBKEY>
```
or 
```
tail -f log.txt | grep -i "My next leader slot"
```

Check validator status

```
solana gossip
```
and 

```
solana validators
```

## **12. Kill Validator Process**

Check validator process

```
ps aux | grep solana-validator
```

Kill validator process

```
pkill -f solana-validator
```

Check validator process again, make sure it has been killed properly

```
ps aux | grep solana-validator
```