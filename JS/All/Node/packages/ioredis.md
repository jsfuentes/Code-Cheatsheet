# IoRedis

```
npm install ioredis
```

## Setup

```ts
new Redis(); // Connect to 127.0.0.1:6379
new Redis(6380); // 127.0.0.1:6380
new Redis(6379, "192.168.1.1"); // 192.168.1.1:6379
new Redis("/tmp/redis.sock");
new Redis({
  port: 6379, // Redis port
  host: "127.0.0.1", // Redis host
  username: "default", // needs Redis >= 6
  password: "my-top-secret",
  db: 0, // Defaults to 0
});
```

## Usage

```ts
redis.set("mykey", "value"); // Returns promise

redis.get("mykey").then((result) => {
  console.log(result); // Prints "value"
});

redis.zadd("sortedSet", 1, "one", 2, "dos", 4, "quatro", 3, "three");
redis.zrange("sortedSet", 0, 2, "WITHSCORES").then((elements) => {
  // ["one", "1", "dos", "2", "three", "3"] as if the command was `redis> ZRANGE sortedSet 0 2 WITHSCORES`
  console.log(elements);
});

// All arguments are passed directly to the redis server, so technically ioredis supports all Redis commands.
// The format is: redis[SOME_REDIS_COMMAND_IN_LOWERCASE](ARGUMENTS_ARE_JOINED_INTO_COMMAND_STRING)
// so the following statement is equivalent to the CLI: `redis> SET mykey hello EX 10`
redis.set("mykey", "hello", "EX", 10);
```

### Lists

```ts
//add
const numbers = [1, 3, 5, 7, 9];
  await redis.lpush("user-list", numbers);

  const popped = await redis.lpop("user-list");
  console.log(popped); // 9

//retrieve
  const all = await redis.lrange("user-list", 0, -1);
  console.log(all); // [ '7', '5', '3', '1' ]

  const position = await redis.lpos("user-list", 5);
  console.log(position); // 1
```

## Sets

```ts
// Array of members to be added to the set
const setMembers = ['member1', 'member2', 'member3'];

// Using the SADD command to add members to the set
redis.sadd(mySetKey, ...setMembers)
  .then(result => {
    console.log(`Added ${result} members to the set`);
    
    // Using the SMEMBERS command to retrieve all members of the set
    return redis.smembers(mySetKey);
  })
```

