# Kratos Internal Docs
### Robust and Resilient Permission System

## Installation
- Install Kratos in all Backend Servers.

## Requirements
- Connection to Redis PubSub (if using Distributed Ledger configuration)
- Connection to Kratos Central Server (if using Centralized configuration)
- MySQL within V7 Infrastructure (Non VORD, must be durable) for data storage. Read Performance Disclaimer for more Information

### Performance Disclaimer
##### Kratos was built for resilience and robustness, Kratos will prioritize security and data durability above efficiency and performance.
##### Kratos does not use any internal cache but instead relies on LuckyNetwork's distributed MySQL Caching. Hence why it is recommended to run Kratos within LuckyNetwork V7 Infrastructure

## Types of Kratos 
There are 4 types of Kratos each handles different things
### (API) Kratos Velocity
#### Runs in Velocity Proxy as an API to expose permissioning & prefixes information to Velocity Plugins.
### (API) Kratos Spigot-SLAVE
#### Runs in Spigot Backend as an API to expose permissioning & prefixes information to Spigot Plugins.
### Kratos Spigot-HYBRID
#### Runs in Spigot Backend as an API to expose permissioning & prefixes information and enable permissioning & prefix manipulation to Spigot Plugins.
### Kratos-CENTRAL
#### A Centralized instance of Kratos responsible for data manipulation and ensuring data security.

## FAQ
#### What is 'Protected' Rank
###### Protected is a state that can be delegated to a rank. Protected rank are subject to extra security checks. Protected rank status are meant to be delegated to Staff Ranks.
###### Newly issued Protected rank are in Locked state by default.
#### What is 'Locked' Rank
###### Locked is a state that can be delegated to a rank. Ranks in locked state could be handled differently by downstream plugin. However, Kratos will refuse to recognize Locked rank that are Protected for security reasons.
###### Kratos Spigot-HYBRID and Kratos-CENTRAL can lock and unlock non protected rank.
###### Kratos Spigot-HYBRID can lock a protected rank but cannot unlock a protected rank. This is due to the fact that Locked protected Rank are no longer recognized by Kratos. Therefore Kratos Spigot-HYBRID cannot reach the Rank object as it is not recognized in the first place. Kratos Spigot-HYBRID does not have alternate Kratos Rank Loader logic to recognize protected and locked rank.
###### Kratos-CENTRAL can unlock a protected rank with the right authentication code. With a correct authentication code, Kratos-CENTRAL can attempt to load locked protected rank using alternate Kratos Rank Loader.

## Knox Mode
#### Knox Mode is an option to run Krato with Cryptographic functions enabled.
While Using Knox Mode, Kratos Rank Loader will attempt to verify rank and prefix relations before loading them. Knox Mode ensures that rank data can only be manipulated by Kratos-CENTRAL hence why Kratos Spigot-HYBRID will automatically be downgraded to Spigot-SLAVE when Knox Mode is enabled. Unlocking a Protected Rank while Knox Mode is enabled requires an authorized administrator to generate a one time authentication code from Kratos Secret Management Engine. One time authentication code will be required by Kratos-CENTRAL to sign and validate unlock process of Protected rank. Kratos will store all encryption key and do all PKE functions within a self-contained Kratos Secret Management Engine. Kratos Secret Management Engine will not release stored encryption key and will only process one time authentication code request from an authorized staff using an authorized device that is connected via Level 2 intranet.
