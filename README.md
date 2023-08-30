# Distributed Storage Solutions (DSS) Calibration Network SP

DSS is proving a SP on the Calibration net to assist with FEVM and General development of the network. 
You can find the configuration and information below.  


# t033435
t033435 is a 32GiB Miner on the calibration network. 
The miner can seal upto 4.5TiB/s a day and will accept deals of all sizes.
Deals will be flushed into the sealing stack every 2 hours or once it receives 32GiB of deals for a sector, witchever comes first. 

1.  Publish storage deal messages are aggregated and published every 1h, deals can wait up to 1h.
2.  Sector waiting for more deals to come in, deals can wait up to 2h.
3.  Sealing takes around 6h to complete.

**Users should expect time to get deals on chain to be up to 10h, so deals should be issued with a minimum 24h to deal start epoch.**


##  Retrieval's

We serve retrievals via the following options:
```
%# boost provider retrieval-transports t033435
libp2p
  /ip4/113.29.247.7/tcp/46155
http
  /dns/t033435.syd.distributedstorage.com/tcp/443/https
    https://t033435.syd.distributedstorage.com:443
bitswap
  /dns/t033435.syd.distributedstorage.com/tcp/4269/p2p/12D3KooWQQTfY5VaVDHMUhnsPC8cEMrnte3tLWpUndgmXhgBqRZD
```


##  Peer ID and address info

Peer ID: `12D3KooWDAwfQhGvFRDs8HJh4xsjgYxjQSpnm9C946SSK23dQgbk`
Public address: `/ip4/113.29.247.7/tcp/46155`


### Configurations parameters

#### Deal acceptance parameters

-   min. deal size: 256B
-   max. deal size: 32GiB
-   unverified price per GiB: 0 FIL
-   verified price per GiB: 0 FIL
-   accept online storage deals: yes
-   accept offline storage deals: no
-   accept online retrieval deals: yes
-   accept offline retrieval deals: no

#### Storage Ask

-   Price / epoch / Gib 0 atto
-   Verified Price / epoch / Gib 0 atto
-   Min Piece Size 256B
-   Max Piece Size 32GiB

#### Deal publish

-   Deal publish period - 1h
-   Deals per Publish Message - 4


## Config's

##### Boost config.toml 
```
[Libp2p]
  AnnounceAddresses = ["/ip4/113.29.247.7/tcp/46155"]
  
[Dealmaking]
  ConsiderOnlineStorageDeals = true
  ConsiderOfflineStorageDeals = false
  ConsiderOnlineRetrievalDeals = true
  ConsiderOfflineRetrievalDeals = false
  ConsiderVerifiedStorageDeals = true
  ConsiderUnverifiedStorageDeals = true
  PieceCidBlocklist = []
  ExpectedSealDuration = "24h0m0s"
  MaxDealStartDelay = "336h0m0s"
  StartEpochSealingBuffer = 480
  DealProposalLogDuration = "24h0m0s"
  RetrievalLogDuration = "24h0m0s"
  StalledRetrievalTimeout = "30s"
  Filter = ""
  RetrievalFilter = ""
  MaxTransferDuration = "24h0m0s"
  RemoteCommp = false
  MaxConcurrentLocalCommp = 2
  HTTPRetrievalMultiaddr = "/ip4/113.29.247.7/tcp/80/http"
  HttpTransferMaxConcurrentDownloads = 2
  HttpTransferStallCheckPeriod = "30s"
  HttpTransferStallTimeout = "5m0s"
  BitswapPeerID = ""
  DealLogDurationDays = 30
  SealingPipelineCacheTimeout = "30s"
  FundsTaggingEnabled = true

[Wallets]
  Miner = "t033435"
  PublishStorageDeals = "t3rw6bxbhtw5ncryiz3k4qyvqcqhmvkqgv3eqeuqgppnpukp6gfl7wsgzqkla5f52yfp2cxpdt7clx3evoraxa"
  DealCollateral = "t3rw6bxbhtw5ncryiz3k4qyvqcqhmvkqgv3eqeuqgppnpukp6gfl7wsgzqkla5f52yfp2cxpdt7clx3evoraxa"

[ContractDeals]
  Enabled = true
  AllowlistContracts = []
```

##### Miner config.toml 
```
[Sealing]
  MaxWaitDealsSectors = 2
  MaxSealingSectors = 0
  MaxSealingSectorsForDeals = 0
  PreferNewSectorsForDeals = true
  MaxUpgradingSectors = 0
  WaitDealsDelay = "2h0m0s"
  AlwaysKeepUnsealedCopy = true
  FinalizeEarly = true
  MakeNewSectorForDeals = true
  MakeCCSectorsAvailable = true
  BatchPreCommits = false
  AggregateCommits = false
```
