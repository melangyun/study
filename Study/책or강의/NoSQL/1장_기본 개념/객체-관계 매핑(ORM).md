Patterns of Enterprise Application Architecure (PoEAA)기준 객체 - 관계 불일치 문제를 해결하는 패턴
# 1.  Active Record
- 객체가 자기 자신의 CRUD 책임을 가짐
- 도메인 모델과 DB 접근 로직이 하나의 클래스에 통합
```kotlin
class User {
  private val id:Long
  private val name:String

  fun save(conn: Connection){
    val stmt = conn.prepareStatement("INSERT INTO user (name) VALUES (?)")
    stmt.setString(1, name)
    stmt.executeUpdate();
  }

  fun findById(conn: Connection, id: Long):User {
    val stmt = conn.prepareStatement("SELECT id, name FROM users WHERE id = ?");
    stmt.setLong(1, id);
	val rs:ResultSet = stmt.executeQuery();
	if (rs.next()) {
		User user = new User();
		user.id = rs.getLong("id");
		user.name = rs.getString("name");
		return user;
	}
	return null;
  }
}
```

# 2. Data Mapper
- 객체는 비즈니스 로직을 담당. 저장 책임은 X
```java
@Entity
public class User {
    @Id
    @GeneratedValue
    private Long id;
    private String name;

    // getter/setter 생략
}

// 데이터 접근을 담당하는 Repository
public interface UserRepository extends JpaRepository<User, Long> {
    Optional<User> findByName(String name);
}
```
User에 대한 매핑은 JPA가 담당.
복잡한 도메인 구조에 강력함

# 3. Table Data Gateway
각 테이블마다 접근 클래스를 둠(일종의 DAO)
도메인 객체는 그냥 DTO역할, 저장 로직은 별도 객체에서 처리

```java
// DTO
public class User {
    private Long id;
    private String name;
}

// Gateway (DAO)
public class UserGateway {
    private final DataSource dataSource;

    public UserGateway(DataSource dataSource) {
        this.dataSource = dataSource;
    }

    public void insert(User user) throws SQLException {
        try (Connection conn = dataSource.getConnection()) {
            PreparedStatement stmt = conn.prepareStatement("INSERT INTO users (name) VALUES (?)");
            stmt.setString(1, user.getName());
            stmt.executeUpdate();
        }
    }

    public User findById(Long id) throws SQLException {
        try (Connection conn = dataSource.getConnection()) {
            PreparedStatement stmt = conn.prepareStatement("SELECT * FROM users WHERE id = ?");
            stmt.setLong(1, id);
            ResultSet rs = stmt.executeQuery();
            if (rs.next()) {
                User user = new User();
                user.setId(rs.getLong("id"));
                user.setName(rs.getString("name"));
                return user;
            }
            return null;
        }
    }
}
```