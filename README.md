# 📦 WMS Project

창고 관리(Warehouse Management System, WMS)는 가구 재고 및 입출고 현황을 효율적으로 관리하기 위한 Java 기반 콘솔 애플리케이션입니다. JDBC를 통해 MySQL 데이터베이스와 연동되며, MVC 아키텍처 패턴을 적용했습니다.

---

## 🧭 프로젝트 개요

기업의 창고 관리 업무는 재고의 정확성과 실시간 입출고 관리가 핵심입니다. 본 시스템은 가구류 제품을 대상으로 다음과 같은 문제를 해결합니다.

- 📉 재고 불일치 문제 해소
- 🕒 입출고 이력의 실시간 관리
- 👤 사용자 권한에 따른 접근 제어
- 🧩 창고별, 섹션별 물류 관리 체계화

---

## 🛠️ 기술 스택

- **Language** : Java (JDK 17)
- **Database** : MySQL 8.0.22
- **Database Access** : JDBC
- **Tooling** : IntelliJ IDEA, GitHub, Workbench, Railway

---

## 📂 프로젝트 구조

```
src/
 ┣ controller/      # 사용자 요청 처리
 ┣ service/         # 비즈니스 로직 인터페이스
 ┣ serviceImpl/     # Service 구현체
 ┣ dao/             # 데이터 접근 인터페이스
 ┣ daoImpl/         # DAO 구현체 (JDBC)
 ┣ domain/          # VO, DTO 클래스
 ┣ Session/         # 세션 관리
 ┗ view/            # CLI 기반 UI
```

---

## 🔀 Git Flow 전략

4인 팀 프로젝트로 **feature → develop → main** 순서로 병합하는 Git Flow 전략을 적용했습니다.

- **main** : 배포용 안정 브랜치
- **develop** : 통합 개발 브랜치
- **feature/** : 기능별 개발 브랜치
  - `feature/inbound-outbound` : 입출고 관리
  - `feature/inventory` : 재고 관리
  - `feature/member-board` : 회원/로그인 관리
  - `feature/warehouse` : 창고 관리

### 💡 커밋 컨벤션

- `feat`: 새로운 기능 추가
- `fix`: 버그 수정
- `refactor`: 코드 리팩토링
- `chore`: 환경 설정 및 기타
- `docs`: 문서 수정

---

## ✨ 주요 기능

### 🧾 입출고 관리
상품 입고 및 출고 내역 등록, 입출고 이력 조회, 상태 변경 기능

### 📦 재고 관리
창고별 재고 현황 조회, 상품별 재고 수량 관리, 재고 실사 기능

### 👤 회원 관리
신규 사용자 등록, 로그인/로그아웃, 권한별 접근 제어

### 🏭 창고 관리
창고 및 섹션 등록/수정/삭제, 창고별 상품 분류 및 위치 관리, 용량 정보 조회

---

## 👨‍💻 담당 역할

### 🗂️ ERD 설계
팀원들과 함께 요구사항을 분석하고 데이터베이스 설계를 주도했습니다. 창고, 재고, 입출고, 회원 테이블 간의 관계를 정의하고 정규화를 통해 데이터 무결성을 확보했습니다.

### 🏭 창고 관리 모듈 구현
창고 관리 기능을 전담하여 **Controller - Service - DAO - View** 계층을 완성했습니다.

#### 주요 구현 내용

**1. MVC 패턴 기반 계층 분리**
- **Controller**: 사용자 요청을 받아 Service로 전달하고 결과 반환
- **Service**: 비즈니스 로직 처리 (창고 타입 변환, 유효성 검증)
- **DAO**: MySQL Stored Procedure 호출을 통한 CRUD 작업
- **View**: 콘솔 기반 사용자 인터페이스 구현

**2. 싱글톤 패턴 적용**
```java
private static WarehouseController instance = new WarehouseController();
public static WarehouseController getInstance() {
    return instance;
}
```
Controller와 Service 계층에 싱글톤 패턴을 적용하여 메모리 효율성을 높이고 전역 접근성을 확보했습니다.

**3. Stored Procedure 활용**
데이터베이스 로직을 Stored Procedure로 구현하여 네트워크 트래픽을 최소화하고 성능을 향상시켰습니다.
- `usp_Warehouse_Insert`: 창고 등록
- `usp_Warehouse_UpdateStatus`: 운용 상태 토글
- `usp_warehouse_selectByType/Name/Location`: 다양한 조건 검색

**4. 권한별 접근 제어**
총관리자, 창고관리자, 일반회원 권한에 따라 메뉴와 기능을 차등 제공했습니다.
- **총관리자**: 창고 등록, 상태 수정, 전체 조회
- **창고관리자**: 조회 기능만 제공
- **일반회원**: 운용 중인 창고만 조회 가능

**5. 입력 검증 및 예외 처리**
사용자 입력에 대한 유효성 검사를 View 계층에서 수행하여 안정성을 확보했습니다.
```java
// 창고 용량 검증
while (true) {
    try {
        capacity = Integer.parseInt(reader.readLine().trim());
        if (capacity <= 0) {
            System.out.println(":: 용량은 1 이상이어야 합니다. ::");
            continue;
        }
        break;
    } catch (NumberFormatException e) {
        System.out.println(":: 숫자만 입력 가능합니다. ::");
    }
}
```

**6. JDBC 리소스 관리**
Try-with-resources 구문을 활용하여 Connection, Statement, ResultSet 자원을 안전하게 관리했습니다.

---

## 💡 개발 포인트

- MVC 아키텍처를 통한 계층적 구조 설계
- Singleton 패턴으로 객체 생성 최적화
- Stored Procedure 활용으로 DB 성능 향상
- Git Flow 기반 협업으로 코드 충돌 최소화
- Try-with-resources를 통한 JDBC 리소스 관리

---

## 🚀 향후 개선 방향

- GUI 기반 화면으로 확장 (JavaFX or Spring Boot Web)
- 창고 용량 대비 재고 현황 시각화 기능 추가
- REST API 도입을 통한 외부 시스템 연동
- 창고별 담당자 세부 권한 관리 기능 강화
