# LuckyGlobal Party Internal Docs
### Global Party system for LuckyNetwork V7 year 2023 Update

## LuckyGlobalParty
A Decentralized Party system based on a Distributed Database model.

## Installation
- Install GlobalParty / BedWars Party in all Backend Servers.


## Operations
#### Party Create
###### Create a Party
#### Party Transfer
###### Transfer a Party to another member
#### Party Leave
###### Leave the party. Leader cannot leave a party
#### Party Disband
###### (Leader Only) Disband or Remove the Party.
#### Party Kick
###### (Leader Only) Kick a Party member.
#### Party Clear
###### (Leader Only) Kick all offline Party member.
#### Party Warp
###### (Leader Only) Warp all player to the leader's current game or server.
#### Party Go
###### Teleport to party leader's current game or server.
#### Party Chat
###### Send a message visible to all Party Member

## Data Persistence - Fast Recovery from Server Restarts
GlobalParty instances are decentralized and does not store any party information in a persistent database. GlobalParty trigger an immediate GlobalSync to quickly recover data from another instance called 'Master' without waiting for another instance periodic update to rebuild data that might took up to three seconds. Here are three 'Master' election algorithm:
### Floating Master (Default)
#### In this configuration, the oldest GlobalParty instance will act as a 'Master' server when another server requested a GlobalSync. This is the closest thing to total decentralization.
###### Pros: Very resilient, Party data most likely will survive a total server restart level or OFFLINE Maintenance. During an OFFLINE Maintenance, the Party Data can survive in an instance that runs on servers that are classified as a "designated survivor" such as Vote Servers, Cons: Not performance wise and might cause unexpected load. For example, if GlobalParty 'elects' Vote Servers with little resource as the 'Master Server', the server could crash if hundreds of servers were rebooted simultaneously.
### Designated Central 
#### This is the prefered configuration. One server can be dedicated to save Party Data.
###### Pros: Very efficient, Cons: Still not fault-tolerant and not highly available
### Floating Multiple Designated Central 
#### In this configuration, Multiple Designated Central will act as a 'Master' where the oldest Central Server will act as the 'Primary Master'. Every 'Master' Server would store Party Data but only the 'Primary Master' will serve the data by default. Should the 'Primary Master' entered a fault state, the second oldest 'Master' will be elected as the 'Primary Master'.
###### Pros: Very efficient and Highly Available, Cons: Very complicated and is still in experimental
 

## Troubleshoot
#### Party data is stuck
###### GlobalParty internal operations are fully autonomous. A Centralized PartyDisbander Task also runs periodically on GlobalParty Master to ensure GlobalParty data is syncronized across all servers. An Internal Timer in each GlobalParty instances will takeover Centralized PartyDisbander should the centralized PartyDisbander entered fault state. 
