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

## Troubleshoot
#### Party data is stuck
###### /party sync could trigger global syncronization ensuring data integrity. Each GlobalParty instance will periodically check for inactive party and issue a PartyRemove notice to all GlobalParty instance if found.
#### Need to reset the Party Data in one server
##### This is not recommended and there is no builtin function to perform this action manually. GlobalParty is failsafe by default. Data inconsistency between instances will be overriden by the Global Syncronization event.
#### Need to reset the Party Data in all server
###### The first method to try is to trigger the /party reset command in one of the GlobalParty instance. This is a builtin function for controlled decentralized reset. This function will broadcast PartyReset notice to other GlobalParty instance. This method will work most of the time.
###### Should the first method fail, try triggering the /party disconnect. This will cause all GlobalParty instance to stop communicating to each other, triggering "Timeout Failsafe" function and deleting inactive Party data. Execute the command again after 1 minute to re-enable Party Syncronization. GlobalParty will then trigger the Global Syncronization event after Syncronization is re-enabled.
###### Should all method fail, a hardcoded failsafe can be triggered by sending a classified sequence of characters to the GlobalParty Network. Each GlobalParty instance is hardcoded to delete all of its data thus triggering PartyReset upon receive of the classified character sequence. This method is very risky and wont be needed most of the time. To access the GlobalParty Network, you need to have access to the Intranet.
###### Each GlobalParty instances are by default have Deadman function enabled that will also trigger PartyReset should it detect inconsistency and prolonged absence of human intervention.
