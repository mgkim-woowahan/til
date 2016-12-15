### CRUD

Key-Value 로 데이터를 저장하는 Redis의 CRUD는 간단하다.

```redis
> SET loginuser mingook
OK
> GET loginuser
mingook
> SET loginuser cinabro88
cinabro88
> DEL loginuser
(integer) 1
```

위 예처럼 SET, GET, DEL의 세가지 명령어로 CRUD를 간단히 수행할 수 있다.

### Atomically Increment

Value로 Numeric을 가지는 경우, 값을 증가시킬 수 있다.

```Redis
> SET count 10
OK
> INCR count
(integer) 11
```

INCR 명령어는 해당 값의 원자성을 보장해 준다.

### Expire

Redis는 데이터에 expire 타임을 설정할 수 있다.

```Redis
> SET cart pizza
OK
> EXPIRE cart 10
(integer) 1
> TTL cart
(integer) 10
```

Expire Time은 초단위로 설정할 수 있으며, TTL 명령으로 확인할 수 있다. TTL에서 -1은 무제한, -2는 값이 없음을 의미한다.

여기서 주의할 점은, 해당 Key를 업데이트 하면 Expire 값은 reset 된다.

### Value Data Structure

Redis와 Memcached의 가장 큰 차이는 Value에 String뿐만 아니라 다양한 자료구조를 사용할 수 있다는 점이다.

#### List

LPUSH, RPUSH 명령으로 리스트의 처음과 끝에 데이터를 추가할 수 있으며, LRANGE 명령으로 리스트의 데이터를 조회할 수 있다.

```
> RPUSH member mingook
(integer) 1
> RPUSH member cinabro88
(integer) 2
> LPUSH member admin
(integer) 3
> LRANGE member 0 -1
1) "admin"
2) "mingook"
3) "cinabro88"
```

LRANGE 의 파라미터는 순서대로 (List의 Key, 시작, 끝) 을 나타낸다. 세번째 파라미터의 경우 -1은 끝까지를 의미한다.

그외에 제공되는 커맨드로는 LLEN, LPOP, RPOP 가 있다. 명령어를 보는 순간 어떤 동작을 할지는 예상가능!! (예상안되면 한번 실행해보자)

#### Set

Set은 순서가 없으며, 데이터가 중복해서 저장되지 않는다. 기본적인 메소드들은 다음과같다.* 추가 - SADD key value* 제거 - SREM key value* 포함여부 - SISMEMBER key value* 출력 - SMEMBERS key* 병합 - SUNION key1 key2 SUNION은 두개의 SET을 합쳐준다. 이때도 중복된 값은 제거된다.

#### Sorted Set

정렬이 가능한 Set이다. 데이터를 추가할때 score(가중치)를 같이 입력해서 오름차순으로 정렬한다.* 추가 - ZADD key score value* 제거 - ZREM key value* 출력 - ZRANGE key start end

#### Hash

마지막 자료구조는 Hash이다. Hash는 field라는 sub key가 추가되어, 하나의 key에 객체를 저장할 수 있다.

```
> HSET cart:mingook shop 1
(integer) 1
> HSET cart:mingook food pizza
(integer) 1
> HSET cart:mingook quantity 2
(integer) 1
> HGET cart:mingook food
"pizza"
> HGET cart:mingook shop
"1"
```

공식사이트에서 자세한 커맨드를 확인할 수 있다.

### 참고

-	[Redis 공식사이트](www.naver.com)
