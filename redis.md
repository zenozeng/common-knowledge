# Redis

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
