# Redis Commands

## Installation
```javascript
// install redis
sudo apt-get install redis-server
```

```javascript
// Check redis status
sudo service redis-server status
```

```javascript
// Stop redis
sudo service redis-server stop
```

```javascript
// Start redis
sudo service redis-server start
```

```javascript
// Restart redis
sudo service redis-server restart
```

```javascript
// Start redis with config file
sudo redis-server redis.conf
```

```javascript
// Check redis version
redis-cli --version
```

```javascript
// Connect to redis
redis-cli
```

```javascript
// Shutdown redis
redis-cli shutdown
```

```javascript
// Check where redis-cli is running
which redis-cli
```

```javascript
// Check where redis is installed
locate redis.conf

    executable:/usr/bin/redis-cli
    executable:/usr/bin/redis-server
    config_file:/etc/redis/redis.conf
```


## Basic
```javascript
// Check connection
PING
```

```javascript
// Test message transfer
ECHO "message"
```

```javascript
// list key dictionary 
KEYS *
```

```javascript
// list keys starting with 
KEYS a*
```

```javascript
// list keys ending with 
KEYS *z
```

```javascript
// list keys starting and ending with 
KEYS a*z
```

```javascript
// list keys with having in middle
KEYS *xyz*
```

```javascript
// scan keys with name pattern
redis-cli -c -h <IP> -p <PORT> -a <PASSWROD> SCAN 0 MATCH "KEY*" COUNT 1000000
```

```javascript
// Dictionary size
DBSIZE
```

```javascript
// Dictionary info
INFO keyspace
```

```javascript
// create a key 
SET mykey "mykey value"
```

```javascript
// get a key
GET mykey
```

```javascript
// create a key with expiry (EX = seconds, PX = milliseconds)
SET mykey "mykey value" EX 10
// or set in seconds
EXPIRE mykey 10
```

```javascript
// check expiry of a key  (-1 = not set, -2 = expired)
TTL mykey
```

```javascript
// check datatype of a key
TYPE mykey
```

```javascript
// check if a key exists (1 = true, 0 = false)
EXISTS mykey
```

```javascript
// delete a key
DEL mykey
```


## Intermediate (Redis Configurations)

```javascript
//Enable Authentication
sudo nano /etc/redis/redis.conf 
// add 'requirepass 123' in '/etc/redis/redis.conf'

// restart redis required
sudo service redis-server restart
```

```javascript
//Enable  Redis on LAN/WAN
sudo nano /etc/redis/redis.conf // add 'bind 192.168.1.245' in '/etc/redis/redis.conf'

// restart redis required
sudo service redis-server restart
```

```javascript
//change default redis port
sudo nano /etc/redis/redis.conf // change 'port 6379' to 'port 7000'

// restart redis required
sudo service redis-server restart
```

```javascript
//Measure redis command performance On Windows in 'PowerShell'
Measure-Command { redis-cli -h 127.0.0.1 -p 6379 keys * }

//Measure redis command performance On Linux in 'Terminal'
time redis-cli -h 127.0.0.1 -p 6379 keys "*"
```

```javascript
//redis.service for auto start
/etc/systemd/system/redis.service
```

## Advanced (Cluster)

```javascript
//create a redis-conf
nano redis.conf
```

```properties
#redis.conf
port 7000
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
appendonly yes
```

```javascript
//create directories for cluster nodes
mkdir 7000 7001 7002 7003 7004 7005
```

```javascript
//copy redis.conf to all node folders
cp redis.conf 7000/redis.conf
cp redis.conf 7001/redis.conf
cp redis.conf 7002/redis.conf
cp redis.conf 7003/redis.conf
cp redis.conf 7004/redis.conf
cp redis.conf 7005/redis.conf
```
> Open each node conf file in each folder and replace port with node's port

```javascript
//navigate to each folder and run redis
7000$ sudo redis-server ./redis.conf
7001$ sudo redis-server ./redis.conf
7002$ sudo redis-server ./redis.conf
7003$ sudo redis-server ./redis.conf
7004$ sudo redis-server ./redis.conf
7005$ sudo redis-server ./redis.conf
```

```javascript
//create cluster of all these running nodes
redis-cli --cluster create 127.0.0.1:7000 127.0.0.1:7001 127.0.0.1:7002 127.0.0.1:7003 127.0.0.1:7004 127.0.0.1:7005 --cluster-replicas 1

//it will ask for confirmation (yes), type `yes` and hit enter
```

```javascript
//connect to the a node in cluster mode
redis-cli -h 127.0.0.1 -p 7000 -c
```

```javascript
//check cluster and nodes status
CLUSTER nodes
```

```javascript
//check role of the a node in cluster mode
ROLE
```


#### Redis-Server executable file directory
```
└── var
    └── bin
        └── redis-server
```

#### Systemd services
```
└── etc
    └── systemd
        └── system
            ├── redis_7000.service
            └── redis_7001.service
```

#### Node config files
```
└── etc
    └── redis
        ├── redis_7000.conf
        └── redis_7001.conf
```

#### Log Directories
```
└── var
    └── log
        └── redis
            ├── redis-server.log
            ├── redis-server.log.1.gz
            ├── redis-server.log.2.gz
            └── redis-server.log.3.gz
```
