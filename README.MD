# Redis Commands

## Basic
```javascript
// Check redis version
redis-cli --version

// Connect to redis
redis-cli

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

```

## Advance

```javascript

```
