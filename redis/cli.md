
## Redis CLI Example
[[redis]] cli
```bash
redis-cli
SET age 25
GET age
DEL age
```

---

## Integration with Java
can use **Jedis**, **Lettuce**, or **Redisson** libraries.
### Basic Jedis Example:

```java
import redis.clients.jedis.Jedis;

public class RedisExample {
    public static void main(String[] args) {
        try (Jedis jedis = new Jedis("localhost", 6379)) {
            jedis.set("key", "value");
            String value = jedis.get("key");
            System.out.println(value);
        }
    }
}
```

