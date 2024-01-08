# final 변수와 상수

변수에 final 키워드가 붙으면 더는 변경할 수 없다.

## final 지역 변수

```java
public class FinalMain {
    public static void main() {
        final int data1;
        data1 = 10; // 최초 할당
        data1 = 8; // 컴파일 에러 발생

        final int data2 = 10; // 선언과 동시에 할당
        data2 = 20; // 컴파일 오류
    }

    public void method(final int parameter) {
        parameter = 10; // 불가능
    }
}
```

final 이 붙은 지역 변수는 최초 할당한 이후에 값을 변경하고자 하면, 컴파일 에러가 발생한다.
또한, 인수로 넘어간 final 변수는 중간에 변경이 불가능하다.

## final 멤버 변수

### 생성자 초기화

```java
public class ConstructInit {
    final int value;

    public ConstructInit(int value) {
        this.value = value;
    }
}
```

멤버 변수에 final 이 붙으면 생성자를 통해서만 초기화가 가능하다.

### 필드 초기화

```java
public class FieldInit {
    static final int CONST_VALUE = 10; // better - 메모리 낭비 x
    final int value = 10;

    public FieldInit() {
        // this.value = value; 불가능!
    }
}
```

위와 같이, 멤버 변수가 선언과 동시에 할당되었다면, 생성자를 통해서도 값을 변경할 수 없다.
이는 객체마다 값이 다르지 않은데, 같은 값을 할당하므로 메모리 상의 낭비가 발생할 수 있다.
static final (상수) 는 이런 상황에서 메서드 영역에 정적으로 메모리가 할당되기 때문이다.

## final 상수

항상 일정한 값을 갖는 수
변하지 않는 고정된 값

### 특징

- 대문자를 사용한다
- 필드를 직접 접근해서 사용한다.
- 상수는 값을 변경할 수 없다. 따라서 접근해도 어차피 변하지 않기 때문에 직접 접근해도 괜찮다.

```java
public class ConstantMain1 {
    public static void main(String[] args) {
        System.out.println("프로그램 최대 참여자 수 " + 1000);
        int currentUserCount = 999;
        process(currentUserCount++);
        process(currentUserCount++);

        process(currentUserCount++);
    }

    private static void process(int currentUserCount) {
        System.out.println("참여자 수:" + currentUserCount);
        if (currentUserCount > 1000) {
            System.out.println("대기자로 등록합니다.");
        } else {
            System.out.println("게임에 참가합니다.");
        }
    }
}
```

위와 같은 상황에서 1000을 2000으로 변경하고 싶다면 어떻게 해야 할까?
변경되어야 하는 지점이 두개가 존재한다. 또한, 가독성 측면에서도 이점이 없다.
위의 코드에서 1000을 `매직 넘버`라고 한다.

이러한 상황에서 1000명은 고정된 값이기 때문에 상수를 사용하는 것이 적절하다.

```java
public class ConstantMain1 {
    public static void main(String[] args) {
        System.out.println("프로그램 최대 참여자 수 " + Constant.MAX_USERS);
        int currentUserCount = 999;
        process(currentUserCount++);
        process(currentUserCount++);

        process(currentUserCount++);
    }

    private static void process(int currentUserCount) {
        System.out.println("참여자 수:" + currentUserCount);
        if (currentUserCount > Constant.MAX_USERS) {
            System.out.println("대기자로 등록합니다.");
        } else {
            System.out.println("게임에 참가합니다.");
        }
    }
}
```

위처럼 상수를 사용하는 것이 적절하다.

# final 변수와 참조

final 은 변수의 값을 변경하지 못하도록 한다.

- 기본형 변수 : 값을 변경할 수 없다.
- 참조형 변수 : 참조값을 변경할 수 없다.

```java
public class FinalRefMain {
    public static void main(String[] args) {
        final Data data = new Data();
        //data = new Data(); //final 변경 불가 컴파일 오류
        // 참조 대상의 값은 변경 가능 
        data.value = 10;
        System.out.println(data.value);
        data.value = 20;
        System.out.println(data.value);
    }
}
```

위의 변경은 참조값을 변경하는 것이 아니라, 참조하는 대상의 값을 변경하는 것이므로 변경이 가능하다.
