### Docker Networking

#### To list docker networks:
``` bash
docker network ls

NETWORK ID     NAME         DRIVER    SCOPE
70b781c33d4c   bridge       bridge    local
81f55feb9dd7   host         host      local
ac4c002c411c   none         null      local
```

#### Bridge Network
Bridge is default network. It creates virtual bridge that connects multiple container using ip address.

#### Inspecting Docker network
``` bash
docker network inspect bridge
```
By inspecting docker network we understand each docker network is assigned with a subnet

#### Create Docker network
``` bash
docker network create <user-defined-name>
```
By creating user defined network we can isolate the containers in that network from the containers in the default network

