# AI Coding Guidelines

AI가 개발할 때 고려해야 할 가이드라인 모음입니다.

## 📋 가이드라인 파일 구조

### 1. 공통 가이드 (모든 언어/플랫폼 적용)
- **파일**: `ai-coding-guidelines-common.md`
- **적용 범위**: 모든 개발 프로젝트 (언어/플랫폼 무관)
- **내용**: 개발 원칙, 네이밍, 하드코딩 제거, 테스트, 자동화, 문서화, 최신 기술/아키텍처, 레거시 지양, 테스트 용이성

### 2. 언어별 특화 가이드

#### Java 프로젝트
- **파일**: `ai-coding-guidelines-java.md`
- **적용 범위**: Java/Spring Boot 프로젝트
- **내용**: Java 특화 네이밍, Spring Boot, JUnit, Mockito, Gradle, Maven 등

#### Kotlin 프로젝트
- **파일**: `ai-coding-guidelines-kotlin.md`
- **적용 범위**: Kotlin/Spring Boot 프로젝트
- **내용**: Kotlin 언어 특성(Null Safety, Coroutines), MockK, Kotlin DSL 등

## 🚀 AI 적용 방법

### 새 프로젝트 시작 시
1. **공통 가이드 먼저 확인**: `ai-coding-guidelines-common.md` 읽기
2. **언어별 가이드 추가 확인**: 해당 언어의 특화 가이드 읽기
3. **프로젝트 설정**: 가이드라인에 따라 프로젝트 구조, 빌드 도구, 테스트 설정

### 기존 프로젝트 개선 시
1. **현재 상태 점검**: 가이드라인 체크리스트로 현재 상태 평가
2. **우선순위 결정**: 컴파일 오류 → 테스트 실패 → 하드코딩 → 네이밍 → 가독성 순서
3. **단계별 개선**: 한 번에 하나씩 체계적으로 개선

## 📝 AI 실행 체크리스트

### 코드 수정 전
- [ ] 연관 파일 영향도 분석
- [ ] 프로젝트 목적 부합성 확인
- [ ] 기존 테스트 코드 검토
- [ ] 최신 기술/아키텍처, 레거시 여부 점검
- [ ] 테스트 용이성 점검
- [ ] 네이밍/하드코딩/가독성/문서화/자동화 등 전반적 품질 점검

### 코드 수정 중
- [ ] 네이밍 규칙 준수
- [ ] 하드코딩 제거
- [ ] 가독성 개선
- [ ] 언어별 특화 가이드 적용

### 코드 수정 후
- [ ] 빌드 실행 및 성공 확인
- [ ] 테스트 실행 및 성공 확인
- [ ] 연관 파일 동기화
- [ ] 문서 업데이트

## 🔧 자동화 원칙

- **즉시 실행**: 컴파일 오류, 빌드 실패 발견 시 즉시 수정
- **높은 우선순위**: 테스트 실패, 하드코딩 발견 시 즉시 수정
- **중간 우선순위**: 네이밍 개선, 가독성 향상
- **낮은 우선순위**: 문서 업데이트, 예시 추가

## 📚 사용 예시

### Java 프로젝트
```bash
# 1. 공통 가이드 확인
cat ai-coding-guidelines-common.md

# 2. Java 특화 가이드 확인
cat ai-coding-guidelines-java.md

# 3. 가이드라인에 따라 개발 진행
```

### Kotlin 프로젝트
```bash
# 1. 공통 가이드 확인
cat ai-coding-guidelines-common.md

# 2. Kotlin 특화 가이드 확인
cat ai-coding-guidelines-kotlin.md

# 3. 가이드라인에 따라 개발 진행
```

## ⚠️ 주의사항

- **변경 불가능한 전제조건**: 레이아웃 변경, 전제조건 추가는 기존 전제조건의 핵심내용들은 변경하지 않는다
- **자동화 원칙**: 사용자가 명시적으로 금지하지 않는 한 모든 문제를 자동으로 해결
- **품질 우선**: 코드 품질과 가독성을 최우선으로 고려

## 🔗 관련 파일

- [ai-coding-guidelines-common.md](./ai-coding-guidelines-common.md) - 공통 개발 가이드
- [ai-coding-guidelines-java.md](./ai-coding-guidelines-java.md) - Java 특화 가이드
- [ai-coding-guidelines-kotlin.md](./ai-coding-guidelines-kotlin.md) - Kotlin 특화 가이드

---

**AI 개발 시 이 가이드라인을 참고하여 일관성 있고 품질 높은 코드를 작성하세요!** 
