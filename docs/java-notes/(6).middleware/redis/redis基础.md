## Redis基础命令

### login

```shell
redis-cli -h host -p port -a password
```

```shell
redis-cli -h 127.0.0.1 -p 6379 -a "mypass"
```

### key

```shell
## 设置key
set redis_key redis_value
set hello redis

## 删除key
del key_name
del hello

## 序列化
dump key_name
dump hello

## 存在
exist key_name
exist hello

## 设置过期时间
expire key_name time_in_seconde
expire hello 60

## 匹配
keys pattern
keys * # 查询所有
keys he*

## 移动
move key_name destination
move hello 1

## 移除过期时间，使key永久有效
persist key_name
persist key

## 以毫秒为单位返回 key 的剩余过期时间
pttl key_name
pttl hello

## 以秒为单位返回 key 的剩余过期时间
ttl key_name
ttl hello

## 从当前数据库中随机返回一个 key
randomkey

## 修改 key 的名称
rename old_key_name new_key_name
rename hello hillo

## 判断key的类型
type key_name
type hello
```

### redis string

```shell
## SET 命令用于设置给定 key 的值。如果 key 已经存储其他值， SET 就覆写旧值，且无视类型。
set key value
SET key "value"

```

