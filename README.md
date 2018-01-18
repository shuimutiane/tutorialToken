# tutorialToken

随着最近两年基于以太坊智能合约基础设施和相关工具的迅猛发展，开发出具有工业水准的ERC20代币的技术门槛也大大降低。本文将介绍如何快速的开发您自己的ERC20代币。

### 1. 安装Node.js，

安装文件和各平台具体安装方法请见https://nodejs.org/zh-cn/download/。 由于我们后面使用的开发工具truffle以及本地测试区块链ganache都是基于javascript 开发

### 2. 安装truffle,truffle

正如其网站所宣传的一样，它是智能合约开发的瑞士军刀。就像maven大大简化的Java程序的编译和部署，truffle也使得智能合约的开发和部署更加傻瓜化。

npm install -g truffle

### 3. 安装ganache. 

ganache是一个专门为开发智能合约定制的区块链本地节点工具。大家可以从 http://truffleframework.com/ganache/ 下载对应平台的安装包并安装。它和以太坊原本节点软件(geth,parity)相比，具有以下优点，

  1> 安装方便，省去繁琐的配置，点击几下鼠标便可完成。

  2> 省系统资源，他不会没完没了的挖矿，只是在有交易需要打包的时候才打包。

  3> 有图形界面，从图形界面可以方便和直观的查看块，交易，账户等信息。

### 4. 启动ganache

### 5. 打开一个命令行终端

输入如下命令：

mkdir TutorialToken

cd TutorialToken

truffle unbox tutorialtoken

npm install zeppelin-solidity

稍微解释一下上面的命令，第一和第二行创建目录TutorialToken并进入该目录。第三行使用truffle的unbox命令使用tutorialtoken这个项目作为范例，创建ERC20代币智能合约的骨架。第四行是安装智能合约的第三方库zeppelin-solidity, zeppelin-solidity之于ERC20代币智能合约就类似spring boot之于JAVA web后端开发，是一个事实上的业界标准库。

### 6. 使用诸如VSCode, Atom等类似的编辑器打开上面的目录

如果你是前端开发人员，你应该发现目录结构和普通的JavaScript前端项目非常相似，唯一不同的就是多了contracts和migrations这两个目录。

6.1 在contracts目录下创建一个新文件TutorialToken.sol, 内容如下：


```
pragma solidity ^0.4.17;

import 'zeppelin-solidity/contracts/token/StandardToken.sol';

contract TutorialToken is StandardToken {

string public name = "TutorialToken";

string public symbol = "HT";

uint8 public decimals = 2;

uint public INITIAL_SUPPLY = 888888;

function TutorialToken() public {

totalSupply = INITIAL_SUPPLY;

balances[msg.sender] = INITIAL_SUPPLY;

}

}

```

6.2 在migrations目录下兴建2_deploy_contracts.js,内容如下：

```
var TutorialToken = artifacts.require("TutorialToken");

module.exports = function(deployer) {

deployer.deploy(TutorialToken);

}

```

6.3 编译智能合约

truffle compile

6.4 部署智能合约

truffle migrate

6.5 修改./src/js/app.js 第16行，将

```
App.web3Provider = new Web3.providers.HttpProvider('http://127.0.0.1:9545');
```
改成

```
App.web3Provider = new Web3.providers.HttpProvider('http://127.0.0.1:7545');
```

6.6 npm install

6.7 npm run dev

6.8 用firefox或者chrome打开http://localhost:3000, 如果你看到如下画面，恭喜您，你的ERC20代币TutorialToken已经大功搞成。

6.9 你可以在 address编辑框输入0xf17f52151EbEF6C7334FAD080c5704D77216b732， Amount编辑框输入100，那么你的balance将会变成888788. 说明转账功能也是OK的。

按照文中所述生成的项目大家也可以直接从https://github.com/bubble501/tutorialToken.git 下载。

本文的主要目的是通过ERC20代币的开发现大家展示以太坊的智能合约开发入门非常简单。 虽然目前看来，基于区块链的智能合约应用还比较幼稚和单薄，但是代币发行和虚拟猫已经让其牛刀小试，并且反响不俗。笔者认为区块链和智能合约在未来五到十年一定会大放异彩，渗透到普通人的平常生活。作为开发或者立志成为开发人员的你，一定不要错过区块链和智能合约这个风口，现在开始投入学习就像两千年初加入腾讯，享受技术的红利。

转自：https://www.toutiao.com/a6506298560676364804/
