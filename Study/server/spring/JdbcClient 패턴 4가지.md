# 1. 자동매퍼 (타입 넘기기)

```kotlin
data class User(
    val id: Long,
    val name: String,
    val status: Status,         // ENUM
    val createdAt: LocalDateTime
)

val users: List<User> = jdbcClient.sql(
    "select id, name, status, created_at from users where status = :status"
).param("status", Status.ACTIVE)
 .query(User::class.java)     // 내부적으로 DataClassRowMapper 선택
 .list()
```

- Kotlin data class / Java record -> `DataClassRowMapper`
- JavaBean -> `BeanPropertyRowMapper`
- 스네이크 -> 카멜 자동 변환 지원
# 2. 커스텀 RowMapper
```kotlin
class UserRowMapper : RowMapper<User> {
    override fun mapRow(rs: ResultSet, rowNum: Int): User {
        val id = rs.getLong("id").let { if (rs.wasNull()) null else it } ?: error("id null")
        return User(
            id = id,
            name = rs.getString("name"),
            status = Status.valueOf(rs.getString("status")),
            createdAt = rs.getTimestamp("created_at").toLocalDateTime()
        )
    }
}

val users = jdbcClient.sql("select * from users")
    .query(UserRowMapper())    // 커스텀 매퍼 주입
    .list()
```
- 정점: enum, json, 복합 변환 등 마음대로 가능
- 단점: 코드량 증가. but 명시적 / 안전함

# 3. DataClassRowMapper / BeanPropertyRowMapper 명시
```kotlin
val mapper = DataClassRowMapper<User>(User::class.java)
val users = jdbcClient.sql("select id, name, status, created_at from users")
    .query(mapper)
    .list()
```
- 타입 추론이 애매하거나, 자동 선택을 확실히 통제하고 싶을때!
# 4. 중첩 / 조인 매핑(RowMapper + ResultSetExtractor)
- 한 행 = 한객체가 유지되는 경우 -> `커스텀 RowMapper`에서 합성
```kotlin
data class OrderWithUser(
    val orderId: Long,
    val price: Long,
    val user: UserSummary
)
data class UserSummary(val id: Long, val name: String)

class OrderWithUserMapper : RowMapper<OrderWithUser> {
    override fun mapRow(rs: ResultSet, rowNum: Int): OrderWithUser {
        val user = UserSummary(
            id   = rs.getLong("u_id"),
            name = rs.getString("u_name")
        )
        return OrderWithUser(
            orderId = rs.getLong("o_id"),
            price   = rs.getLong("o_price"),
            user    = user
        )
    }
}

// SQL에서 반드시 컬럼에 alias 줘서 충돌 피하기
val sql = """
  select o.id as o_id, o.price as o_price,
         u.id as u_id, u.name as u_name
  from orders o join users u on u.id = o.user_id
"""

val list = jdbcClient.sql(sql).query(OrderWithUserMapper()).list()
```
-  `여러 행 = 부모 하나 + 자식 여러 개`로 모아야 할 때 → **ResultSetExtractor (그룹핑)**
```kotlin
val sql = """
  select o.id as o_id, o.price as o_price,
         i.id as item_id, i.sku as item_sku
  from orders o join order_items i on i.order_id = o.id
  where o.id = :orderId
"""

val order = jdbcClient.sql(sql)
    .param("orderId", id)
    .query { rs ->
        var parent: Order? = null
        val items = mutableListOf<Item>()
        while (rs.next()) {
            if (parent == null) {
                parent = Order(
                    id = rs.getLong("o_id"),
                    price = rs.getLong("o_price"),
                    items = items
                )
            }
            items += Item(
                id = rs.getLong("item_id"),
                sku = rs.getString("item_sku")
            )
        }
        parent ?: error("not found")
    }
    .single()
```