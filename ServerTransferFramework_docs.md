# ServerTransferFramework Documentations
### A part of VerseEngine project for Reliable Player Transfer

## ServerTransferFramework Context
##### ServerTransferFramework was developed as a part of the VerseEngine Project, a Hyper-Scaleable Game Server Engine. ServerTransferFramework is used to reliabily transfer a player between servers.

## Definition
- Player : An object or an entity of a Minecraft Player
- Origin Server : A Game Server which the current player is on.
- Destination Server : A Game Server which the Player wishes to be transfered to.
- Transfer : A transaction between the origin server and the destination server where a player will be moved from the origin server to the destination server if the transaction is sucessful.
- ServerTransferFramework instance : An instance of ServerTransferFramework that can initiate or receive Transfer request. One server should have one ServerTransferFramework

## Components
- ServerTransferFramework : A system classified as a SuperSystem type which could act as a Client or Server at the same time. Every instance ServerTransferFramework communicate with other instance in order to initiate a transfer or respond to a transfer.
- Redis : A Redis Server is required by ServerTransferProtocol to communicate with each other
- HUMP : A High Performance Unified Messanging Protocol is an alternative to Redis that ServerTransferProtocol could use to communicate with each other

## Requirements
- Standard CraftBukkit server software
- Redis with High-Availability configuration or HUMP
- LuckyNetwork V4-2020 Setup or Higher
- Bungeecord Gelacord fork or ArmoredVelocity (Velocity fork) for best performance.

## Installation
- Install the ServerTransferFramework on all server group
- Configure the Group and Subgroup name
- Ensure that all ServerTransferFramework instance are connected to the same Redis Server or HUMP Network

## Configurations
- server-name           : The name of the server. Should be the same as the name registered in the Proxy. Putting "DEFAULT" will use the Bukkit's Server Name
- server-group          : The group name of the server. Server with the same group will be "linked" automatically for stuff such as Group Balancing. ServerTransferFramework cannot transfer player to a server with different group for safety reason(s)
- server-subgroup       : The subgroup name of the server. Cannot be null or blank.
- regulate-player-join  : If enabled, ServerTransferFramework will only allow players that are transfered to the server to join. Useful for security reason(s)

## API
### Events
- IncomingTransferRequestEvent  : Triggered when the ServerTransferFramework received a Transfer request from another server. Event is cancellable and custom reason can be set as the cancelled reason.
- IncomingTransferFinishEvent   : Triggered when a successful transfer has been performed and the player is now joined in the server. Event is not cancellable.
- IncomingTransferFailureEvent  : Triggered when the ServerTransferFramework detected a general failure where a transfer is not successful.
- OutgoingTransferRequestEvent  : Triggered when the ServerTransferFramework send a Transfer request to another server.
- OutgoingTransferFinishEvent   : Triggered when a successful transfer has been performed and the player is now joined in the destination server.
- OutgoingTransferFailureEvent  : Triggered when the ServerTransferFramework detected a general failure where an outbound transfer is not successful.

### Methods
#### ServerTransferFramework#getAPI()
- void performTransfer(String player_uuid, String destination_server, String action_payload)
- List<Server> getServers()

### Warning
##### While ServerTransferFramework expose some unsafe method to manipulate its internal database and algorithm, it is not recommended to interact with ServerTransferManager other than using the Events and Methods above.
##### ServerTransferFramework was designed to be fully autonomous and self-contained in its operation.


## Troubleshoot
#### NullPointerExeption thrown
###### It is a known bug that ServerTransferFramework will thrown an NPE when trying to register a group and subgroup for the first time. However, ServerTransferFramework should be able to register the group and subgroup on the second try using a failsafe mechanismn based on the V6-2022 Reliability Policy.

##### ServerTransferFramework state of automation
###### ServerTransferFramework was designed based on V7-2023 policy where the system is expected to handle every situation without any human interference. Disclaimer: ServerTransferFramework was never tested for compliance with the protocol, ensure monitoring at all time.
