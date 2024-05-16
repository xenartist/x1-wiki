# XOLANA Validator Guide

# Prerequisites

* System Tuning

Linux

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



# Building

## **1. Install rustc, cargo and rustfmt.**

```bash
$ curl https://sh.rustup.rs -sSf | sh
$ source $HOME/.cargo/env
$ rustup component add rustfmt
```

When building the master branch, please make sure you are using the latest stable rust version by running:

```bash
$ rustup update
```

On Linux systems you may need to install libssl-dev, pkg-config, zlib1g-dev, protobuf etc.

On Ubuntu:
```bash
$ sudo apt-get update
$ sudo apt-get install libssl-dev libudev-dev pkg-config zlib1g-dev llvm clang cmake make libprotobuf-dev protobuf-compiler
```

## **2. Download the source code.**

```bash
$ git clone https://github.com/jacklevin74/xolana.git
$ cd solana
$ git checkout v1.18.12
```

## **3. Build.**

```bash
$ ./cargo build --release
```

* Check version

```
./target/release/solana-validator -V
```
It should be shown like this:
```
solana-validator 1.18.12 (src:00000000; feat:4215500110, client:SolanaLabs)
```

## **4. Create key-pairs**

* Create a new wallet

```
./target/release/solana-keygen new --no-passphrase
```

* Create identity.json

```
./target/release/solana-keygen new --no-passphrase -o identity.json
```

* Create vote.json

```
./target/release/solana-keygen new --no-passphrase -o vote.json
```

* Create withdrawer.json

```
./target/release/solana-keygen new --no-passphrase -o  withdrawer.json
```

* Create stake.json

```
./target/release/solana-keygen new --no-passphrase -o stake.json
```

## **5. Airdrop testing SOL**

* Config 

```
./target/release/solana config set -u http://69.10.34.226:8899
```

* Airdrop SOL

```
./target/release/solana airdrop 50200
```

## **6. Run Validator**

```
./target/release/solana-validator --identity identity.json --limit-ledger-size --rpc-port 8899 --entrypoint 69.10.34.226:8001 --full-rpc-api --log ./log.txt --vote-account vote.json  --max-genesis-archive-unpacked-size 1073741824 --no-incremental-snapshots --require-tower --enable-rpc-transaction-history --enable-extended-tx-metadata-storage  --skip-startup-ledger-verification &
```

Check normal logs
```
tail -f log.txt
```

Check catch up status

```
./target/release/solana catchup --our-localhost
```

Should be shown info like this:

```
<IDENTITY_PUBKEY> has caught up (us: 74487 them: 74488)
```

Check validator status

```
./target/release/solana gossip
```
and 

```
./target/release/solana validators
```

Check ledger status

```
./target/release/solana-validator --ledger ./ledger monitor
```

## **7. Transfer 100 SOL to identity account**

```
./target/release/solana transfer <IDENTITY_PUBKEY> 100
```

## **8. Create Stake Account**

```
./target/release/solana create-stake-account stake.json 10
```

## **9. Create Vote Account**

```
./target/release/solana create-vote-account vote.json identity.json  <WITHDRAWER_PUBKEY> --commission 10
```

## **10. Stake**

Transfer 50,000 SOL to public address of stake.

```
./target/release/solana transfer <STAKE_PUBKEY> 50000
```

Do delegate stake operation.

```
./target/release/solana delegate-stake stake.json vote.json
```

Do stake operation.

```
./target/release/solana stake-account stake.json
```

## **11. Check status**

Normal logs
```
tail -f log.txt
```

Check leader schedule
```
./target/release/solana leader-schedule | grep <IDENTITY_PUBKEY>
```
or 
```
tail -f log.txt | grep -i "My next leader slot"
```

Check validator status

```
./target/release/solana gossip
```
and 

```
./target/release/solana validators
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