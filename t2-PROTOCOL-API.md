# DOCUMENTATIONS
## What is t2 ?
# MAJOR CONCEPTS

# MAJOR USE CASES

# t2 API
## Introduction
Welcome to the API docs for T2 World. We aim to highlight all the endpoints which are exposed on the public API and explain how to use them and what they return.
The protocols have two categories of APIs: one with public accessibility, one with logged in user as authentication in header.
These two set of APIs does NOT represents exactly the counter part of Blockchain APIs for Read & Write.
The sets of API requires user token in header, representing any call that needs to identify the caller identity. This does not imply the API has the capability to perform a WRITE onto the blockchain.

### Public APIs
You call the following APIs without proceeding login call
| ROOT        | URL                                                          | METHOD | PARAMETERS |
| ----------- | ------------------------------------------------------------ | ------ | ---------- |
| World       | /v1/world/stats                                              | GET    |            |
|             | /v1/world/stats-events                                       | GET    |            |
|             | /v1/world/subscribe                                          | PUT    |            |
|             | /v1/world/subscribers                                        | GET    |            |
|             | /v1/world/users                                              | GET    |            |
| Contents    | /v1/contents/{contentId}                                     | GET    |            |
|             | /v1/contents/{contentId}/pages                               | GET    |            |
|             | /v1/contents/{contentId}/pages/{pageId}/events               | GET    |            |
| Items       | /v1/items/search                                             | GET    |            |
|             | /v1/items/{itemId}                                           | GET    |            |
|             | /v1/items/{itemId}/versions                                  | GET    |            |
| Users       | /v1/users/{userId}                                           | GET    |            |
|             | /v1/users/{userId}/stats-events                              | GET    |            |
|             | /v1/users/{userId}/events                                    | GET    |            |
|             | /v1/users/{userId}/items/{itemId}/contents/{contentId}/pages/{pageId}/stats | GET    |            |
| Territories | /v1/territories/search                                       | GET    |            |
|             | /v1/territories/{territoryId}                                | GET    |            |
|             | /v1/territories/{territoryId}/spaces                         | GET    |            |
|             | /v1/territories/{territoryId}/spaces/{spaceId}               | GET    |            |
|             | /v1/territories/{territoryId}/citizens/search                | GET    |            |

### Authenticated APIs
### Login
| ROOT | URL            | METHOD | PARAMETERS                                               | RETURNS             |
| ---- | -------------- | ------ | -------------------------------------------------------- | ------------------- |
| Auth | /v1/auth/login | POST   | {"UserId": "0xe120a1c90a813796425a2e9ef36f692f92d17073"} | {"Token":"abcdefg"} |

### Authenticated APIs
The authenticated APIs requires header being set to following:

**Headers**

| KEY           | VALUE                                        |
| ------------- | -------------------------------------------- |
| Authorization | JWT <Token value returned in /v1/auth/login> |
| Content-Type  | application/json                             |



### API Calls

| ROOT        | URL                                                          | METHOD | PARAMETERS |
| ----------- | ------------------------------------------------------------ | ------ | ---------- |
| Users       | /v1/users/my-passport                                        | GET    |            |
|             | /v1/users/my-passport                                        | PATCH  |            |
|             | /v1/users/my-footsteps                                       | GET    |            |
|             | /v1/users/my-items                                           | GET    |            |
|             | /v1/users/my-webpaper                                        | GET    |            |
|             | /v1/users/{userId}/items/{itemId}/contents/{contentId}/pages/{pageId}/events/start | PUT    |            |
|             | /v1/users/{userId}/items/{itemId}/contents/{contentId}/pages/{pageId}/events/stop | PUT    |            |
|             | /v1/users/{userId}/initialize                                | PUT    |            |
|             | /v1/users/{userId}/items/{itemId}/contents/{contentId}/pages/{pageId}/sync-stats | PUT    |            |
|             | /v1/users/{userId}/sync-stats                                | PUT    |            |
| Contents    | /v1/contents                                                 | POST   |            |
|             | /v1/contents/import                                          | PUT    |            |
|             | /v1/contents/upload                                          | POST   |            |
| Items       | /v1/items                                                    | POST   |            |
|             | /v1/items/versions                                           | POST   |            |
|             | /v1/items/versions/{versionId}/review-action                 | PUT    |            |
| Territories | /v1/territories                                              | POST   |            |



## API links

[api.t2.world](https://hvc0cu76ch.execute-api.ap-northeast-1.amazonaws.com/Prod/swagger/index.html)

# t2 Smart Contracts
## Introduction
There are six contracts for T2 World. They are TXT Contract, Passport Contract, Governance Contract, Territory Contract, Item Contract and T2 World Contract. The first three contract were deployed for the tokens(TXT, Passport, Governanace) in T2 World. The Territory Contract is used to record  the details of the territories in T2 World. the Item Contract is used to record the details of the items in T2 World and the main business logic. The T2 World contract is a platform for managing other contracts.

The contracts have two categories of methods: one is for the users, one is called by T2World.

The methods in T2World are divided into public methods and contract methods. public method can be called by users for daily operations in T2 World. contract methods are the methods of different module that must be called by the platform management contract.

T2 World 的methods 分为 public methods 和 contract methods. public methods 是可以由用户调用进行日常操作的方法. contract methods 是必须由平台管理合约进行调用的各个不同模块合约的方法.

## T2World Public Methods

The T2World Public Methods are for users.

T2World is the platform contract of t2 world which contains all public methods.  users can use the methods of platform contract to participate in the content sharing and POA (proof of attention) journey of t2 world. for the DAO management, we let the platform contract calls the module contracts to manage various information and activities in t2 world.

T2World是T2 World的平台合约. 包含了所有的公共方法. 用户使用该平台合约的方法参与到T2World的内容分享和POA之旅中. 为了DAO的管理, 由该平台合约调用其它各个模块对应的合约, 来实现T2 World中的各种信息和活动. 

| CONTRACT | METHOD               | INTRODUCTION                                            | PARAMETERS                                                   | RETURNS                                                      |
| -------- | -------------------- | ------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| T2World  | createPassport       | create a new passport                                   | title: title of the new passport. <br />detail: detail of the new passport. <br />reputation: reputation of the new passport. |                                                              |
|          | getPassports         | get a certain passport                                  |                                                              | a list of all passports.                                     |
|          | createTerritory      | create a new territory                                  | name: name of the new territory.                             |                                                              |
|          | getTerritories       | get a list of all territories                           |                                                              | list of all territories.                                     |
|          | createItem           | create a new item                                       | territory: ID of a certain territory.<br />title: title of the new item.<br />hh: hash key of the new content. |                                                              |
|          | updateItem           | update a certain item                                   | id: ID of a certain item.<br />title: new title of the item.<br />hh: new content hash key of the item. |                                                              |
|          | getItems             | get a list of all items                                 |                                                              | a list of all items.                                         |
|          | getItemsByTerritory  | get a list of items which after the given terrtiroy     | territory: ID of a certain territory.                        | a list containing all items under the territory.             |
|          | votingItem           | voting to a certain item                                | itemId: ID of a certain item.<br />votingToken token number of votes. |                                                              |
|          | getVotingInfo        | get the voting information of all items                 |                                                              | a list containing all item voting information.               |
|          | stakeItem            | stake to a certain item                                 | itemId: ID of a certain item.<br />stakeToken: token number of the stake. |                                                              |
|          | getStakeInfo         | get stake information of all items                      |                                                              | a list containing all item stake information.                |
|          | prepareReceiveTokens | calculate the tokens than every stakeholders should get |                                                              |                                                              |
|          | getReceiveInfo       | get the receive information of all stakeholders         |                                                              | a list containing the receive information of all stakeholders. |
|          | withdraw             | withdraw the token to the caller                        |                                                              |                                                              |



## Contracts Methods

The contracts methods will be called by T2World Contract. Most of them need a sender parameter.

These contracts are used as token contracts and data interaction contracts. it contains five modules: Passport, TXT, Governance, Territory and Item. the first three contracts are token contracts in t2 world, and can do  various operations to tokens in t2 world. Territory and Item are two data contracts which is used to record data information of territory and item in t2 world.

As the contracts are called by T2World, not by users. the contract methods which had changed contract data all need a address parameter which send from T2World. 

这些合约做为token合约和数据交互合约来使用. 包含了五个模块: Passport, TXT, Governance, Territory, Item.

Passport, TXT, Governance是三个Token合约, 分别为T2 World中的三个token账本合约, 可以进行对应token的各种操作.

 Territory, Item是两个数据合约. 分别用来记录T2 World中Territory和Item的数据信息.

由于合约要被T2World调用, 合约调用者是T2World, 需要接受T2World传递过来的用户wallet address. 跟用户相关的方法都需要个sender参数传递用户wallet address.

| CONTRACT | METHOD         | INTRODUCTION           | PARAMETERS | RETURNS |
| -------- | -------------- | ---------------------- | ---------- | ---------- |
| Passport | createPassport | create a new passport  | sender: wallet address of the creator.<br />title: title of the new passport. <br />detail: detail of the new passport. <br />reputation: reputation of the new passport. |  |
|  | getPassports   | get a certain passport |            | a list of all passports. |
| Territory | createTerritory  | create a new territory        |sender: wallet address of the creator. <br />name: name of the new territory.||
|  | hasTerritory     | if there has a certain territory with the given ID |id: ID of a certain territory.|a bool value(true or false).|
|  | getTerritory     | get a certain territory                            |id: ID of a certain territory.|details of a territory.|
|  |getTerritoryList | get a list of all territories                      ||list of all territories.|
| Item | createItem             | create a new item              |territory: ID of a certain territory.<br />title: title of the new item.<br />author: wallet address of the creator.<br />hh: hash key of the new content.||
| | updateItem             | update a certain item                                   |id: ID of a certain item.<br />title: new title of the item.<br />hh: new content hash key of the item.||
| | getItem                | get a certain item                                      |id: ID of a certain item.|details of the item.|
| | getItemList            | get a list of all items                                 ||a list of all items.|
| | getItemListByTerritory | get a list of items which after the given terrtiroy     |territory: ID of a certain territory.|a list containing all items under the territory.|
| | votingItem             | voting to a certain item                                |sender: wallet address of the user.<br />itemId: ID of a certain item.<br />votingToken token number of votes.||
| | getVotingInfo          | get the voting information of all items                 ||a list containing all item voting information.|
| | stakeItem              | stake to a certain item                                 |sender: wallet address of the user.<br />itemId: ID of a certain item.<br />stakeToken: token number of the stake.||
| | getStakeInfo           | get stake information of all items                      ||a list containing all item stake information.|
| | prepareReceiveTokens   | calculate the tokens than every stakeholders should get |||
| | getReceiveInfo         | get the receive information of all stakeholders         ||a list containing the receive information of all stakeholders.|
| | withdraw               | withdraw the token to the caller                        |sender: wallet address of a user.||



## TXT Contract

This contract is for the TXT token. It's a token of ERC20 protocol.

TXT Contract is an account contract used to record TXT token which use ERC20 protocol. T2World call this contract  to minting and trade the TXT token. users can trade txt by it.

TXT 合约是用来记录TXT token的账本合约，采用了ERC20协议. T2 World通过调用TXT合约，进行TXT token的minting和交易. 用户之间可以进行TXT token的交易.

## Governance Contract
This contract is for governance token. It's a token of ERC20 protocol.

Governance Contract is an account contract used to record Governance token which use ERC20 protocol. T2World call this contract  to minting and trade the TXT token. every territory (community) has an unique Governance Token. users can trade governance by it.

Governance合约是用来记录 Governance token的账本合约, 采用了ERC20协议. T2 World通过调用Governance合约来进行Governance token的minting和交易. 每个territory（community）拥有一个不同的Governance token. 用户之间可以进行Governance token的交易.

## Passport Contract
This contract is for passport token. It's a token of ERC721 protocol.

Passport Contract is an account contract used to record Passport NFT which use ERC721 protocol. T2World call this contract to minting the Passport token.

Passport合约是用来记录 passport nft 的账本合约, 采用了ERC721协议. T2 World通过调用Passport合约来进行badge的记录.

| METHOD | INTRODUCTION |
|-------- |---|
| createPassport | create a new passport |
| getPassports| get a certain passport |

### createPassport

**function head**

    function createPassport(address sender, string memory title, string memory detail, uint reputation) public;

* parameters 
    * sender: wallet address of the creator.
    * title: title of the new passport.
    * detail: detail of the new passport.
    * reputation: reputation of the new passport.

**description**

this method add a new passport with the given parameters.

该方法创建一个创建者wallet address 为sender的新的passport NFT. 包含title, detail, reputation 等信息.

由于是被T2World调用, sender地址是T2World的地址, 需要传递用户的wallet address.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

### getPassports

**function head**

    function getPassports() view public returns(PassportDetail[] memory);

* returns
    * a list of all passports.

**description**

this method returns a list of all passports.

通过该方法可以获取到包含所有passport的列表.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

## Territory Contract
This contract is for territories in T2 World.

Territory Contract is an data contract used to record territory data. T2World call this contract to create territory and other operations about territory.

Territory 合约是用来记录territory数据的数据合约. T2 World通过调用Territory合约来进行Territory的创建和相关操作.

| METHOD | INTRODUCTION |
|-------- |---|
| createTerritory | create a new territory |
| hasTerritory | if there has a certain territory with the given ID |
| getTerritory | get a certain territory |
| getTerritoryList | get a list of all territories |

### createTerritory

**function head**

    function createTerritory(address sender, string memory name) public returns(bool);

* prarameters
    * sender: wallet address of the creator.
    * name: name of the new territory.

**description**

this method add a new territory with the given parameters.

该方法创建一个创建者为sender的Territory, 包含 name 信息.

由于是被T2World调用, sender地址是T2World的地址, 需要传递用户的wallet address.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

### hasTerrtory

**function head**
        
    function hasTerrtory(uint id) view public returns(bool); 

* parameters 
    * id: ID of a certain territory.

* returns
    * a bool value(true or false).

**decription**

this method returns a bool value whether there is a territory of the given ID.

该方法判断是否已经存在为该ID的territory, 由于item需要在一个存在的territory下面.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

### getTerritory

**function head**
    
    function getTerritory(uint id) view public returns(Territory memory);

* parameters
    * id: ID of a certain territory.

* returns
    * details of a territory.

**description**

this method returns the details of a territory of the given ID.

根据id获取对应territory的信息.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

### getTerritoryList

**function head**

    function getTerritoryList() view public returns(Territory[] memory);

* returns
    * list of all territories.

**description**

this method returns a list of all territories.

该方法返回一个包含所有territory的列表, 是否需要添加关于territory的筛选, 如name, 创建者.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

## Item Contract
This contract is for items in T2 World.

Item Contract is an data contract used to record territory data. T2World call this contract to create item and other operations about item.

Item合约是用来记录item数据的数据合约. T2 World通过调用Item合约来进行item的创建、修改和其他相关操作.

| METHOD | INTRODUCTION |
|-------- |---|
| createItem | create a new item |
| updateItem | update a certain item |
| getItem | get a certain item |
| getItemList | get a list of all items |
| getItemListByTerritory | get a list of items which after the given terrtiroy |
| votingItem | voting to a certain item |
| getVotingInfo | get the voting information of all items |
| stakeItem | stake to a certain item |
| getStakeInfo | get stake information of all items |
| prepareReceiveTokens | calculate the tokens than every stakeholders should get |
| getReceiveInfo | get the receive information of all stakeholders |
| withdraw | withdraw the token to the caller |

### createItem

**function head**

     function createItem(uint256 territory, string memory title, address author, string memory hh) public;

* parameters
    * territory: ID of a certain territory.
    * title: title of the new item.
    * author: wallet address of the creator.
    * hh: hash key of the new content.

**description**

this method add a new item with the given parameters.

该方法创建一个创建者为sender的Item, 包含title, hh(把内容上传到arweave后的hash key)信息.

由于是被T2World调用, sender地址是T2World的地址, 需要传递用户的wallet address.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

### updateItem

**function head**

    function updateItem(uint256 id, string memory title, string memory hh) public;

* parameters
    * id: ID of a certain item.
    * title: new title of the item.
    * hh: new content hash key of the item. 

**description**

this method update the title and content hash key of the item with the given ID.

该方法更新一个存在的Item的title和hh(把内容上传到arweave后的hash key)信息.

hh部分会添加一个新的version记录.

### getItem

**function head**

   function getItem(uint256 id) view public returns(Item memory);

* parameters
    * id: ID of a certain item.

* returns
    * details of the item.

**description**

this method returns details of a certain item with the given ID.

根据id获取对应的item信息.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

### getItemList

**function head**

    function getItemList() view public returns(Item[] memory);

* returns
    * a list of all items.

**description**

this method returns a list of all items.

获取一个包含所有item的列表.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

### getItemListByTerritory

**function head**

    function getItemListByTerritory(uint territory) view public returns(Item[] memory);

* parameters
    * territory: ID of a certain territory.

* returns
    * a list containing all items under the territory.

**description**

this method returns a list of all items under the given territory.

获取一个包含确定的territory下面的所有item的列表.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

### votingItem

**function head**

    function votingItem(address sender, uint256 itemId, uint256 votingToken) public;

* parameters
    * sender: wallet address of the user.
    * itemId: ID of a certain item.
    * votingToken token number of votes.

**description**

this method votes on a given item according to the specified number of votes.

用户给一个存在的item进行投票，并可以指定具体投票数量.

由于是被T2World调用, sender地址是T2World的地址, 需要传递用户的wallet address.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

### getVotingInfo

**function head**

    function getVotingInfo() view public returns(ItemVotingInfo[] memory) ;

* returns
    * a list containing all item voting information.

**description**

this method returns a list containing all item voting information.

通过该方法可以获取到所有item的voting信息, 每个item的voting数量.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

### stakeItem

**function head**

    function stakeItem(address sender, uint256 itemId, uint256 stakeToken) public;

* parameters
    * sender: wallet address of the user.
    * itemId: ID of a certain item.
    * stakeToken: token number of the stake.

**description**

this method stake to a item with the given ID.

用户给一个存在的item进行投资，并可以指定具体投资数量.

由于是被T2World调用, sender地址是T2World的地址, 需要传递用户的wallet address.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

### getStakeInfo

**function head**

    function getStakeInfo() view public returns(ItemStakeInfo[] memory);

* returns
    * a list containing all item stake information.

**description**

this method return a list containing all item stake information.

通过该方法可以获取到所有投资者的投资信息, 投资的item数量和总投资token数量.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

### prepareReceiveTokens

**function head**

    function prepareReceiveTokens() public;

**description**

this method calculate the tokens that every stakeholders should get.

该方法会计算所有的投资者当期可以获取到的revenue, 并进行记录. 并没有发送.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址. 

### getReceiveInfo

**function head**

    function getReceiveInfo() view public returns(ReceiveInfo[] memory);

* returns
    * a list containing the receive information of all stakeholders.

**description**

get the receive information of all the stakeholder.

该方法返回所有投资者的投资信息, 已经收到的revenue和可以提取的revenue.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.        

### withdraw

**function head**

    function withdraw(address sender) public;

* parameters
    * sender: wallet address of a user.

**description**

this method withdraw the token to the sender(user).

用户通过该方法提取被记录下来应该收取到的revenue, 一次性提取完.

由于是被T2World调用, sender地址是T2World的地址, 需要传递用户的wallet address.

需要验证该方法的调用地址是否为T2World. 可以由合约创建者设置T2World合约的地址.

## T2World Contract

The T2 World contract is a platform for managing other contracts.

T2 World合约是平台管理合约. 其他合约由该合约调用进行各种操作. 用户可以调用该合约进行T2 World范围内的活动.

| METHOD               | INTRODUCTION                                            |
| -------------------- | ------------------------------------------------------- |
| createPassport       | create a new passport                                   |
| getPassports         | get a certain passport                                  |
| createTerritory      | create a new territory                                  |
| getTerritories       | get a list of all territories                           |
| createItem           | create a new item                                       |
| updateItem           | update a certain item                                   |
| getItems             | get a list of all items                                 |
| getItemsByTerritory  | get a list of items which after the given terrtiroy     |
| votingItem           | voting to a certain item                                |
| getVotingInfo        | get the voting information of all items                 |
| stakeItem            | stake to a certain item                                 |
| getStakeInfo         | get stake information of all items                      |
| prepareReceiveTokens | calculate the tokens than every stakeholders should get |
| getReceiveInfo       | get the receive information of all stakeholders         |
| withdraw             | withdraw the token to the caller                        |

### createPassport

**function head**

    function createPassport(string memory title, string memory detail, uint reputation) public;

* parameters 
  * title: title of the new passport.
  * detail: detail of the new passport.
  * reputation: reputation of the new passport.

**description**

this method add a new passport with the given parameters.

该方法创建一个创建者为方法调用者wallet address的新passport NFT. 包含title, detail, reputation 等信息.

### getPassports

**function head**

    function getPassports() view public returns(PassportDetail[] memory);

* returns
  * a list of all passports.

**description**

this method returns a list of all passports.

通过该方法可以获取到包含所有passport的列表.

### createTerritory

**function head**

    function createTerritory(string memory name) public returns(bool);

* parameters
  * name: name of the new territory.

**description**

this method add a new territory with the given parameters.

该方法创建一个创建者为sender的Territory, 包含 name 信息.

### getTerritories

**function head**

    function getTerritories() view public returns(Territory[] memory);

* returns
  * list of all territories.

**description**

this method returns a list of all territories.

该方法返回一个包含所有territory的列表, 是否需要添加关于territory的筛选, 如name, 创建者.

### createItem

**function head**

     function createItem(uint256 territory, string memory title, string memory hh) public;

* parameters
  * territory: ID of a certain territory.
  * title: title of the new item.
  * hh: hash key of the new content.

**description**

this method add a new item with the given parameters.

### updateItem

**function head**

    function updateItem(uint256 id, string memory title, string memory hh) public;

* parameters
  * id: ID of a certain item.
  * title: new title of the item.
  * hh: new content hash key of the item. 

**description**

this method update the title and content hash key of the item with the given ID.

### getItems

**function head**

    function getItems() view public returns(Item[] memory);

* returns
  * a list of all items.

**description**

this method returns a list of all items.

获取一个包含所有item的列表.

### getItemsByTerritory

**function head**

    function getItemsByTerritory(uint256 territory) view public returns(Item[] memory);

* parameters
  * territory: ID of a certain territory.

* returns
  * a list containing all items under the territory.

**description**

this method returns a list of all items under the given territory.

获取一个包含确定的territory下面的所有item的列表.

### votingItem

**function head**

    function votingItem(uint256 itemId, uint256 votingToken) public;

* parameters
  * itemId: ID of a certain item.
  * votingToken token number of votes.

**description**

this method votes on a given item according to the specified number of votes.

用户给一个存在的item进行投票，并可以指定具体投票数量.

### getVotingInfo

**function head**

    function getVotingInfo() view public returns(ItemVotingInfo[] memory) ;

* returns
  * a list containing all item voting information.

**description**

this method returns a list containing all item voting information.

通过该方法可以获取到所有item的voting信息, 每个item的voting数量.

### stakeItem

**function head**

    function stakeItem(uint256 itemId, uint256 stakeToken) public;

* parameters
  * itemId: ID of a certain item.
  * stakeToken: token number of the stake.

**description**

this method stake to a item with the given ID.

用户给一个存在的item进行投资，并可以指定具体投资数量.

### getStakeInfo

**function head**

    function getStakeInfo() view public returns(ItemStakeInfo[] memory);

* returns
  * a list containing all item stake information.

**description**

this method return a list containing all item stake information.

通过该方法可以获取到所有投资者的投资信息, 投资的item数量和总投资token数量.

### prepareReceiveTokens

**function head**

    function prepareReceiveTokens() public;

**description**

this method calculate the tokens that every stakeholders should get.

该方法会计算所有的投资者当期可以获取到的revenue, 并进行记录. 并没有发送.

### getReceiveInfo

**function head**

    function getReceiveInfo() view public returns(ReceiveInfo[] memory);

* returns
  * a list containing the receive information of all stakeholders.

**description**

get the receive information of all the stakeholder.

该方法返回所有投资者的投资信息, 已经收到的revenue和可以提取的revenue.        

### withdraw

**function head**

    function withdraw() public;

**description**

this method withdraw the token to the sender(user).

用户通过该方法提取被记录下来应该收取到的revenue, 一次性提取完.33