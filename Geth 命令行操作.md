# Geth

### Geth操作

1. 初始化`geth --datadir aChain/data0 init aChian/genesis.json`
   1. aChain/genesis.json是创世区块路径
2. 启动Geth控制台`geth --datadir aChain/data0 --networkid 1108 console 2>>aChain/geth.log`
3. 打开一个新的命令行输入`tail -f aChain\geth.log`查看日志

+++

### Geth 控制台操作

1. 检查是否存在账户`eth.accounts`
2. 创建新的账户`personal.newAccount()`或`personal.newAccount("123456")`
3. 开始挖矿`miner.start()`
4. 停止挖矿`miner.stop()`
5. 查看矿工地址`eth.coinbase`
6. 更改矿工`miner.setEtherbase(acc0)`
7. 查看区块数量`eth.blockNumber`
8. 查看余额`eth.getBalance(acc0)`
9. 转账`eth.sendTransaction({from:eth.accounts[0],to:eth.accounts[1],value:1})`以太坊存在保护机制每个一段时间账户就会自动锁定，这个时候任何以太币在账户之间的转换都会被拒绝，除非把该账户解锁。
10. 解锁账户`personal.unlockAccount(acc0)`

