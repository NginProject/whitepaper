# Ngin: Search Engine Based Ecosystem

![Ngin: Engine for future](./NgSlogan.png)

## Summary

Search engine is the core of internet. To hug the new century of blockchain and serve every user, we (four members now) decide to build a new search engine based on blockchain technology, and name it "Ngin"(speak as engine).

## Description

In this chain, the work of every miner need to do is acting as an "search engine spider", aka PoF(Proof of Fetch), the miner will . While running the mining software, everyone will gather webpage's url & info from a source url which can be desided by miner, and then push these to the blockchain. To get rid of scam on pushing, the blockchain system will check every page and each url & detail. The rule of verification is that the url & page will be sent to each MN, and if passing more than 10 other nodes' check on 10 block, the miner will get rewards. So with consistently pushing sites and detail to the chain, they would gain considerable benefit from chain. 

Have to say that, for initialization, we will choose the PoW at first to gather more attention. But gradually the every part of daemon(ngind) will be replaced with 

For user, who just want to search rather than join, they can freely search what they want like using google. For people who want to do more and gain more, they can use their token which are from mining to get more advanced search function. What’s the search function? For example, history webpage view, searching in a limited time range, more reliable or user-friendly answer, and so on.

Due to the significance and future development of a search engine on blockchain, we DO NOT choose to host on any existing public chain. So we decide to build on floor. As the result, it maybe takes a lot of time and capital from our team. But we would afford all pressure on the way, and try our best to produre a new kingdom like Google.

Also, to be like Google, we would build more services and provide api for vendors after the mainnet. Everyone would be able to connect to the new blockchain world through our Ngin.


```
+-----------------------------+        +-----------------------------+
|  Url & Info Fetch Miner     |        |  Url & Info Fetch Miner     |
+-----------------------------+        +-----------------------------+ 
            |                                          |
            |  +------submit with crypto---------------+                           +  +
            |  |                                                                   |  | 
+---------------------------+                             +---------------------------+
| Local/Nation Mining Pool  |                             | Local/Nation Mining Pool  |
+---------------------------+                             +---------------------------+
           |                                                            |
           |                          +------verify the result----------+
           |                          |
+--------------+              +--------------+
| (Master)Node | -----mix-----| (Master)Node |
+--------------+              +--------------+
        |                             |                            +-------------+
        |                             |-------provide service----->| User/Vendor |
        |                             |                            +-------------+
+--------------+              +--------------+
| (Master)Node | -------------| (Master)Node |
+--------------+              +--------------+
    |                                      |
    +                                      +
```

## Advantages

What's the advantage of a search engine on blockchain? 

1. Truely free, without any track or any register method required. 
2. No ads at all as you willing. Or you can choose to get reward from enabled ads 
3. Cheap advertising service.
4. Repid decentralized search experience.
5. All msg are encrypted. Keep all details safe.
6. More business development. (Born from an internal project, and will get cooperation with some other traditional company)
7. The change on proof will gain more user and support (PoW -> MasterNodes + PoW -> FuncNodes + PoF)
8. Not scam, official team will always support the project.
9. More services or applications on the base of decentralized search engine. Like AI assistant, cloud IME(Input Tool), Integrated Web Explorer, VPN or Proxy, custom data Analysis... All will be added into roadmap!
10. Equal Distribution, No ICO/Presale, No Premine
11. Get rid of content censorship, search the real things.
12. Anyone can visit any where, no bias.
13. Get bonus when valid searching or ads viewing, best choice for users.
14. Browser, Client, RemoteNode... - More than one method to get our service
15.    
...
...
?. More and more





## Backend Detail 

the main Ngin backend program is called ngind (means Ngin Daemon). It's a fork of geth. As the result, all interfaces like jsonrpc and web3 are similar to the ethereum. So, if need to convert the ethereum components to ngin components, for example, contracts, just need to change all web3 methods' "eth." prefix into "ngin.". 

Some may think changing eth to ngin is unnecessary. Why must we need to modify? We will do a totally new fork of geth, so almost all component, like the jsonrpc module, will be replaced by our version. Also, it’s meaningful that letting users realize that we are ngin rather than ethereum, to remember our ngin brand. 

Therefore, ngin contains almost all ethereum features. Short block time, fully decentralization, smart contracts, relatively transparent transactions,  

## Tech Spec

What's the components of Search Engine?

1. Spider (Fetch & Update):

Spider Technology Architecture:

Spider will follow the Proof of Fetch. Similiar to PoW, PoF will introduce two working method to the Spider Func.

First is the Peer to Peer, aka p2p. As we know, the blockchain is constituted with lots of equal nodes. For one node, the other node act as its peer. When a node/spider fetch a new/updated website info, it will format it and compress it into a msg. The msg will flow from one to another to make itself checked by most nodes. After that, all nodes' database will appended the msg.

But as we known, a pure p2p network has some disadvantage: long delay, waste bandwidth... So like pool-miner in PoW, our PoF has Master-Slave Architecture.

What's the Master-Slave Architecture? Almost all search engine work in this architecture! In that, the Fetch task will be divided into different part. For example, the Slave will download raw data, and the Master will do more on data format and assign small tasks to slaves, even manage database and make indexes. 

Finally, combine the two. We can get a more powerful structure.

```
+--------------------+
| Miner(SlaveSpider) |----+
+--------------------+    |                                                                                +---------
                          +---------+--------------------+                       +--------------------+----+
+--------------------+              | Pool(MasterSpider) |----------...----------| Pool(MasterSpider) |
| Miner(SlaveSpider) |--------------+--+-----------------+                       +--------------------+----+
+--------------------+                 |      |           \                    /           |               |                              
                                       |      |                                            |               +---------------
+--------------------+                 |      .                                            .
| Miner(SlaveSpider) |-----------------+      .                                            .
+--------------------+                        .     GOAL: Add latest data into storage     .
                                              |                                            |
+--------------------+                        |                                            |
| Miner(SlaveSpider) |----+                   |                                            |              +---       
+--------------------+    |                   |           /                     \          |              |  
                          +---------+--------------------+                       +--------------------+---+
+--------------------+              | Pool(MasterSpider) |----------...----------| Pool(MasterSpider) |
| Miner(SlaveSpider) |--------------+--+-----------------+                       +---------+----------+----------
+--------------------+                 |                                                   |
                                       |                                                   |
+--------------------+                 |                                                   +-----------------
| Miner(SlaveSpider) |-----------------+
+--------------------+

```

2. Index

Search Engine need to get a result from database with the query. It looks same to most website do, but in actual, the Search Engine require more. If you simply use the RDMS like MySQL, MsSQL, the speed of locating the keywords in query will be quite slow - because there is no index on full-text. To speed up, it is a basic knowledge that we need to make a PostingList.

[WIP: intro PostingList]


3. Search

[WIP: Our PageRank?]

[WIP: More Algo on Search]

[WIP: Decentralized Search Tasks]

## Plan

1.	Based on Elastic Integrated framework.

Elastic(Lucene) + connector(e2eBridge) + ngind(contract)

Elasticsearch(Elastic) is a search engine based on Lucene library. It provides a distributed, multitenant-capable full-text search engine with an HTTP web interface and schema-free JSON documents. Elasticsearch is developed in Java and is released as open source under the terms of the Apache License. According to the DB-Engines ranking, Elasticsearch is the most popular enterprise search engine followed by Apache Solr, also based on Lucene.

In this solution, Elastic act as a search engine & local database storage solution providor. And the ngin network just acts as the data conveyor.  

```
[WIP]
```

2.	Totally New Design in golang (on the basic of ngind)

Half-done from an internal project.

In this solution, all part will be made on our control. and ngin network will not only work as the data conveyor but do decentralized index, searching tasks. Now our internal project is not a blockchain solution but a simple solution for in-site search, but it's portable, scalable, accurate and powerful. We will develop it based on blockchain design and decenteralization idea, extending its ability on service handing capacity, making it combined with current ngind(fork of geth), to get a general internet web search engine. 

``` 
[WIP]
```

## FuncNodes Types & Rewards: (with different rewards)

1. Plan #1

Server:

```
Elastic: Do full-content search based on blockchain database --------------------------------------------------- much
Pool: update the data ------------------------------------------------------------------------------------------ medium 
Host: Do web-based search service ------------------------------------------------------------------------------ little
Minimal: online required, data sync ---------------------------------------------------------------------------- little
```

User:

```
Miner: Add instance into blockchain ---------------------------------------------------------------------------- medium
Search User: get little reward when they do click (if ads exist) ----------------------------------------------- little
```

2. Plan #2

```
Miner ---------------------------------------------------------------------------------------------------------- medium
NodeHolder(ngind) ---------------------------------------------------------------------------------------------- medium
PoolNodeHolder(ngind+ngPool) ----------------------------------------------------------------------------------- large
```

## How do team get benefit from this project?

1. diff between posting ads' price and reading ads' reward.

2. Professional in-site search/analysis services providing.

3. Future peripheral products like AI-Assistant.

NOTICE: dev funds is for ngin's develop and market, will not be used for benefit

## Why don't choose DApp?
DApp used to be our choose. 

But now it is canceled, because we can not rely on other's chain/ecosystem. Though masternode is no problem on ETH/EOS's chain, but what if FuncNode? what if PoF's spiders & pools? As the result, We think using our public chain would be more free and flexible. 

## Why don't choose Token?
We are not a finished project, and we dont like excessive marketing without any resource. And some teammates wanna be anonymous. Token is not a good choice.

And We need getting growth with our community. So the road of a Coin is satisfy the needs of us.

## Temporary Algorithm - M00N
As you know, now we are generating blocks based on Proof of Work. So we need an algorithm to achieve that.

As the result, M00N was born. M00N is an algorithm which frequently change its built-in sub-algorithm.

M00N is a variant of cryptonight, but it takes only 1MB for scratchpad. Besides variant codes on , M00N adds different algorithm into the last "Select hash" step. The default for cryptonight is `0=BLAKE-256 [BLAKE], 1=Groestl-256 [GROESTL], 2=JH-256 [JH], and 3=Skein-256 [SKEIN].`, current version of M00N adds `BMW` algo. And in future the sub-algorithm will be added, replaced, or removed when necessary fork.

```
// Part of CryptoNight Paper
                                  |
                                  V
                            +----------+
                            | Keccak-f |
                            +----------+
                             |    |
                 +-----------+    |
                 |                |
                 V                V
          +-------------+  +-------------+
          | Select hash |->| Chosen hash |
          +-------------+  +-------------+
                                  |
                                  V
                          +--------------+
                          | Final result |
                          +--------------+
```

When necessary? In our plan, ngin should be mined equally on every machine. So we dislike the GPU mining and make ngin's mining cpu-only. We will start fork when GPU mining appearing. Or there need to change/test some new feature, we will also start a necessary fork. 


# Fork?
Yes, we are ETC fork. Though it appears that ETH is much more powerful, but ETH takes too much historical burden which block us developing.  


## Community

[![Join Discord](https://discordapp.com/assets/34b52b6af57f96d86dd0b48c9e7841f7.png)](https://discord.gg/xxr748Y)
