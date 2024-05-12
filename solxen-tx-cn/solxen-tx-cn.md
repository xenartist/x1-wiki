# solXEN挖矿中文简明教程 2024.05.12

文档维护 by [xen_artist](https://twitter.com/xen_artist)

## 1. 下载 Solana 钱包

### Mac & Linux

### 1.1 下载 Solana 钱包

* 打开您喜欢的终端应用程序。

* 在您的机器上运行以下命令来安装 Solana 发行版 [v1.18.12](https://github.com/solana-labs/solana/releases/tag/v1.18.12)：

```
sh -c "$(curl -sSfL https://release.solana.com/v1.18.12/install)"
```

* 如有以下输出则表示下载成功：

```
  downloading v1.18.12 installer
  Configuration: /home/solana/.config/solana/install/config.yml
  Active release directory: /home/solana/.local/share/solana/install/active_release
  * Release version: v1.18.12
  * Release URL: https://github.com/solana-labs/solana/releases/download/v1.18.12/solana-release-x86_64-unknown-linux-gnu.tar.bz2
  Update successful
```

* 取决于不同系统，安装程序消息的末尾可能会提示：

```
Please update your PATH environment variable to include the solana programs:
```

* 如果看到上述消息，请复制并粘贴推荐的命令以更新 `PATH`

可以通过将以下行添加到 $HOME/.profile 或 /etc/profile（用于系统范围的安装）来执行此操作：

```
export PATH="/home/ubuntu/.local/share/solana/install/active_release/bin:$PATH"
```

**注意：** 对配置文件的更改可能不会立刻应用到当前回话，直到下次登录。要立即应用更改，只需直接运行 shell 命令或使用诸如 `source $HOME/.profile` 的命令从配置文件执行它们。

* 运行以下命令确认已安装所需版本的 `solana`：

```
solana --version
```

* 安装成功后，`solana-install update` 可以随时用于更新 Solana 软件至最新版本。

### Windows

### 1.2 下载 Solana 钱包

* 以管理员身份打开命令提示符（`cmd.exe`）

* 在 Windows 搜索栏中搜索命令提示符。当命令提示符应用程序出现时，请右键单击并选择“以管理员身份运行”。如果系统提示是否允许此应用程序更改您的设备，请单击是。

* 复制并粘贴以下命令，然后按 Enter 键将 Solana 安装程序下载到临时目录：

```
cmd /c "curl https://release.solana.com/v1.18.12/solana-install-init-x86_64-pc-windows-msvc.exe --output C:\solana-install-tmp\solana-install-init.exe --create-dirs"
```

* 复制并粘贴以下命令，然后按 Enter 键安装 Solana 的最新版本。如果您的系统看到安全提示，请选择允许程序运行。

```
C:\solana-install-tmp\solana-install-init.exe v1.18.12
```

* 安装程序完成后，按 Enter 键。

* 关闭命令提示符窗口，并重新以普通用户身份打开一个新的命令提示符窗口

* 在搜索栏中搜索“命令提示符”，然后单击命令提示符应用程序图标，无需以管理员身份运行）

* 输入以下命令确认您已安装所需版本的 `solana`：

```
solana --version
```

* 安装成功后，`solana-install update` 可以随时用于更新 Solana 软件至最新版本。

## 2. 创建新钱包

* 使用命令 `solana-keygen` 生成新钱包（**注意**：请将 **--derivation-path** 添加为参数）。

```
solana-keygen new --derivation-path
```

* 将提示以下信息，请按 ENTER 继续。

```
Generating a new keypair

For added security, enter a BIP39 passphrase

NOTE! This passphrase improves security of the recovery seed phrase NOT the
keypair file itself, which is stored as insecure plain text

BIP39 Passphrase (empty for none):  
```

* 然后将生成一个 12 个单词的种子短语（又称为助记词或恢复短语）（例如 *leaf jealous olympic later mistake slim oven depth under near very frown*），请将其保存在**安全**的地方，因为它将被用在 `solxen-tx.yaml` 的 **Mnemonic** 配置字段上。

```
Wrote new keypair to id.json
================================================================================
pubkey: 4tf7QSWxYFzmvicRimtJwCtuWfnPq43ZQxjkooCKKUJf
================================================================================
Save this seed phrase and your BIP39 passphrase to recover your new keypair:
leaf jealous olympic later mistake slim oven depth under near very frown
================================================================================
```

* 上面生成的公钥（例如 *4tf7QSWxYFzmvicRimtJwCtuWfnPq43ZQxjkooCKKUJf*）是公共主钱包地址（通常是第一个地址），将用于充值 SOL以运行 `solxen-tx`。

## 3. 获取 DEVNET 的 SOL 空投（可选）

* https://faucet.solana.com/
* https://faucet.quicknode.com/solana/
* https://solfaucet.com/

## 4. 下载最新版本的solxen-tx挖矿客户端（go语言版本）

* 下载地址：https://github.com/mmc-98/solxen-tx/releases
* Windows版本：solxen-tx-windows-amd64.zip
* macOS版本（Intel CPU）：solxen-tx-darwin-amd64.tar.gz
* macOS版本（M1/M2/M3 CPU）：solxen-tx-darwin-arm64.tar.gz
* Linux版本（Intel/AMD CPU）：solxen-tx-linux-amd64.tar.gz
* Linux版本（ARM嵌入式CPU）：solxen-tx-linux-arm64.tar.gz

## 5. 配置文件 solxen-tx.yaml

* 解压下载后的压缩包后，会看到2个文件，一个是solxen-tx的二进制可执行文件，另外一个是 solxen-tx.yaml配置文件；
* 开发网（devnet）配置文件详细说明：

```
  Name: solxen-tx
  Sol:
  Url: "https://api.devnet.solana.com"                          # rpc地址(可替换)
  Mnemonic: "leaf jealous olympic later mistake slim oven depth under near very frown" # 助记词(请替换为自己的助记词)
  Num: 1                                                        # 并发数(也即并发钱包数量)
  Fee: 3000                                                     # 优先级费用(单位为microLamports)
  ToAddr: "0xrjo23jro342r3ur90ewi0vjq3jr3o4i3por3k4r3"          # 接收xn空投的eth格式的地址(请替换为自己的钱包地址)
  ProgramID: "开发网上的合约地址"                                  # solxen合约地址
  Time: 1000                                                    # 间隔时间(单位毫秒)
  HdPAth: m/44'/501'/0'/0'                                      # 钱包地址路径(缺省即可)
```

* 主网（mainnet）配置文件详细说明：

```
Name: solxen-tx
Sol:
  Url: "https://api.mainnet-beta.solana.com"                    # rpc地址(可替换)
  Mnemonic: "leaf jealous olympic later mistake slim oven depth under near very frown" # 助记词(请替换为自己的助记词)
  Num: 1                                                        # 并发数(也即并发钱包数量)
  Fee: 3000                                                     # 优先级费用(单位为microLamports)
  ToAddr: "0xrjo23jro342r3ur90ewi0vjq3jr3o4i3por3k4r3"          # 接收xn空投的eth格式的地址(请替换为自己的钱包地址)
  ProgramID: "主网上的合约地址"                                    # solxen合约地址
  Time: 1000                                                    # 间隔时间(单位毫秒)
  HdPAth: m/44'/501'/0'/0'                                      # 钱包地址路径(缺省即可)
```

## 6. solXEN挖矿

* 配置文件设置好后，运行二进制可执行文件solxen-tx，启动程序，挖矿初始化；
* 在日志一开始，会显示使用的钱包地址是哪一个，或者多个（取决于配置文件中Num的数值是1还是>1的数值）；请确保充值的钱包地址是正确的；
* 停掉程序，充值SOL到挖矿钱包地址；
* 充值成功后，再次启动程序，正式开始挖矿；
* 在solXEN挖矿排行榜查看个人挖矿信息：https://sol-xen-app.infrafc.org/leaderboard

## 7. 其他参考信息

* solXEN挖矿白皮书：https://docs.solxen.io/
* solXEN挖矿排行榜：https://sol-xen-app.infrafc.org/leaderboard [备用: https://leaderboard.solxen.io/]
* solXEN挖矿英文电报：https://t.me/+Z5kEez70pyQ5NTAz
* solXEN挖矿中文电报：https://t.me/XENChatCn
* X1/XEN生态百科全书：https://x1.wiki
