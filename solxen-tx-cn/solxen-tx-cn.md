# solXEN挖矿中文简明教程

## 1. 安装 Phantom 网页钱包 （或者任意支持Solana的Web3钱包，比如OKX/SolFlare等）

* 如果是第一次创建账户，会生成12个单词的助记词，保存下来，会在solxen-tx的配置文件中用到；
* 如果不是第一次创建账户，则从已有账户导出12个单词的助记词即可；
* 为了方便理解，这里举例12个单词的助记词为：

```
leaf jealous olympic later mistake slim oven depth under near very frown
```

* 注意：主钱包一般为第一个钱包地址；



## 2. 下载最新版本的solxen-tx挖矿客户端（go语言版本）

* 下载地址：https://github.com/mmc-98/solxen-tx/releases
* Windows版本：solxen-tx-windows-amd64.zip
* macOS版本（Intel CPU）：solxen-tx-darwin-amd64.tar.gz
* macOS版本（M1/M2/M3 CPU）：solxen-tx-darwin-arm64.tar.gz
* Linux版本（Intel/AMD CPU）：solxen-tx-linux-amd64.tar.gz
* Linux版本（ARM嵌入式CPU）：solxen-tx-darwin-arm64.tar.gz

## 3. 配置文件 solxen-tx.yaml

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

## 4. solXEN挖矿

* 配置文件设置好后，运行二进制可执行文件solxen-tx，启动程序，挖矿初始化；
* 在日志一开始，会显示使用的钱包地址是哪一个，或者多个（取决于配置文件中Num的数值是1还是>1的数值）；注意和web3钱包中的钱包地址进行核对，确保充值的钱包地址是正确匹配的；
* 停掉程序，充值SOL到挖矿钱包地址；
* 充值成功后，再次启动程序，正式开始挖矿；
* 在solXEN挖矿排行榜查看个人挖矿信息：https://sol-xen-app.infrafc.org/leaderboard

## 5. 其他参考信息

* solXEN挖矿白皮书：https://docs.solxen.io/
* solXEN挖矿排行榜：https://sol-xen-app.infrafc.org/leaderboard
* solXEN挖矿英文电报：https://t.me/+Z5kEez70pyQ5NTAz
* solXEN挖矿中文电报：https://t.me/XENChatCn
* X1/XEN生态百科全书：https://x1.wiki
