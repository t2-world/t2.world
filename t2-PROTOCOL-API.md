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

## Core Flow
### Public APIs
You call the following APIs without proceeding login call
### World
#### GET ​/v1​/world​/stats
#### GET /v1​/world​/stats-events
#### PUT ​/v1​/world​/subscribe
#### GET ​/v1​/world​/subscribers
#### GET ​/v1​/world​/users
### Content
#### GET ​/v1​/contents​/{contentId}
#### GET ​/v1​/contents​/{contentId}​/pages
#### GET ​/v1​/contents​/{contentId}​/pages​/{pageId}​/events
### Items
#### GET ​/v1​/items​/search
#### GET ​/v1​/items​/{itemId}
#### GET ​/v1​/items​/{itemId}​/versions
### User
#### GET ​/v1​/users​/{userId}
#### GET ​/v1​/users​/{userId}​/stats-events
#### GET ​/v1​/users​/{userId}​/events
#### GET ​/v1​/users​/{userId}​/items​/{itemId}​/contents​/{contentId}​/pages​/{pageId}​/stats
### Territories
#### GET ​/v1​/territories​/search
#### GET ​/v1​/territories​/{territoryId}
#### GET ​/v1​/territories​/{territoryId}​/spaces
#### GET ​/v1​/territories​/{territoryId}​/spaces​/{spaceId}
#### GET ​/v1​/territories​/{territoryId}​/citizens​/search

### Authenticated APIs
### Login As First Call
#### POST /v1​/auth​/login

### Authenticated APIs
The following APIs requires header being set to
```
Authorization: JWT <token retrieved from login call>
```

### Users
#### GET ​/v1​/users​/my-passport
#### PATCH /v1​/users​/my-passport
#### GET ​/v1​/users​/my-footsteps
#### GET ​/v1​/users​/my-items
#### GET ​/v1​/users​/my-webpaper
#### PUT ​/v1​/users​/{userId}​/items​/{itemId}​/contents​/{contentId}​/pages​/{pageId}​/events​/start
#### PUT ​/v1​/users​/{userId}​/items​/{itemId}​/contents​/{contentId}​/pages​/{pageId}​/events​/stop
#### PUT ​/v1​/users​/{userId}​/initialize
#### PUT ​/v1​/users​/{userId}​/items​/{itemId}​/contents​/{contentId}​/pages​/{pageId}​/sync-stats
#### PUT ​/v1​/users​/{userId}​/sync-stats

### Contents
#### POST ​/v1​/contents
#### PUT ​/v1​/contents​/import
#### POST ​/v1​/contents​/upload

### Items
#### POST ​/v1​/items
#### POST ​/v1​/items​/versions
#### PUT ​/v1​/items​/versions​/{versionId}​/review-action

### Territories
#### POST ​/v1​/territories


## API links
[api.t2.world](https://hvc0cu76ch.execute-api.ap-northeast-1.amazonaws.com/Prod/swagger/index.html)

# t2 Smart Contracts
## Introduction
There are six contracts for T2 World. They are TXT Contract, Passport Contract, Governance Contract, Territory Contract, Item Contract and T2 World Contract. The first three contract were deployed for the tokens(TXT, Passport, Governanace) in T2 World. The Territory Contract is used to record  the details of the territories in T2 World. the Item Contract is used to record the details of the items in T2 World and the main business logic. The T2 World contract is a platform for managing other contracts.

我们总共为T2 World部署了六个合约，分别是TXT Contract、Passport Contract、Governance Contract、Territory Contract、Item Contract、T2 World Contract。
前三个合约是为了部署T2 World中的tokens：TXT、Passport、Governance Token。Territory Contract和Item Contract是分别用来记录Territory和Item详细信息以及业务逻辑的合约。T2 World是用来集中调用管理其它合约的总合约。

## TXT Contract
This contract is for the TXT token. It's a token of ERC20 protocol.

## Governance Contract
This contract is for governance token. It's a token of ERC20 protocol

## Passport Contract
This contract is for passport token. It's a token of ERC721 protocol.

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

        

