# Redis Commands

## Installation
```javascript
// install redis
sudo apt-get install redis-server

// Check redis version
redis-cli --version

// Connect to redis
redis-cli

// Start redis
sudo service redis-server start

// Stop redis
sudo service redis-serverstop

// Restart redis
sudo service redis-server restart

// Check redis status
sudo service redis-server status

// Start redis with config file
sudo redis-server redis.conf

// Shutdown redis
redis-cli shutdown

// Check where redis-cli is running
which redis-cli

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

// Test message transfer
ECHO "message"

// list key dictionary 
KEYS *
```

```javascript
// list keys starting with 
KEYS a*

// list keys ending with 
KEYS *z

// list keys starting and ending with 
KEYS a*z

// list keys with having in middle
KEYS *xyz*

// Dictionary size
DBSIZE

// Dictionary info
INFO keyspace
```

```javascript
// create a key 
SET mykey "mykey value"

// get a key
GET mykey

// create a key with expiry (EX = seconds, PX = milliseconds)
SET mykey "mykey value" EX 10
// or set in seconds
EXPIRE mykey 10

// check expiry of a key  (-1 = not set, -2 = expired)
TTL mykey

// check datatype of a key
TYPE mykey

// check if a key exists (1 = true, 0 = false)
EXISTS mykey

// delete a key
DEL mykey
```


## Intermediate
```javascript
//Enable Authentication
sudo nano /etc/redis/redis.conf 
// add 'requirepass 123' in '/etc/redis/redis.conf'
// restart redis

//Enable LAN
sudo nano /etc/redis/redis.conf // add 'bind 192.168.1.245' in '/etc/redis/redis.conf'
// restart redis

//Measure redis command performance in 'PowerShell'
Measure-Command { redis-cli -h 127.0.0.1 -p 6379 keys * }
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

//will ask for confirmation (yes), type `yes` and hit enter
```

```js
//connect to the a node in cluster mode
redis-cli -h 127.0.0.1 -p 7000 -c
```

```js
//check cluster and nodes status
cluster nodes
```
