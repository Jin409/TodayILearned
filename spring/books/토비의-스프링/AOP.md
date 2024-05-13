# 트랜잭션 코드의 분리

- 트랜잭션의 경계는 비지니스 로직의 전후이므로 UserService 에 위치하게 된다.

## 메소드 분리

```java
public void upgradeLevels() throws Exception {

    // 트랜잭션 시작
    Transactionstatus status = this.transactionlanager.getTransaction(new DefaultTransactionDefinition());

    // 비지니스 로직
    try {
        List<User> users = userDao.getA11();
        for (User user : users) {
            if (canUpgradeLevel(user)) {
                upgradeLevel(user);
            }
        }

        // 트랜잭션 종료
        this.transactionManager.commit(status);
    } catch (Exception e) {
        this.transactionManager.rollback(status);
        throw e;
    }
}
```

- 비지니스 로직 코드를 사이에 두고 트랜잭션의 시작과 종료가 앞뒤로 위치하고 있다.
    - 또한, 비지니스 - 트랜잭션 코드 간에 주고받는 정보가 없다.

```java
public void upgradeLevels() throws Exception {

    // 트랜잭션 시작
    Transactionstatus status = this.transactionlanager.getTransaction(new DefaultTransactionDefinition());

    // 비지니스 로직
    try {
        upgradeLevelsInternal();

        // 트랜잭션 종료
        this.transactionManager.commit(status);
    } catch (Exception e) {
        this.transactionManager.rollback(status);
        throw e;
    }
}

public void upgradeLevelsInternal() {
    List<User> users = userDao.getA11();
    for (User user : users) {
        if (canUpgradeLevel(user)) {
            upgradeLevel(user);
        }
    }
}
```

- 독립적으로 메서드를 분리했다.

## DI 를 이용한 클래스의 분리

- UserService 밖으로 트랜잭션 코드를 뽑아낼 수는 없을까?
    - UserService 밖으로 트랜잭션 코드를 뽑아내면 된다.

### DI 적용을 이용한 트랜잭션 분리

- UserService 밖으로 트랜잭션 코드를 빼버리면, UserService 를 사용하는 클라이언트 코드에서는 트랜잭션 기능이 빠진 UserService 를 사용하게 된다.
    - 이는 클라이언트와 UserService 사이에 인터페이스를 추가해주면 된다.
    - 이렇게 하면, 런타임 시에 구현 클래스를 바꿔 끼워 사용할 수 있다.
        - ex) 테스트 시에는 테스트 구현 클래스 / 정식 운영 시에는 정규 구현 클래스

### UserService 인터페이스 도입

```java
public interface UserService {
    void add(User user);

    void upgradeLevels();
}
```

### 분리된 트랜잭션 기능

```java
public class UserServiceTx implements UserService {
    UserService userService;
    PlatformTransactionManager transactionManager;

    public void setTransactionManager(PlatformTransactionManager transactionManager) {
        this.transactionManager = transactionManager;
    }

    public void setUserService(UserService userService) {
        this.userService = userService;
    }

    public void add(User user) {
        userService.add(user);
    }

    public void upgradeLevels() {
        TransactionStatus status = this.transactionManager
•getTransaction(new DefaultTransactionDefinition());
        try {
            userService.upgradeLevels();
            this.transactionManager.commit(status);
        } catch (RuntimeException e) {
            this.transactionManager.rollback(status);
            throw e;
        }
    }
}
```

- 비지니스로직은 UserService 에 위임한다.

### 트랜잭션 경계설정 코드 분리의 장점

- 비지니스 로직을 담당하고 있는 UserServiceImpl 에 대한 코드 작성 시에 트랜잭션과 같은 기술적인 부분을 신경쓰지 않아도 된다.
- 비지니스 로직에 대한 테스트를 쉽게 만들 수 있다.
