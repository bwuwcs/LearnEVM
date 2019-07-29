# EVM 操作码表

### 1. [solidity文档中的操作码表](https://solidity-cn.readthedocs.io/zh/develop/assembly.html)

| Instruction                                  |      |      | Explanation                                                  |
| -------------------------------------------- | ---- | ---- | ------------------------------------------------------------ |
| stop                                         | -    | F    | 停止执行，与 return(0,0) 等价                                |
| add(x, y)                                    |      | F    | x + y                                                        |
| sub(x, y)                                    |      | F    | x - y                                                        |
| mul(x, y)                                    |      | F    | x * y                                                        |
| div(x, y)                                    |      | F    | x / y                                                        |
| sdiv(x, y)                                   |      | F    | x / y，以二进制补码作为符号                                  |
| mod(x, y)                                    |      | F    | x % y                                                        |
| smod(x, y)                                   |      | F    | x % y，以二进制补码作为符号                                  |
| exp(x, y)                                    |      | F    | x 的 y 次幂                                                  |
| not(x)                                       |      | F    | ~x，对 x 按位取反                                            |
| lt(x, y)                                     |      | F    | 如果 x < y 为 1，否则为 0                                    |
| gt(x, y)                                     |      | F    | 如果 x > y 为 1，否则为 0                                    |
| slt(x, y)                                    |      | F    | 如果 x < y 为 1，否则为 0，以二进制补码作为符号              |
| sgt(x, y)                                    |      | F    | 如果 x > y 为 1，否则为 0，以二进制补码作为符号              |
| eq(x, y)                                     |      | F    | 如果 x == y 为 1，否则为 0                                   |
| iszero(x)                                    |      | F    | 如果 x == 0 为 1，否则为 0                                   |
| and(x, y)                                    |      | F    | x 和 y 的按位与                                              |
| or(x, y)                                     |      | F    | x 和 y 的按位或                                              |
| xor(x, y)                                    |      | F    | x 和 y 的按位异或                                            |
| byte(n, x)                                   |      | F    | x 的第 n 个字节，这个索引是从 0 开始的                       |
| shl(x, y)                                    |      | C    | 将 y 逻辑左移 x 位                                           |
| shr(x, y)                                    |      | C    | 将 y 逻辑右移 x 位                                           |
| sar(x, y)                                    |      | C    | 将 y 算术右移 x 位                                           |
| addmod(x, y, m)                              |      | F    | 任意精度的 (x + y) % m                                       |
| mulmod(x, y, m)                              |      | F    | 任意精度的 (x * y) % m                                       |
| signextend(i, x)                             |      | F    | 对 x 的最低位到第 (i * 8 + 7) 进行符号扩展                   |
| keccak256(p, n)                              |      | F    | keccak(mem[p...(p + n)))                                     |
| jump(label)                                  | -    | F    | 跳转到标签 / 代码位置                                        |
| jumpi(label, cond)                           | -    | F    | 如果条件为非零，跳转到标签                                   |
| pc                                           |      | F    | 当前代码位置                                                 |
| pop(x)                                       | -    | F    | 删除（弹出）栈顶的 x 个元素                                  |
| dup1 ... dup16                               |      | F    | 将栈内第 i 个元素（从栈顶算起）复制到栈顶                    |
| swap1 ... swap16                             | *    | F    | 将栈顶元素和其下第 i 个元素互换                              |
| mload(p)                                     |      | F    | mem[p...(p + 32))                                            |
| mstore(p, v)                                 | -    | F    | mem[p...(p + 32)) := v                                       |
| mstore8(p, v)                                | -    | F    | mem[p] := v & 0xff （仅修改一个字节）                        |
| sload(p)                                     |      | F    | storage[p]                                                   |
| sstore(p, v)                                 | -    | F    | storage[p] := v                                              |
| msize                                        |      | F    | 内存大小，即最大可访问内存索引                               |
| gas                                          |      | F    | 执行可用的 gas                                               |
| address                                      |      | F    | 当前合约 / 执行上下文的地址                                  |
| balance(a)                                   |      | F    | 地址 a 的余额，以 wei 为单位                                 |
| caller                                       |      | F    | 调用发起者（不包括 `delegatecall`）                          |
| callvalue                                    |      | F    | 随调用发送的 Wei 的数量                                      |
| calldataload(p)                              |      | F    | 位置 p 的调用数据（32 字节）                                 |
| calldatasize                                 |      | F    | 调用数据的字节数大小                                         |
| calldatacopy(t, f, s)                        | -    | F    | 从调用数据的位置 f 的拷贝 s 个字节到内存的位置 t             |
| codesize                                     |      | F    | 当前合约 / 执行上下文地址的代码大小                          |
| codecopy(t, f, s)                            | -    | F    | 从代码的位置 f 开始拷贝 s 个字节到内存的位置 t               |
| extcodesize(a)                               |      | F    | 地址 a 的代码大小                                            |
| extcodecopy(a, t, f, s)                      | -    | F    | 和 codecopy(t, f, s) 类似，但从地址 a 获取代码               |
| returndatasize                               |      | B    | 最后一个 returndata 的大小                                   |
| returndatacopy(t, f, s)                      | -    | B    | 从 returndata 的位置 f 拷贝 s 个字节到内存的位置 t           |
| create(v, p, s)                              |      | F    | 用 mem[p...(p + s)) 中的代码创建一个新合约、发送 v wei 并返回 新地址 |
| create2(v, n, p, s)                          |      | C    | 用 mem[p...(p + s)) 中的代码，在地址 keccak256(<address> . n . keccak256(mem[p...(p + s))) 上 创建新合约、发送 v wei 并返回新地址 |
| call(g, a, v, in, insize, out, outsize)      |      | F    | 使用 mem[in...(in + insize)) 作为输入数据， 提供 g gas 和 v wei 对地址 a 发起消息调用， 输出结果数据保存在 mem[out...(out + outsize))， 发生错误（比如 gas 不足）时返回 0，正确结束返回 1 |
| callcode(g, a, v, in, insize, out, outsize)  |      | F    | 与 `call` 等价，但仅使用地址 a 中的代码 且保持当前合约的执行上下文 |
| delegatecall(g, a, in, insize, out, outsize) |      | F    | 与 `callcode` 等价且保留 `caller` 和 `callvalue`             |
| staticcall(g, a, in, insize, out, outsize)   |      | F    | 与 `call(g, a, 0, in, insize, out, outsize)` 等价 但不允许状态修改 |
| return(p, s)                                 | -    | F    | 终止运行，返回 mem[p...(p + s)) 的数据                       |
| revert(p, s)                                 | -    | B    | 终止运行，撤销状态变化，返回 mem[p...(p + s)) 的数据         |
| selfdestruct(a)                              | -    | F    | 终止运行，销毁当前合约并且把资金发送到地址 a                 |
| invalid                                      | -    | F    | 以无效指令终止运行                                           |
| log0(p, s)                                   | -    | F    | 以 mem[p...(p + s)) 的数据产生不带 topic 的日志              |
| log1(p, s, t1)                               | -    | F    | 以 mem[p...(p + s)) 的数据和 topic t1 产生日志               |
| log2(p, s, t1, t2)                           | -    | F    | 以 mem[p...(p + s)) 的数据和 topic t1、t2 产生日志           |
| log3(p, s, t1, t2, t3)                       | -    | F    | 以 mem[p...(p + s)) 的数据和 topic t1、t2、t3 产生日志       |
| log4(p, s, t1, t2, t3, t4)                   | -    | F    | 以 mem[p...(p + s)) 的数据和 topic t1、t2、t3 和 t4 产生日志 |
| origin                                       |      | F    | 交易发起者地址                                               |
| gasprice                                     |      | F    | 交易所指定的 gas 价格                                        |
| blockhash(b)                                 |      | F    | 区块号 b 的哈希 - 目前仅适用于不包括当前区块的最后 256 个区块 |
| coinbase                                     |      | F    | 当前的挖矿收益者地址                                         |
| timestamp                                    |      | F    | 从当前 epoch 开始的当前区块时间戳（以秒为单位）              |
| number                                       |      | F    | 当前区块号                                                   |
| difficulty                                   |      | F    | 当前区块难度                                                 |
| gaslimit                                     |      | F    | 当前区块的 gas 上限                                          |

### 2. [汇编指令集完整的列表](https://www.jianshu.com/p/230c6d805560)

| uint8 | Mnemonic| Expression  | Notes |Explanation|
| :----------------------------- | :--------------- | :----------------------| :----------------------------------------------------------- |:------------------|
| [`00`](https://ethervm.io/#00) | `STOP`| `STOP()`| halts execution of the contract                              ||
| [`01`](https://ethervm.io/#01) | `ADD`            | `a + b`                                                      | (u)int256 addition modulo 2**256                             ||
| [`02`](https://ethervm.io/#02) | `MUL`            | `a * b`                                                      | (u)int256 multiplication modulo 2**256                       ||
| [`03`](https://ethervm.io/#03) | `SUB`            | `a - b`                                                      | (u)int256 subtraction modulo 2**256                          ||
| [`04`](https://ethervm.io/#04) | `DIV`            | `a // b`                                                     | uint256 division                                             ||
| [`05`](https://ethervm.io/#05) | `SDIV`           | `a // b`                                                     | int256 division                                              ||
| [`06`](https://ethervm.io/#06) | `MOD`            | `a % b`                                                      | uint256 modulus                                              ||
| [`07`](https://ethervm.io/#07) | `SMOD`           | `a % b`                                                      | int256 modulus                                               ||
| [`08`](https://ethervm.io/#08) | `ADDMOD`         | `(a + b) % N`                                                | (u)int256 addition modulo N                                  ||
| [`09`](https://ethervm.io/#09) | `MULMOD`         | `(a * b) % N`                                                | (u)int256 multiplication modulo N                            ||
| [`0A`](https://ethervm.io/#0A) | `EXP`            | `a ** b`                                                     | uint256 exponentiation modulo 2**256                         ||
| [`0B`](https://ethervm.io/#0B) | `SIGNEXTEND`     | `y = SIGNEXTEND(x, b)`                                       | sign extends x from (b + 1) * 8 bits to 256 bits.            ||
| [`0C`](https://ethervm.io/#0C) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`0D`](https://ethervm.io/#0D) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`0E`](https://ethervm.io/#0E) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`0F`](https://ethervm.io/#0F) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`10`](https://ethervm.io/#10) | `LT`             | `a < b`                                                      | uint256 comparison                                           ||
| [`11`](https://ethervm.io/#11) | `GT`             | `a > b`                                                      | uint256 comparison                                           ||
| [`12`](https://ethervm.io/#12) | `SLT`            | `a < b`                                                      | int256 comparison                                            ||
| [`13`](https://ethervm.io/#13) | `SGT`            | `a > b`                                                      | int256 comparison                                            ||
| [`14`](https://ethervm.io/#14) | `EQ`             | `a == b`                                                     | (u)int256 equality                                           ||
| [`15`](https://ethervm.io/#15) | `ISZERO`         | `a == 0`                                                     | (u)int256 is zero                                            |如果 a == 0 为 1，否则为 0|
| [`16`](https://ethervm.io/#16) | `AND`            | `a & b`                                                      | 256-bit bitwise and                                          ||
| [`17`](https://ethervm.io/#17) | `OR`             | `a | b`                                                      | 256-bit bitwise or                                           ||
| [`18`](https://ethervm.io/#18) | `XOR`            | `a ^ b`                                                      | 256-bit bitwise xor                                          ||
| [`19`](https://ethervm.io/#19) | `NOT`            | `~a`                                                         | 256-bit bitwise not                                          ||
| [`1A`](https://ethervm.io/#1A) | `BYTE`           | `y = (x >> (248 - i * 8)) & 0xFF`| ith byte of (u)int256 x, counting from most significant byte ||
| [`1B`](https://ethervm.io/#1B) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`1C`](https://ethervm.io/#1C) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`1D`](https://ethervm.io/#1D) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`1E`](https://ethervm.io/#1E) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`1F`](https://ethervm.io/#1F) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`20`](https://ethervm.io/#20) | `SHA3`           | [跳转](https://ethervm.io/#20) | keccak256                                                    ||
| [`21`](https://ethervm.io/#21) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`22`](https://ethervm.io/#22) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`23`](https://ethervm.io/#23) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`24`](https://ethervm.io/#24) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`25`](https://ethervm.io/#25) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`26`](https://ethervm.io/#26) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`27`](https://ethervm.io/#27) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`28`](https://ethervm.io/#28) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`29`](https://ethervm.io/#29) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`2A`](https://ethervm.io/#2A) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`2B`](https://ethervm.io/#2B) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`2C`](https://ethervm.io/#2C) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`2D`](https://ethervm.io/#2D) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`2E`](https://ethervm.io/#2E) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`2F`](https://ethervm.io/#2F) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`30`](https://ethervm.io/#30) | `ADDRESS`        | `address(this)`                                              | address of the executing contract||
| [`31`](https://ethervm.io/#31) | `BALANCE`        | `address(addr).balance`                                      | address balance in wei                                       ||
| [`32`](https://ethervm.io/#32) | `ORIGIN`         | `tx.origin`                                                  | transaction origin address                                   ||
| [`33`](https://ethervm.io/#33) | `CALLER`         | `msg.caller`                                                 | message caller address                                       ||
| [`34`](https://ethervm.io/#34) | `CALLVALUE`      | `msg.value`                                                  | message funds in wei                                         ||
| [`35`](https://ethervm.io/#35) | `CALLDATALOAD`   | `msg.data[i:i+32]`                                           | reads a (u)int256 from message data                          ||
| [`36`](https://ethervm.io/#36) | `CALLDATASIZE`   | `msg.data.size`                                              | message data length in bytes                                 ||
| [`37`](https://ethervm.io/#37) | `CALLDATACOPY`   | [跳转](https://ethervm.io/#37) | copy message data||
| [`38`](https://ethervm.io/#38) | `CODESIZE`       | `address(this).code.size`                                    | length of the executing contract's code in bytes             ||
| [`39`](https://ethervm.io/#39) | `CODECOPY`       | `memory[destOffset:destOffset+length] =     address(this).code[offset:offset+length]` | copy executing contract's bytecode                           ||
| [`3A`](https://ethervm.io/#3A) | `GASPRICE`       | `tx.gasprice`                                                | gas price of the executing transaction, in wei per unit of gas ||
| [`3B`](https://ethervm.io/#3B) | `EXTCODESIZE`    | `address(addr).code.size`                                    | length of the contract bytecode at addr, in bytes            ||
| [`3C`](https://ethervm.io/#3C) | `EXTCODECOPY`    | `memory[destOffset:destOffset+length] =     address(addr).code[offset:offset+length]` | copy contract's bytecode                                     ||
| [`3D`](https://ethervm.io/#3D) | `RETURNDATASIZE` | `size = RETURNDATASIZE()`                                    | the size of the returned data from the last external call, in bytes ||
| [`3E`](https://ethervm.io/#3E) | `RETURNDATACOPY` | `memory[destOffset:destOffset+length] =     RETURNDATA[offset:offset+length]` | copy returned data                                           ||
| [`3F`](https://ethervm.io/#3F) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`40`](https://ethervm.io/#40) | `BLOCKHASH`      | `hash = block.blockHash(blockNumber)`                        | hash of the specific block, only valid for the 256 most recent blocks, excluding the current one ||
| [`41`](https://ethervm.io/#41) | `COINBASE`       | `block.coinbase`                                             | address of the current block's miner                         ||
| [`42`](https://ethervm.io/#42) | `TIMESTAMP`      | `block.timestamp`                                            | current block's Unix timestamp in seconds                    ||
| [`43`](https://ethervm.io/#43) | `NUMBER`         | `block.number`                                               | current block's number                                       ||
| [`44`](https://ethervm.io/#44) | `DIFFICULTY`     | `block.difficulty`                                           | current block's difficulty                                   ||
| [`45`](https://ethervm.io/#45) | `GASLIMIT`       | `block.gaslimit`                                             | current block's gas limit                                    ||
| [`46`](https://ethervm.io/#46) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`47`](https://ethervm.io/#47) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`48`](https://ethervm.io/#48) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`49`](https://ethervm.io/#49) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`4A`](https://ethervm.io/#4A) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`4B`](https://ethervm.io/#4B) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`4C`](https://ethervm.io/#4C) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`4D`](https://ethervm.io/#4D) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`4E`](https://ethervm.io/#4E) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`4F`](https://ethervm.io/#4F) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`50`](https://ethervm.io/#50) | `POP`            | `POP()`                                                      | pops a (u)int256 off the stack and discards it               ||
| [`51`](https://ethervm.io/#51) | `MLOAD`          |                            | reads a (u)int256 from memory                                ||
| [`52`](https://ethervm.io/#52) | `MSTORE`         |                                                              | writes a (u)int256 to memory                                 ||
| [`53`](https://ethervm.io/#53) | `MSTORE8`        | `memory[offset] = value & 0xFF`                              | writes a uint8 to memory                                     ||
| [`54`](https://ethervm.io/#54) | `SLOAD`          | `value = storage[key]`                                       | reads a (u)int256 from storage                               ||
| [`55`](https://ethervm.io/#55) | `SSTORE`         | `storage[key] = value`                                       | writes a (u)int256 to storage                                ||
| [`56`](https://ethervm.io/#56) | `JUMP`           | `$pc = destination`                                          | unconditional jump                                           ||
| [`57`](https://ethervm.io/#57) | `JUMPI`          | $pc = cond ? destination : $pc + 1| conditional jump if condition is truthy                      |栈中先后pop出两个值x,y，x表示跳转到第几个JUMPDEST，而y表示一个标记（若为0，则跳到下一个JUMPDEST）,若y不为0，则由x决定跳到第几个。|
| [`58`](https://ethervm.io/#58) | `PC`             | `$pc`                                                        | program counter                                              ||
| [`59`](https://ethervm.io/#59) | `MSIZE`          | `size = MSIZE()`                                             | size of memory for this contract execution, in bytes         ||
| [`5A`](https://ethervm.io/#5A) | `GAS`            | `gasRemaining = GAS()`                                       | remaining gas                                                ||
| [`5B`](https://ethervm.io/#5B) | `JUMPDEST`       | ``                                                           | metadata to annotate possible jump destinations              ||
| [`5C`](https://ethervm.io/#5C) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`5D`](https://ethervm.io/#5D) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`5E`](https://ethervm.io/#5E) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`5F`](https://ethervm.io/#5F) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`60`](https://ethervm.io/#60) | `PUSH1`          | `PUSH(uint8)`                                                | pushes a 1-byte value onto the stack                         ||
| [`61`](https://ethervm.io/#61) | `PUSH2`          | `PUSH(uint16)`                                               | pushes a 2-byte value onto the stack                         ||
| [`62`](https://ethervm.io/#62) | `PUSH3`          | `PUSH(uint24)`                                               | pushes a 3-byte value onto the stack                         ||
| [`63`](https://ethervm.io/#63) | `PUSH4`          | `PUSH(uint32)`                                               | pushes a 4-byte value onto the stack                         ||
| [`64`](https://ethervm.io/#64) | `PUSH5`          | `PUSH(uint40)`                                               | pushes a 5-byte value onto the stack                         ||
| [`65`](https://ethervm.io/#65) | `PUSH6`          | `PUSH(uint48)`                                               | pushes a 6-byte value onto the stack                         ||
| [`66`](https://ethervm.io/#66) | `PUSH7`          | `PUSH(uint56)`                                               | pushes a 7-byte value onto the stack                         ||
| [`67`](https://ethervm.io/#67) | `PUSH8`          | `PUSH(uint64)`                                               | pushes a 8-byte value onto the stack                         ||
| [`68`](https://ethervm.io/#68) | `PUSH9`          | `PUSH(uint72)`                                               | pushes a 9-byte value onto the stack                         ||
| [`69`](https://ethervm.io/#69) | `PUSH10`         | `PUSH(uint80)`                                               | pushes a 10-byte value onto the stack                        ||
| [`6A`](https://ethervm.io/#6A) | `PUSH11`         | `PUSH(uint88)`                                               | pushes a 11-byte value onto the stack                        ||
| [`6B`](https://ethervm.io/#6B) | `PUSH12`         | `PUSH(uint96)`                                               | pushes a 12-byte value onto the stack                        ||
| [`6C`](https://ethervm.io/#6C) | `PUSH13`         | `PUSH(uint104)`                                              | pushes a 13-byte value onto the stack                        ||
| [`6D`](https://ethervm.io/#6D) | `PUSH14`         | `PUSH(uint112)`                                              | pushes a 14-byte value onto the stack                        ||
| [`6E`](https://ethervm.io/#6E) | `PUSH15`         | `PUSH(uint120)`                                              | pushes a 15-byte value onto the stack                        ||
| [`6F`](https://ethervm.io/#6F) | `PUSH16`         | `PUSH(uint128)`                                              | pushes a 16-byte value onto the stack                        ||
| [`70`](https://ethervm.io/#70) | `PUSH17`         | `PUSH(uint136)`                                              | pushes a 17-byte value onto the stack                        ||
| [`71`](https://ethervm.io/#71) | `PUSH18`         | `PUSH(uint144)`                                              | pushes a 18-byte value onto the stack                        ||
| [`72`](https://ethervm.io/#72) | `PUSH19`         | `PUSH(uint152)`                                              | pushes a 19-byte value onto the stack                        ||
| [`73`](https://ethervm.io/#73) | `PUSH20`         | `PUSH(uint160)`                                              | pushes a 20-byte value onto the stack                        ||
| [`74`](https://ethervm.io/#74) | `PUSH21`         | `PUSH(uint168)`                                              | pushes a 21-byte value onto the stack                        ||
| [`75`](https://ethervm.io/#75) | `PUSH22`         | `PUSH(uint176)`                                              | pushes a 22-byte value onto the stack                        ||
| [`76`](https://ethervm.io/#76) | `PUSH23`         | `PUSH(uint184)`                                              | pushes a 23-byte value onto the stack                        ||
| [`77`](https://ethervm.io/#77) | `PUSH24`         | `PUSH(uint192)`                                              | pushes a 24-byte value onto the stack                        ||
| [`78`](https://ethervm.io/#78) | `PUSH25`         | `PUSH(uint200)`                                              | pushes a 25-byte value onto the stack                        ||
| [`79`](https://ethervm.io/#79) | `PUSH26`         | `PUSH(uint208)`                                              | pushes a 26-byte value onto the stack                        ||
| [`7A`](https://ethervm.io/#7A) | `PUSH27`         | `PUSH(uint216)`                                              | pushes a 27-byte value onto the stack                        ||
| [`7B`](https://ethervm.io/#7B) | `PUSH28`         | `PUSH(uint224)`                                              | pushes a 28-byte value onto the stack                        ||
| [`7C`](https://ethervm.io/#7C) | `PUSH29`         | `PUSH(uint232)`                                              | pushes a 29-byte value onto the stack                        ||
| [`7D`](https://ethervm.io/#7D) | `PUSH30`         | `PUSH(uint240)`                                              | pushes a 30-byte value onto the stack                        ||
| [`7E`](https://ethervm.io/#7E) | `PUSH31`         | `PUSH(uint248)`                                              | pushes a 31-byte value onto the stack                        ||
| [`7F`](https://ethervm.io/#7F) | `PUSH32`         | `PUSH(uint256)`                                              | pushes a 32-byte value onto the stack                        ||
| [`80`](https://ethervm.io/#80) | `DUP1`           | `PUSH(value)`                                                | clones the last value on the stack                           ||
| [`81`](https://ethervm.io/#81) | `DUP2`           | `PUSH(value)`                                                | clones the 2nd last value on the stack                       ||
| [`82`](https://ethervm.io/#82) | `DUP3`           | `PUSH(value)`                                                | clones the 3rd last value on the stack                       ||
| [`83`](https://ethervm.io/#83) | `DUP4`           | `PUSH(value)`                                                | clones the 4th last value on the stack                       ||
| [`84`](https://ethervm.io/#84) | `DUP5`           | `PUSH(value)`                                                | clones the 5th last value on the stack                       ||
| [`85`](https://ethervm.io/#85) | `DUP6`           | `PUSH(value)`                                                | clones the 6th last value on the stack                       ||
| [`86`](https://ethervm.io/#86) | `DUP7`           | `PUSH(value)`                                                | clones the 7th last value on the stack                       ||
| [`87`](https://ethervm.io/#87) | `DUP8`           | `PUSH(value)`                                                | clones the 8th last value on the stack                       ||
| [`88`](https://ethervm.io/#88) | `DUP9`           | `PUSH(value)`                                                | clones the 9th last value on the stack                       ||
| [`89`](https://ethervm.io/#89) | `DUP10`          | `PUSH(value)`                                                | clones the 10th last value on the stack                      ||
| [`8A`](https://ethervm.io/#8A) | `DUP11`          | `PUSH(value)`                                                | clones the 11th last value on the stack                      ||
| [`8B`](https://ethervm.io/#8B) | `DUP12`          | `PUSH(value)`                                                | clones the 12th last value on the stack                      ||
| [`8C`](https://ethervm.io/#8C) | `DUP13`          | `PUSH(value)`                                                | clones the 13th last value on the stack                      ||
| [`8D`](https://ethervm.io/#8D) | `DUP14`          | `PUSH(value)`                                                | clones the 14th last value on the stack                      ||
| [`8E`](https://ethervm.io/#8E) | `DUP15`          | `PUSH(value)`                                                | clones the 15th last value on the stack                      ||
| [`8F`](https://ethervm.io/#8F) | `DUP16`          | `PUSH(value)`                                                | clones the 16th last value on the stack                      ||
| [`90`](https://ethervm.io/#90) | `SWAP1`          | `a, b = b, a`                                                | swaps the last two values on the stack                       ||
| [`91`](https://ethervm.io/#91) | `SWAP2`          | `a, b = b, a`                                                | swaps the top of the stack with the 3rd last element         ||
| [`92`](https://ethervm.io/#92) | `SWAP3`          | `a, b = b, a`                                                | swaps the top of the stack with the 4th last element         ||
| [`93`](https://ethervm.io/#93) | `SWAP4`          | `a, b = b, a`                                                | swaps the top of the stack with the 5th last element         ||
| [`94`](https://ethervm.io/#94) | `SWAP5`          | `a, b = b, a`                                                | swaps the top of the stack with the 6th last element         ||
| [`95`](https://ethervm.io/#95) | `SWAP6`          | `a, b = b, a`                                                | swaps the top of the stack with the 7th last element         ||
| [`96`](https://ethervm.io/#96) | `SWAP7`          | `a, b = b, a`                                                | swaps the top of the stack with the 8th last element         ||
| [`97`](https://ethervm.io/#97) | `SWAP8`          | `a, b = b, a`                                                | swaps the top of the stack with the 9th last element         ||
| [`98`](https://ethervm.io/#98) | `SWAP9`          | `a, b = b, a`                                                | swaps the top of the stack with the 10th last element        ||
| [`99`](https://ethervm.io/#99) | `SWAP10`         | `a, b = b, a`                                                | swaps the top of the stack with the 11th last element        ||
| [`9A`](https://ethervm.io/#9A) | `SWAP11`         | `a, b = b, a`                                                | swaps the top of the stack with the 12th last element        ||
| [`9B`](https://ethervm.io/#9B) | `SWAP12`         | `a, b = b, a`                                                | swaps the top of the stack with the 13th last element        ||
| [`9C`](https://ethervm.io/#9C) | `SWAP13`         | `a, b = b, a`                                                | swaps the top of the stack with the 14th last element        ||
| [`9D`](https://ethervm.io/#9D) | `SWAP14`         | `a, b = b, a`                                                | swaps the top of the stack with the 15th last element        ||
| [`9E`](https://ethervm.io/#9E) | `SWAP15`         | `a, b = b, a`                                                | swaps the top of the stack with the 16th last element        ||
| [`9F`](https://ethervm.io/#9F) | `SWAP16`         | `a, b = b, a`                                                | swaps the top of the stack with the 17th last element        ||
| [`A0`](https://ethervm.io/#A0) | `LOG0`           |                          | fires an event                                               ||
| [`A1`](https://ethervm.io/#A1) | `LOG1`           |  | fires an event                                               ||
| [`A2`](https://ethervm.io/#A2) | `LOG2`           |          | fires an event                                               ||
| [`A3`](https://ethervm.io/#A3) | `LOG3            |                                                              | fires an event                                               ||
| [`A4`](https://ethervm.io/#A4) | `LOG4`           |  | fires an event                                               ||
| [`A5`](https://ethervm.io/#A5) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`A6`](https://ethervm.io/#A6) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`A7`](https://ethervm.io/#A7) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`A8`](https://ethervm.io/#A8) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`A9`](https://ethervm.io/#A9) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`AA`](https://ethervm.io/#AA) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`AB`](https://ethervm.io/#AB) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`AC`](https://ethervm.io/#AC) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`AD`](https://ethervm.io/#AD) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`AE`](https://ethervm.io/#AE) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`AF`](https://ethervm.io/#AF) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`B0`](https://ethervm.io/#B0) | `PUSH`           | `???`                                                        | ???                                                          ||
| [`B1`](https://ethervm.io/#B1) | `DUP`            | `???`                                                        | ???                                                          ||
| [`B2`](https://ethervm.io/#B2) | `SWAP`           | `???`                                                        | ???                                                          ||
| [`B3`](https://ethervm.io/#B3) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`B4`](https://ethervm.io/#B4) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`B5`](https://ethervm.io/#B5) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`B6`](https://ethervm.io/#B6) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`B7`](https://ethervm.io/#B7) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`B8`](https://ethervm.io/#B8) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`B9`](https://ethervm.io/#B9) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`BA`](https://ethervm.io/#BA) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`BB`](https://ethervm.io/#BB) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`BC`](https://ethervm.io/#BC) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`BD`](https://ethervm.io/#BD) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`BE`](https://ethervm.io/#BE) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`BF`](https://ethervm.io/#BF) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`C0`](https://ethervm.io/#C0) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`C1`](https://ethervm.io/#C1) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`C2`](https://ethervm.io/#C2) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`C3`](https://ethervm.io/#C3) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`C4`](https://ethervm.io/#C4) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`C5`](https://ethervm.io/#C5) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`C6`](https://ethervm.io/#C6) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`C7`](https://ethervm.io/#C7) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`C8`](https://ethervm.io/#C8) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`C9`](https://ethervm.io/#C9) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`CA`](https://ethervm.io/#CA) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`CB`](https://ethervm.io/#CB) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`CC`](https://ethervm.io/#CC) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`CD`](https://ethervm.io/#CD) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`CE`](https://ethervm.io/#CE) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`CF`](https://ethervm.io/#CF) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`D0`](https://ethervm.io/#D0) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`D1`](https://ethervm.io/#D1) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`D2`](https://ethervm.io/#D2) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`D3`](https://ethervm.io/#D3) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`D4`](https://ethervm.io/#D4) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`D5`](https://ethervm.io/#D5) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`D6`](https://ethervm.io/#D6) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`D7`](https://ethervm.io/#D7) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`D8`](https://ethervm.io/#D8) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`D9`](https://ethervm.io/#D9) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`DA`](https://ethervm.io/#DA) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`DB`](https://ethervm.io/#DB) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`DC`](https://ethervm.io/#DC) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`DD`](https://ethervm.io/#DD) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`DE`](https://ethervm.io/#DE) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`DF`](https://ethervm.io/#DF) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`E0`](https://ethervm.io/#E0) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`E1`](https://ethervm.io/#E1) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`E2`](https://ethervm.io/#E2) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`E3`](https://ethervm.io/#E3) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`E4`](https://ethervm.io/#E4) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`E5`](https://ethervm.io/#E5) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`E6`](https://ethervm.io/#E6) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`E7`](https://ethervm.io/#E7) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`E8`](https://ethervm.io/#E8) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`E9`](https://ethervm.io/#E9) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`EA`](https://ethervm.io/#EA) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`EB`](https://ethervm.io/#EB) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`EC`](https://ethervm.io/#EC) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`ED`](https://ethervm.io/#ED) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`EE`](https://ethervm.io/#EE) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`EF`](https://ethervm.io/#EF) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`F0`](https://ethervm.io/#F0) | `CREATE`         |                                                              | creates a child contract||
| [`F1`](https://ethervm.io/#F1) | `CALL`           |  | calls a method in another contract                           ||
| [`F2`](https://ethervm.io/#F2) | `CALLCODE`       |   | ???                                                          ||
| [`F3`](https://ethervm.io/#F3) | `RETURN`         |                         | returns from this contract call                              ||
| [`F4`](https://ethervm.io/#F4) | `DELEGATECALL`   |   | calls a method in another contract, using the storage of the current contract ||
| [`F5`](https://ethervm.io/#F5) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`F6`](https://ethervm.io/#F6) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`F7`](https://ethervm.io/#F7) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`F8`](https://ethervm.io/#F8) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`F9`](https://ethervm.io/#F9) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`FA`](https://ethervm.io/#FA) | `STATICCALL`     |  | ???                                                          ||
| [`FB`](https://ethervm.io/#FB) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`FC`](https://ethervm.io/#FC) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`FD`](https://ethervm.io/#FD) | `REVERT`         |                        | reverts with return data                                     ||
| [`FE`](https://ethervm.io/#FE) | *Invalid*        | *-*                                                          | *-*                                                          ||
| [`FF`](https://ethervm.io/#FF) | `SELFDESTRUCT`   | `selfdestruct(address(addr))`                                | destroys the contract and sends all funds to addr.           ||





```
opcodes = {
    0x00: ['STOP', 0, 0, 0], 
    0x01: ['ADD', 2, 1, 3],
    0x02: ['MUL', 2, 1, 5],
    0x03: ['SUB', 2, 1, 3],
    0x04: ['DIV', 2, 1, 5],
    0x05: ['SDIV', 2, 1, 5],
    0x06: ['MOD', 2, 1, 5],
    0x07: ['SMOD', 2, 1, 5],
    0x08: ['ADDMOD', 3, 1, 8],
    0x09: ['MULMOD', 3, 1, 8],
    0x0a: ['EXP', 2, 1, 10],
    0x0b: ['SIGNEXTEND', 2, 1, 5],
    0x10: ['LT', 2, 1, 3],
    0x11: ['GT', 2, 1, 3],
    0x12: ['SLT', 2, 1, 3],
    0x13: ['SGT', 2, 1, 3],
    0x14: ['EQ', 2, 1, 3],
    0x15: ['ISZERO', 1, 1, 3],
    0x16: ['AND', 2, 1, 3],
    0x17: ['OR', 2, 1, 3],
    0x18: ['XOR', 2, 1, 3],
    0x19: ['NOT', 1, 1, 3],
    0x1a: ['BYTE', 2, 1, 3],
    0x20: ['SHA3', 2, 1, 30],
    0x30: ['ADDRESS', 0, 1, 2],
    0x31: ['BALANCE', 1, 1, 20],  # now 400
    0x32: ['ORIGIN', 0, 1, 2],
    0x33: ['CALLER', 0, 1, 2],
    0x34: ['CALLVALUE', 0, 1, 2],
    0x35: ['CALLDATALOAD', 1, 1, 3],
    0x36: ['CALLDATASIZE', 0, 1, 2],
    0x37: ['CALLDATACOPY', 3, 0, 3],
    0x38: ['CODESIZE', 0, 1, 2],
    0x39: ['CODECOPY', 3, 0, 3],
    0x3a: ['GASPRICE', 0, 1, 2],
    0x3b: ['EXTCODESIZE', 1, 1, 20], # now 700
    0x3c: ['EXTCODECOPY', 4, 0, 20], # now 700
    0x3d: ['RETURNDATASIZE', 0, 1, 2],
    0x3e: ['RETURNDATACOPY', 3, 0, 3],
    0x40: ['BLOCKHASH', 1, 1, 20],
    0x41: ['COINBASE', 0, 1, 2],
    0x42: ['TIMESTAMP', 0, 1, 2],
    0x43: ['NUMBER', 0, 1, 2],
    0x44: ['DIFFICULTY', 0, 1, 2],
    0x45: ['GASLIMIT', 0, 1, 2],
    0x50: ['POP', 1, 0, 2],
    0x51: ['MLOAD', 1, 1, 3],
    0x52: ['MSTORE', 2, 0, 3],
    0x53: ['MSTORE8', 2, 0, 3],
    0x54: ['SLOAD', 1, 1, 50],  # 200 now
    # actual cost 5000-20000 depending on circumstance
    0x55: ['SSTORE', 2, 0, 0],
    0x56: ['JUMP', 1, 0, 8],
    0x57: ['JUMPI', 2, 0, 10],
    0x58: ['PC', 0, 1, 2],
    0x59: ['MSIZE', 0, 1, 2],
    0x5a: ['GAS', 0, 1, 2],
    0x5b: ['JUMPDEST', 0, 0, 1],
    0x60: ['PUSH1', 0, 1, 3],
    ......
    0x7f: ['PUSH32', 0, 1, 3],
    0x80: ['DUP1', 1, 2, 3],
    ......
    0x8f: ['DUP32', 16, 17, 3],
    0x90: ['SWAP1', 2, 2, 3],
    ......
    0x9f: ['SWAP32', 17, 17, 3],
    0xa0: ['LOG0', 2, 0, 375],
    0xa1: ['LOG1', 3, 0, 750],
    0xa2: ['LOG2', 4, 0, 1125],
    0xa3: ['LOG3', 5, 0, 1500],
    0xa4: ['LOG4', 6, 0, 1875],
    # 0xe1: ['SLOADBYTES', 3, 0, 50], # to be discontinued
    # 0xe2: ['SSTOREBYTES', 3, 0, 0], # to be discontinued
    # 0xe3: ['SSIZE', 1, 1, 50], # to be discontinued
    0xf0: ['CREATE', 3, 1, 32000],
    0xf1: ['CALL', 7, 1, 40],  # 700 now
    0xf2: ['CALLCODE', 7, 1, 40],  # 700 now
    0xf3: ['RETURN', 2, 0, 0],
    0xf4: ['DELEGATECALL', 6, 1, 40],  # 700 now
    0xf5: ['CALLBLACKBOX', 7, 1, 40],
    0xfa: ['STATICCALL', 6, 1, 40],
    0xfd: ['REVERT', 2, 0, 0],
    0xff: ['SUICIDE', 1, 0, 0],  # 5000 now
}
```