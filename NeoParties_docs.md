# NeoParties
### Global Party system that will supersede LuckyGlobalParty
NeoParties still uses the same concept as LuckyGlobalParty but with additional recovery mechanismn to ensure data consistency between instances and updated to use NeoConstellation for instant player data syncronization.

## Installation
- Install NeoConstellation in all Backend Servers.
- (Optional) Remove Constellation. NeoConstellation and Constellation can both run in the same server.
- Install NeoParties on all Backend Servers


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
#### Operators can invoke actions such as RecreateParty, RemoveOfflineParty, RecreateAllParty, ForceGlobalSync, and HealthReport for recovery steps. Please note that NeoParties are designed to be autonomous. Please run /central healthreport to know if a human intervention are required or not. NeoParties will recommend when to do a GlobalSync based on the health reports.
