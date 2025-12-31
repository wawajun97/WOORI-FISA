# Log4j
- java에서 로그를 찍기 위해 사용하는 도구

---

## 📝 Log4j 설정 및 사용 가이드

### 1. 📦 의존성 추가 (Maven)

`pom.xml`에 아래 의존성들을 추가

```xml
<dependencies>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.18.30</version>
        <scope>provided</scope>
    </dependency>

    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>2.0.9</version>
    </dependency>

    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-core</artifactId>
        <version>2.20.0</version>
    </dependency>
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-api</artifactId>
        <version>2.20.0</version>
    </dependency>

    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-slf4j2-impl</artifactId>
        <version>2.20.0</version>
    </dependency>
</dependencies>
```

### 내부 로깅 설정 (warn 이상일 때만 로그 기록)
status = warn
name = PropertiesConfig

### 1. Appender 설정: 로그를 어디에 출력할 것인가? (여기서는 콘솔)
appender.console.type = Console
appender.console.name = LogToConsole
appender.console.layout.type = PatternLayout
appender.console.layout.pattern = %d{yyyy-MM-dd HH:mm:ss} [%t] %-5p %c{1} - %m%n

### 2. RootLogger 설정: 어떤 수준의 로그부터 출력할 것인가?
### 레벨 순서: TRACE < DEBUG < INFO < WARN < ERROR < FATAL
rootLogger.level = info
rootLogger.appenderRef.stdout.ref = LogToConsole

### 사용법

```java
import lombok.extern.slf4j.Slf4j;

@Slf4j // 자동으로 private static final Logger log 생성
public class LogTest {

    public void logExample(String message) {
        // 1. 중괄호 {} 를 사용하는 파라미터 바인딩 (성능상 이점)
        log.info("입력된 메시지: {}", message);

        // 2. 다양한 로그 레벨 활용
        log.error("에러 발생!");
        log.warn("경고 메시지");
        log.info("정보성 로그");
        log.debug("디버깅용 로그 (설정이 INFO라면 출력되지 않음)");
        log.trace("상세 추적 로그");
    }
}
```
