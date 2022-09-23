# NeoKratos / GAtreus
### Secure User permissions & prefix management system

## Installation
- Install Gatreus in all Backend Servers.

## Requirements
- Connection to Atreus Master Server
- (Optional) Connection to Redis PubSub Server.

## PubSub
Gatreus Client can be configured to receive PubSub messanging for High-Availability in an unlikely event of the Masters are down.

## Types of Gatreus 
There are 4 types of Kratos each handles different things
### Gatreus Universal Client
#### Runs in Velocity, Bukkit, or standalone mode to provide access to Atreus Backend
### Atreus Master
#### Runs in Multi-Master configuration to provide distributed caching, access control, and Transactional Processing to Gatreus Client.

## Knox Mode
#### Gatreus does not have cryptographic functions. All cryptographics are handled by Atreus Master and the database.
