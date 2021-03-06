# Redis

## Pipelining

- RTT
- 减少 socket I/O. 从而减少 read() and write() syscal (user land to kernel land context switch)

https://redis.io/topics/pipelining

## Distributed locks

- https://redis.io/topics/distlock

```
SET resource_name my_random_value NX PX 30000
```

```lua
if redis.call("get",KEYS[1]) == ARGV[1] then
    return redis.call("del",KEYS[1])
else
    return 0
end
```

- 过期保证锁超时自动释放
- random_value 保证不会误释放他人的锁
- 适用于单实例

### Redlock

1. It gets the current time in milliseconds.
2. It tries to acquire the lock in all the N instances sequentially, using the same key name and random value in all the instances. During step 2, when setting the lock in each instance, the client uses a timeout which is small compared to the total lock auto-release time in order to acquire it. For example if the auto-release time is 10 seconds, the timeout could be in the ~ 5-50 milliseconds range. This prevents the client from remaining blocked for a long time trying to talk with a Redis node which is down: if an instance is not available, we should try to talk with the next instance ASAP.
3. The client computes how much time elapsed in order to acquire the lock, by subtracting from the current time the timestamp obtained in step 1. If and only if the client was able to acquire the lock in the majority of the instances (at least 3), and the total time elapsed to acquire the lock is less than lock validity time, the lock is considered to be acquired.
4. If the lock was acquired, its validity time is considered to be the initial validity time minus the time elapsed, as computed in step 3.
5. If the client failed to acquire the lock for some reason (either it was not able to lock N/2+1 or the validity time is negative), it will try to unlock all the instances (even the instances it believed it was not able to lock).

- Lock N/2+1 instances 来支持多实例
- 不依赖服务端节点时钟同步
- 加锁失败时如果发生网络分区，可能需要等待超时

## Codis

- https://github.com/CodisLabs/codis
- https://github.com/CodisLabs/codis/blob/release3.2/doc/tutorial_zh.md#3-jodis-与-ha

## Eviction

https://redis.io/topics/lru-cache

- noeviction: return errors when the memory limit was reached and the client is trying to execute commands that could result in more memory to be used (most write commands, but DEL and a few more exceptions).
- allkeys-lru: evict keys by trying to remove the less recently used (LRU) keys first, in order to make space for the new data added.
- volatile-lru: evict keys by trying to remove the less recently used (LRU) keys first, but only among keys that have an expire set, in order to make space for the new data added.
- allkeys-random: evict keys randomly in order to make space for the new data added.
- volatile-random: evict keys randomly in order to make space for the new data added, but only evict keys with an expire set.
- volatile-ttl: evict keys with an expire set, and try to evict keys with a shorter time to live (TTL) first, in order to make space for the new data added.

### Approximated LRU

![C2D6E3B5-1DFB-4FB6-96CF-7AD7216F11B9](https://user-images.githubusercontent.com/2544489/124779286-3d257f00-df74-11eb-8571-c2cfb770b6c5.png)

```
CONFIG SET maxmemory-samples <count>
```

### LFU (Redis 4.0)

- Least Frequently Used
- Morris counter

## Transcation

https://redis.io/topics/transactions

- atomic
- MULTI / EXEC
- even when a command fails, all the other commands in the queue are processed
- AOF: Redis use a **single** write(2) syscall to write the transaction on disk
- WATCH is used to provide a check-and-set (CAS) behavior to Redis transactions

## Persistence

> The general indication is that you should use both persistence methods if you want a degree of data safety comparable to what PostgreSQL can provide you.
If you care a lot about your data, but still can live with a few minutes of data loss in case of disasters, you can simply use RDB alone.
There are many users using AOF alone, but we discourage it since to have an RDB snapshot from time to time is a great idea for doing database backups, for faster restarts, and in the event of bugs in the AOF engine.

> In the case both AOF and RDB persistence are enabled and Redis restarts the AOF file will be used to reconstruct the original dataset since it is guaranteed to be the most complete.

https://redis.io/topics/persistence
