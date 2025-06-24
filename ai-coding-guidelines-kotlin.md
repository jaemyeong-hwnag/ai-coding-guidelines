# AI Coding Guidelines (Kotlin)

이 문서는 Kotlin 프로젝트에 특화된 개발 가이드라인입니다.
공통 가이드(ai-coding-guidelines-common.md)와 함께 참고하세요.

## Kotlin 특화 개발 원칙

### 1. Kotlin 언어 특성 활용
- **Null Safety**: Nullable 타입(`?`)과 Non-null 타입(`!!`) 적절히 활용
- **Smart Casts**: 타입 체크 후 자동 캐스팅 활용
- **Extension Functions**: 기존 클래스 확장 기능 활용
- **Data Classes**: 데이터 전달용 클래스는 data class 사용
- **Sealed Classes**: 제한된 타입 계층 구조에 활용
- **Coroutines**: 비동기 처리에 활용 (RxJava 대신)

### 2. Kotlin 네이밍 컨벤션
```kotlin
// ✅ 올바른 예시
class UserService
fun validateUserInput()
val userEmail: String
const val MAX_RETRY_COUNT = 3

// ❌ 잘못된 예시
class userService
fun ValidateUserInput()
val email: String
const val maxRetryCount = 3
```

### 3. Kotlin 특화 하드코딩 제거
```kotlin
// ✅ 올바른 예시
object HttpStatusConstants {
    const val OK = "200"
    const val CREATED = "201"
    const val BAD_REQUEST = "400"
}

// ❌ 잘못된 예시
fun processResponse() {
    if (status == "200") { // 하드코딩
        // 처리 로직
    }
}
```

### 4. Kotlin 테스트 작성
```kotlin
// JUnit 5 + MockK 사용
@ExtendWith(MockKExtension::class)
class UserServiceTest {
    
    @MockK
    private lateinit var userRepository: UserRepository
    
    @InjectMocks
    private lateinit var userService: UserService
    
    @Test
    fun `사용자 생성 성공 시 User 객체 반환`() {
        // given
        val userRequest = UserRequest("test@example.com", "password")
        val expectedUser = User(1L, "test@example.com")
        every { userRepository.save(any()) } returns expectedUser
        
        // when
        val result = userService.createUser(userRequest)
        
        // then
        assertThat(result).isEqualTo(expectedUser)
        verify { userRepository.save(any()) }
    }
}
```

### 5. Kotlin 최신 기술/아키텍처
- **Spring Boot 3.x + Kotlin**: 최신 Spring Boot와 Kotlin 조합
- **Kotlin DSL**: Gradle 빌드 스크립트에 Kotlin DSL 사용
- **Kotlin Coroutines**: 비동기 처리에 활용
- **Kotlin Serialization**: JSON 직렬화/역직렬화
- **Kotlinx DateTime**: 날짜/시간 처리
- **Arrow**: 함수형 프로그래밍 라이브러리

### 6. Kotlin 레거시 패턴 지양
```kotlin
// ❌ 레거시 패턴
class OldService {
    fun process(data: String): String? {
        if (data == null) return null
        if (data.isEmpty()) return null
        return data.uppercase()
    }
}

// ✅ 최신 Kotlin 패턴
class ModernService {
    fun process(data: String?): String? = 
        data?.takeIf { it.isNotEmpty() }?.uppercase()
}
```

### 7. Kotlin 테스트 용이성
```kotlin
// ✅ 테스트 친화적 구조
interface UserRepository {
    suspend fun save(user: User): User
    suspend fun findById(id: Long): User?
}

class UserService(
    private val userRepository: UserRepository,
    private val passwordEncoder: PasswordEncoder
) {
    suspend fun createUser(request: UserRequest): User {
        val encodedPassword = passwordEncoder.encode(request.password)
        val user = User(email = request.email, password = encodedPassword)
        return userRepository.save(user)
    }
}
```

### 8. Kotlin 빌드 및 테스트 자동화
```kotlin
// build.gradle.kts
plugins {
    kotlin("jvm") version "1.9.0"
    kotlin("plugin.spring") version "1.9.0"
    kotlin("plugin.jpa") version "1.9.0"
    id("org.springframework.boot") version "3.2.0"
}

dependencies {
    implementation("org.jetbrains.kotlin:kotlin-stdlib-jdk8")
    implementation("org.jetbrains.kotlin:kotlin-reflect")
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-core")
    
    testImplementation("org.jetbrains.kotlin:kotlin-test")
    testImplementation("io.mockk:mockk:1.13.0")
    testImplementation("org.jetbrains.kotlinx:kotlinx-coroutines-test")
}
```

## AI 실행 체크리스트 (Kotlin)

### 코드 수정 전
- [ ] 연관 파일 영향도 분석
- [ ] 프로젝트 목적 부합성 확인
- [ ] 기존 테스트 코드 검토
- [ ] **Kotlin 언어 특성 활용 여부 확인**
    - Null Safety, Smart Casts, Extension Functions 등 적절히 활용
    - Java 스타일 코드를 Kotlin 스타일로 개선
- [ ] **Kotlin 최신 기술/아키텍처 적용 여부 확인**
    - Spring Boot 3.x, Kotlin DSL, Coroutines 등 최신 기술 사용
    - 레거시 패턴(Java 스타일, RxJava 등) 사용 금지
- [ ] **Kotlin 테스트 용이성 확인**
    - MockK, Coroutines Test 등 Kotlin 테스트 도구 활용
    - 의존성 주입, 인터페이스 분리 등 테스트 친화적 구조

### 코드 수정 중
- [ ] Kotlin 네이밍 컨벤션 준수
- [ ] Kotlin 특화 하드코딩 제거
- [ ] Kotlin 언어 특성 활용
- [ ] 가독성 개선

### 코드 수정 후
- [ ] 빌드 실행 및 성공 확인
- [ ] 테스트 실행 및 성공 확인
- [ ] 연관 파일 동기화
- [ ] 문서 업데이트

## Kotlin 예시 시나리오

### 시나리오 1: 새로운 API 응답 클래스 추가
```
1. Data class로 응답 객체 생성
2. Null Safety 고려한 타입 정의
3. Kotlin Serialization 어노테이션 추가
4. MockK를 사용한 테스트 코드 작성
5. 빌드 및 테스트 실행
6. 가이드라인 업데이트 (필요시)
```

### 시나리오 2: 에러 코드 추가
```
1. Sealed class로 에러 타입 정의
2. HttpStatusConstants에 관련 상수 추가
3. MockK를 사용한 ErrorResponse 테스트 업데이트
4. 관련 문서 업데이트
5. 빌드 및 테스트 실행
```

### 시나리오 3: 레거시 Java 코드를 Kotlin으로 개선
```
1. Java 스타일 코드를 Kotlin 스타일로 리팩토링
2. Null Safety, Extension Functions 등 Kotlin 특성 활용
3. RxJava를 Coroutines로 마이그레이션
4. MockK를 사용한 테스트 코드 작성
5. 빌드 및 테스트 실행
6. 가이드라인 업데이트 (필요시)
```

## 주의사항

- **Kotlin 특성 활용**: Java 스타일 코드를 Kotlin 스타일로 개선
- **최신 기술 우선**: Spring Boot 3.x, Coroutines 등 최신 기술 사용
- **테스트 도구**: MockK, Coroutines Test 등 Kotlin 전용 테스트 도구 활용
- **Null Safety**: Nullable 타입을 적절히 활용하여 안전성 확보

---

※ 공통 가이드: ai-coding-guidelines-common.md 참고 