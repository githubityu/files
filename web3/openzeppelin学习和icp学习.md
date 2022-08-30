[TOC]

#### soldity
[ethernaut](https://ethernaut.openzeppelin.com/)
[contracts](https://docs.openzeppelin.com/contracts/4.x/)
[交互](https://docs.openzeppelin.com/contracts/4.x/wizard)
[大佬博客](https://www.pefish.me/)
##### ERC
>ERC20
>ERC721
>ERC155
>Governor


##### 1. settings 属性
>1.1 name
>1.2 symbol
>1.3 premint

##### 2. Features 扩展方法
>2.1 Mintable(mint)
>2.2 Burnable
>2.3 Pausable
>2.4 Permit
>2. 5 Votes
    >2.6 Flash Minting
    >2.7 Snapshots

##### 3. access control
>3.1  Ownable
>3.2  Roles

##### 4. upgradeability
>4.1 Transparent
>4.2  UUPS


##### 5. 步骤
>mkdir learn && cd learn
>npm init -y
>npx truffle init
>npm install --save-dev hardhat
>npx hardhat

###### 编译sol
>truffle compile 仅仅编译编译后修改过的文件
>truffle compile --compile-all 编译所有文件
>npx hardhat compile 用这个编译

###### 安装
>npm install --save-dev @openzeppelin/contracts

###### 交互Hardhat Network内置了本地区块链
>npx hardhat node
>npm install --save-dev @nomiclabs/hardhat-ethers ethers




###### 5.1 部署合约
>npx hardhat run --network localhost scripts/deploy.js
>获取合约对象 ethers.getContractFactory
>部署合约 deployed
>打印合约地址 address

###### 5.1 控制台交互
>npx hardhat console --network localhost
>获取合约对象 ethers.getContractFactory
>挂载到合约地址 attach
>开始交互

###### 5.2 编程方式交互
>npx hardhat run --network localhost ./scripts/index.js


###### 5.3 自动化测试
>npm install --save-dev chai  
>npx hardhat test
>expect

###### 5.4 更复杂 的自动化测试
>npm install --save-dev @openzeppelin/test-helpers
>npx truffle test
> expectEvent
> expectRevert

>npx mnemonics
>npx hardhat console --network rinkeby
>npm install --save-dev @openzeppelin/hardhat-upgrades
>[网址](https://docs.openzeppelin.com/learn/preparing-for-mainnet)


#####  etherscan插件
>npm install --save-dev @nomiclabs/hardhat-etherscan
>npx hardhat verify --network mainnet DEPLOYED_CONTRACT_ADDRESS "Constructor argument 1"


#### truffle
>npm install --save-dev truffle
>npm install --save-dev ganache-cli
>npx ganache-cli --deterministic
>npx truffle console --network development
>npx truffle exec --network development ./scripts/index.js
>npm install --save-dev @truffle/hdwallet-provider
>npm install truffle-flattener -g
>truffle-flattener <solidity-files>


##### hardhat
>npm install --save-dev hardhat
>npx hardhat
>npx hardhat compile
>npx hardhat test
>npx hardhat run scripts/sample-script.js
>npx hardhat node
>npx hardhat run scripts/sample-script.js --network localhost
>先创建full目录 然后再执行
>npx hardhat flatten contracts/land/LANDRegistry.sol > full/LANDRegistry.sol




##### 其他学习资料
>[Solidity](https://www.youtube.com/watch?v=M576WGiDBdQ)
>[比赛项目](https://devpost.com/)



#### ICP
>[doc](https://internetcomputer.org/)
>[developer-docs](https://internetcomputer.org/docs/current/developer-docs/ic-overview)
>[icp](https://github.com/githubityu/ic)


##### 命令行代理
```ts
$env:http_proxy="http://127.0.0.1:1080"
$env:https_proxy="http://127.0.0.1:1080"
```