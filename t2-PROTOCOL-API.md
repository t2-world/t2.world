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

## T2World Public Methods

The T2World Public Methods are for users.

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

## Governance Contract
This contract is for governance token. It's a token of ERC20 protocol

## Passport Contract
This contract is for passport token. It's a token of ERC721 protocol.

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

### getPassports

**function head**

    function getPassports() view public returns(PassportDetail[] memory);

* returns
    * a list of all passports.

**description**

this method returns a list of all passports.

## Territory Contract
This contract is for territories in T2 World.

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

### hasTerrtory

**function head**
        
    function hasTerrtory(uint id) view public returns(bool); 

* parameters 
    * id: ID of a certain territory.

* returns
    * a bool value(true or false).

**decription**

this method returns a bool value whether there is a territory of the given ID.

### getTerritory

**function head**
    
    function getTerritory(uint id) view public returns(Territory memory);

* parameters
    * id: ID of a certain territory.

* returns
    * details of a territory.

**description**

this method returns the details of a territory of the given ID.

### getTerritoryList

**function head**

    function getTerritoryList() view public returns(Territory[] memory);

* returns
    * list of all territories.

**description**

this method returns a list of all territories.

## Item Contract
This contract is for items in T2 World.

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

### updateItem

**function head**

    function updateItem(uint256 id, string memory title, string memory hh) public;

* parameters
    * id: ID of a certain item.
    * title: new title of the item.
    * hh: new content hash key of the item. 

**description**

this method update the title and content hash key of the item with the given ID.

### getItem

**function head**

   function getItem(uint256 id) view public returns(Item memory);

* parameters
    * id: ID of a certain item.

* returns
    * details of the item.

**description**

this method returns details of a certain item with the given ID.

### getItemList

**function head**

    function getItemList() view public returns(Item[] memory);

* returns
    * a list of all items.

**description**

this method returns a list of all items.

### getItemListByTerritory

**function head**

    function getItemListByTerritory(uint territory) view public returns(Item[] memory);

* parameters
    * territory: ID of a certain territory.

* returns
    * a list containing all items under the territory.

**description**

this method returns a list of all items under the given territory.
        
### votingItem

**function head**

    function votingItem(address sender, uint256 itemId, uint256 votingToken) public;

* parameters
    * sender: wallet address of the user.
    * itemId: ID of a certain item.
    * votingToken token number of votes.

**description**

this method votes on a given item according to the specified number of votes.

### getVotingInfo

**function head**

    function getVotingInfo() view public returns(ItemVotingInfo[] memory) ;

* returns
    * a list containing all item voting information.

**description**

this method returns a list containing all item voting information.

### stakeItem

**function head**

    function stakeItem(address sender, uint256 itemId, uint256 stakeToken) public;

* parameters
    * sender: wallet address of the user.
    * itemId: ID of a certain item.
    * stakeToken: token number of the stake.

**description**

this method stake to a item with the given ID.

### getStakeInfo

**function head**

    function getStakeInfo() view public returns(ItemStakeInfo[] memory);

* returns
    * a list containing all item stake information.

**description**

this method return a list containing all item stake information.

### prepareReceiveTokens

**function head**

    function prepareReceiveTokens() public;

**description**

this method calculate the tokens that every stakeholders should get.

### getReceiveInfo

**function head**

    function getReceiveInfo() view public returns(ReceiveInfo[] memory);

* returns
    * a list containing the receive information of all stakeholders.

**description**

get the receive information of all the stakeholder.
        
### withdraw

**function head**

    function withdraw(address sender) public;

* parameters
    * sender: wallet address of a user.

**description**

this method withdraw the token to the sender(user).

## T2World Contract

The T2 World contract is a platform for managing other contracts.

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

### getPassports

**function head**

    function getPassports() view public returns(PassportDetail[] memory);

* returns
  * a list of all passports.

**description**

this method returns a list of all passports.

### createTerritory

**function head**

    function createTerritory(string memory name) public returns(bool);

* parameters
  * name: name of the new territory.

**description**

this method add a new territory with the given parameters.

### getTerritories

**function head**

    function getTerritories() view public returns(Territory[] memory);

* returns
  * list of all territories.

**description**

this method returns a list of all territories.

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

### getItemsByTerritory

**function head**

    function getItemsByTerritory(uint256 territory) view public returns(Item[] memory);

* parameters
  * territory: ID of a certain territory.

* returns
  * a list containing all items under the territory.

**description**

this method returns a list of all items under the given territory.
        

### votingItem

**function head**

    function votingItem(uint256 itemId, uint256 votingToken) public;

* parameters
  * itemId: ID of a certain item.
  * votingToken token number of votes.

**description**

this method votes on a given item according to the specified number of votes.

### getVotingInfo

**function head**

    function getVotingInfo() view public returns(ItemVotingInfo[] memory) ;

* returns
  * a list containing all item voting information.

**description**

this method returns a list containing all item voting information.

### stakeItem

**function head**

    function stakeItem(uint256 itemId, uint256 stakeToken) public;

* parameters
  * itemId: ID of a certain item.
  * stakeToken: token number of the stake.

**description**

this method stake to a item with the given ID.

### getStakeInfo

**function head**

    function getStakeInfo() view public returns(ItemStakeInfo[] memory);

* returns
  * a list containing all item stake information.

**description**

this method return a list containing all item stake information.

### prepareReceiveTokens

**function head**

    function prepareReceiveTokens() public;

**description**

this method calculate the tokens that every stakeholders should get.

### getReceiveInfo

**function head**

    function getReceiveInfo() view public returns(ReceiveInfo[] memory);

* returns
  * a list containing the receive information of all stakeholders.

**description**

get the receive information of all the stakeholder.
        

### withdraw

**function head**

    function withdraw() public;

**description**

this method withdraw the token to the sender(user).
