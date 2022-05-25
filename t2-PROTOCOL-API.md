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


## T2World Public Methods

The T2World Public Methods are for users.

T2World is the platform contract of t2 world which contains all public methods.  users can use the methods of platform contract to participate in the content sharing and POA (proof of attention) journey of t2 world. for the DAO management, we let the platform contract calls the module contracts to manage various information and activities in t2 world.


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
|          | getUserProfile       | get user profile information of the caller              |                                                              | user profile details                                         |
|          | setUserEmail         | set email of the caller                                 | email: a email string                                        |                                                              |



## Contracts Methods

The contracts methods will be called by T2World Contract. Most of them need a sender parameter.

These contracts are used as token contracts and data interaction contracts. it contains five modules: Passport, TXT, Governance, Territory and Item. the first three contracts are token contracts in t2 world, and can do  various operations to tokens in t2 world. Territory and Item are two data contracts which is used to record data information of territory and item in t2 world.

As the contracts are called by T2World, not by users. the contract methods which had changed contract data all need a address parameter which send from T2World. 



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
| User | setT2World | set the T2World Contract address in UserContract |t2world: address of T2World Contract.||
|  | getT2World | get the T2World Contract address that had been set. ||address of T2World Contract that had been set.|
|  | getUserProfile | get user profile details of the wallet |wallet: wallet address of t2world caller.|user profile details.|
|  | setUserEmail | set email of the wallet |wallet: address of t2world caller.<br />email: email of t2world caller that will be set.||



## TXT Contract

This contract is for the TXT token. It's a token of ERC20 protocol.

TXT Contract is an account contract used to record TXT token which use ERC20 protocol. T2World call this contract  to minting and trade the TXT token. users can trade txt by it.



## Governance Contract
This contract is for governance token. It's a token of ERC20 protocol.

Governance Contract is an account contract used to record Governance token which use ERC20 protocol. T2World call this contract  to minting and trade the TXT token. every territory (community) has an unique Governance Token. users can trade governance by it.



## Passport Contract
This contract is for passport token. It's a token of ERC721 protocol.

Passport Contract is an account contract used to record Passport NFT which use ERC721 protocol. T2World call this contract to minting the Passport token.

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

This method add a new passport NFT for sender(wallet address of creator). contains sender, title, detail, and reputation.

As the contract is called by T2World, the method need a sender(wallet address of creator) parameter. and need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.

### getPassports

**function head**

    function getPassports() view public returns(PassportDetail[] memory);

* returns
    * a list of all passports.

**description**

This method returns a list of all passports.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



## Territory Contract
This contract is for territories in T2 World.

Territory Contract is an data contract used to record territory data. T2World call this contract to create territory and other operations about territory.

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

This method add a new territory for sender(wallet address of creator). contains sender, name.

As the contract is called by T2World, the method need a sender(wallet address of creator) parameter. and need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### hasTerrtory

**function head**
        

    function hasTerrtory(uint id) view public returns(bool); 

* parameters 
    * id: ID of a certain territory.

* returns
    * a boolean value(true or false).

**decription**

This method returns a boolean value whether territory with this ID already exists, since item needs to be under an existing territory.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getTerritory

**function head**
    
    function getTerritory(uint id) view public returns(Territory memory);

* parameters
    * id: ID of a certain territory.

* returns
    * details of a territory.

**description**

This method returns details of a territory with the given ID.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getTerritoryList

**function head**

    function getTerritoryList() view public returns(Territory[] memory);

* returns
    * list of all territories.

**description**

This method returns  a list of all territories.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.

PS: if there need add some filters. such as name, creator and so on.



## Item Contract
This contract is for items in T2 World.

Item Contract is an data contract used to record territory data. T2World call this contract to create item and other operations about item.

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

This method add a new item for sender(wallet address of creator). contains territory, title, author and hh(hash key after uploading the content to arweave).

As the contract is called by T2World, the method need a sender(wallet address of creator) parameter. and need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### updateItem

**function head**

    function updateItem(uint256 id, string memory title, string memory hh) public;

* parameters
    * id: ID of a certain item.
    * title: new title of the item.
    * hh: new content hash key of the item. 

**description**

This method update the title and hh(hash key after uploading content to areave) of an existing item. a new version of hh is added to the item. contains id, title, and hh(hash key after uploading content to areave).

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.

PS: if there need to verify that the sender is creator of the item.



### getItem

**function head**

   function getItem(uint256 id) view public returns(Item memory);

* parameters
    * id: ID of a certain item.

* returns
    * details of the item.

**description**

This method returns details of a certain item with the given ID.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getItemList

**function head**

    function getItemList() view public returns(Item[] memory);

* returns
    * a list of all items.

**description**

This method returns a list of all items.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getItemListByTerritory

**function head**

    function getItemListByTerritory(uint territory) view public returns(Item[] memory);

* parameters
    * territory: ID of a certain territory.

* returns
    * a list containing all items under the territory.

**description**

This method returns a list of all items under the given territory.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### votingItem

**function head**

    function votingItem(address sender, uint256 itemId, uint256 votingToken) public;

* parameters
    * sender: wallet address of the user.
    * itemId: ID of a certain item.
    * votingToken token number of votes.

**description**

This method votes on an existing item and can specify the number of votes. contains sender, itemId and votingToken.

As the contract is called by T2World, the method need a sender(wallet address of creator) parameter. and need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getVotingInfo

**function head**

    function getVotingInfo() view public returns(ItemVotingInfo[] memory) ;

* returns
    * a list containing all item voting information.

**description**

This method returns voting information of all items and the number of voting for each item.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### stakeItem

**function head**

    function stakeItem(address sender, uint256 itemId, uint256 stakeToken) public;

* parameters
    * sender: wallet address of the user.
    * itemId: ID of a certain item.
    * stakeToken: token number of the stake.

**description**

This method invests in an existing item and can specify the amount of investment. contains sender, itemId and stakeToken.

As the contract is called by T2World, the method need a sender(wallet address of creator) parameter. and need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getStakeInfo

**function head**

    function getStakeInfo() view public returns(ItemStakeInfo[] memory);

* returns
    * a list containing all item stake information.

**description**

This method returns investment information of all items. contains the total number of tokens invested in each item.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### prepareReceiveTokens

**function head**

    function prepareReceiveTokens() public;

**description**

This method calculate and record the revenue that all investors can get in the current period. the revenue hasn't been sent.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getReceiveInfo

**function head**

    function getReceiveInfo() view public returns(ReceiveInfo[] memory);

* returns
    * a list containing the receive information of all stakeholders.

**description**

This method returns investment information of all stakeholders. contains the revenue that has been received and revenue that can be extracted.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### withdraw

**function head**

    function withdraw(address sender) public;

* parameters
    * sender: wallet address of a user.

**description**

This method allows the sender to extract the recorded revenue that should be collected at one time. contains sender.

As the contract is called by T2World, the method need a sender(wallet address of creator) parameter. and need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract

## UserContract

This contract is for users in T2 World.

Item Contract is an data contract used to record user data. T2World call this contract to get user profile and other operations about user.

| METHOD         | INTRODUCTION                                        |
| -------------- | --------------------------------------------------- |
| setT2World     | set the T2World Contract address in UserContract.   |
| getT2World     | get the T2World Contract address that had been set. |
| getUserProfile | get user profile details of the wallet.             |
| setUserEmail   | set email of the wallet.                            |

### setT2World

**function head**

    function setT2World(address t2world) public onlyOwner;

* parameters 
  * t2world: address of the T2World contract.

**description**

This method set the T2World Contract address in UserContract.

As the contract is called by owner, owner can set the address of T2World to this contract.

### getT2World

**function head**

    function getT2World() public onlyOwner returns(address);

* returns
  * address of the T2World contract.

**description**

This method return the T2World Contract address that had been set in UserContract.

As the contract is called by owner, owner can get the address of T2World to this contract.

### getUserProfile

**function head**

    function getUserProfile(address wallet) public onlyT2World returns(User);

* parameters
  * wallet: caller address of T2World contract.

* returns
  * user profile details of the wallet.

**description**

This method return user profile details of the T2World Contract caller.

As the contract is called by T2World, the method need a sender(wallet address of creator) parameter. and need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.

### setUserEmail

**function head**

    function setUserEmail(address wallet, string memory email) public onlyT2World;

* parameters
  * wallet: caller address of T2World contract.
  * email: email that will be set.

**description**

This method set user emai of the T2World Contract caller.

As the contract is called by T2World, the method need a sender(wallet address of creator) parameter. and need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.





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
| getUserProfile       | get user profile details of the caller.                 |
| setUserEmail         | set email of the caller.                                |

### createPassport

**function head**

    function createPassport(string memory title, string memory detail, uint reputation) public;

* parameters 
  * title: title of the new passport.
  * detail: detail of the new passport.
  * reputation: reputation of the new passport.

**description**

This method add a new passport NFT for sender(caller of this method). contains title, detail, and reputation.

As the contract is called by T2World, the method need a sender(wallet address of creator) parameter. and need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getPassports

**function head**

    function getPassports() view public returns(PassportDetail[] memory);

* returns
  * a list of all passports.

**description**

This method returns a list of all passports.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### createTerritory

**function head**

    function createTerritory(string memory name) public returns(bool);

* parameters
  * name: name of the new territory.

**description**

This method add a new territory for sender(caller of this method). contains name.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getTerritories

**function head**

    function getTerritories() view public returns(Territory[] memory);

* returns
  * list of all territories.

**description**

This method returns  a list of all territories.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### createItem

**function head**

     function createItem(uint256 territory, string memory title, string memory hh) public;

* parameters
  * territory: ID of a certain territory.
  * title: title of the new item.
  * hh: hash key of the new content.

**description**

This method add a new item for sender(caller of this method). contains territory, title, and hh(hash key after uploading the content to arweave).

As the contract is called by T2World, the method need a sender(wallet address of creator) parameter. and need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### updateItem

**function head**

    function updateItem(uint256 id, string memory title, string memory hh) public;

* parameters
  * id: ID of a certain item.
  * title: new title of the item.
  * hh: new content hash key of the item. 

**description**

This method update the title and hh(hash key after uploading content to arweave) of an existing item. a new version of hh is added to the item. contains id, title and hh(hash key after uploading content to arweave).

Need to verify that the sender is creator of the item.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getItems

**function head**

    function getItems() view public returns(Item[] memory);

* returns
  * a list of all items.

**description**

This method returns a list of all items.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getItemsByTerritory

**function head**

    function getItemsByTerritory(uint256 territory) view public returns(Item[] memory);

* parameters
  * territory: ID of a certain territory.

* returns
  * a list containing all items under the territory.

**description**

This method returns a list of all items under the given territory. contains territory(id of a certain territory).

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### votingItem

**function head**

    function votingItem(uint256 itemId, uint256 votingToken) public;

* parameters
  * itemId: ID of a certain item.
  * votingToken token number of votes.

**description**

This method votes on an existing item and can specify the number of votes. contains itemId, and votingToken.

As the contract is called by T2World, the method need a sender(wallet address of creator) parameter. and need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getVotingInfo

**function head**

    function getVotingInfo() view public returns(ItemVotingInfo[] memory) ;

* returns
  * a list containing all item voting information.

**description**

This method returns voting information of all items and the number of voting for each item.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### stakeItem

**function head**

    function stakeItem(uint256 itemId, uint256 stakeToken) public;

* parameters
  * itemId: ID of a certain item.
  * stakeToken: token number of the stake.

**description**

This method invests in an existing item and can specify the amount of investment. contains itemId and stakeToken.

As the contract is called by T2World, the method need a sender(wallet address of creator) parameter. and need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getStakeInfo

**function head**

    function getStakeInfo() view public returns(ItemStakeInfo[] memory);

* returns
  * a list containing all item stake information.

**description**

This method returns investment information of all items. contains the total number of tokens invested in each item.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### prepareReceiveTokens

**function head**

    function prepareReceiveTokens() public;

**description**

This method calculate and record the revenue that all investors can get in the current period. the revenue hasn't been sent.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getReceiveInfo

**function head**

    function getReceiveInfo() view public returns(ReceiveInfo[] memory);

* returns
  * a list containing the receive information of all stakeholders.

**description**

This method returns investment information of all stakeholders. contains the revenue that has been received and revenue that can be extracted.

Need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### withdraw

**function head**

    function withdraw() public;

**description**

This method allows the sender to extract the recorded revenue that should be collected at one time.

As the contract is called by T2World, the method need a sender(wallet address of creator) parameter. and need to verify that the calling address of this method is T2World. author can set the address of T2World to this contract.



### getUserProfile

**function head**

    function getUserProfile() public returns(User);

returns

* user profile details of the caller.

**description**

This method will returns user profile details of the caller. if the isActive is false, the caller hasn't registried.

### setUserEmail

**function head**

    function setUserEmail(string memory email) public;

**description**

This method allows the sender set his email information. and new user will register.



