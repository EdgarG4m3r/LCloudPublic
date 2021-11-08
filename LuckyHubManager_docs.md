# LuckyHubManager Documentations
### Advanced Hub Management System

## LuckyHubManager is consist of two main component
- LuckyHubBungee / LuckyHubVelocity : Contains Hub-Balancer, Hub Router, and Availability Detection. Redirect player to available Hub
- LuckyHubSpigot : Contains Status-Reporter module. Send status report to the LuuckyHubBungee/Velocity via VORD.

## Installation
- Install LuckyHubBungee / LuckyHubVelocity (LuckyHubProxy) in the Proxies
- Install LuckyHubSpigot in the Backend Hubs
- Ensure that both (LuckyHubProxy) and LuckyHubSpigot are connected to the same MySQL Database with VORD enabled
- Ensure that the server-name in the server.properties are correct

## Troubleshoot
#### High CPU usage on Server / Server is lagging
###### Ensure that Virtual Object Relations Database is enabled for the database table. Currently, only `prod` MySQL had this technology enabled.
#### Inconsistent Balancing
###### LuckyHubBungee only comes with Static Round-Robin algorithm for balancing. (LuckyHubProxy) will also skip unregistered server.
#### One or more server is being skipped
###### Ensure that you've followed the installation step correctly. If the server setup version is > V5-2021, please ensure that LCloudBungeeBridge is installed in the proxy.
#### External Balancer cannot send player to the Hub or Limbo
###### By default, LuckyHubManager will automatically balance player that are connecting to this server `Hub` and `Limbo` 

#### Message Broker is down
###### If either the Message Broker or VORD is down, LuckyHubManager will keep the latest configuration until everything is back to normal.

##### LuckyHubManager state of automation
###### LuckyHubManager was designed based on V6-2022 policy where the system is expected to handle every situation without any human interference. Therefore, manual human interference such as updating the configuration is not possible. In an event of an emergency requiring manual interference, The Operator must explicitly disable LuckyHubManager Controller by shutting down its process. By doing this, any automation will be disabled.
