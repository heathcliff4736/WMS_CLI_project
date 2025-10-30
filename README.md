# 📦 WMS Project

창고 관리(Warehouse Management System, WMS)는 가구 재고 및 입출고 현황을 효율적으로 관리하기 위한 시스템입니다.
본 프로젝트는 Java 기반 콘솔 애플리케이션으로, JDBC를 통해 MySQL 데이터베이스와 연동되며,
MVC 아키텍처 패턴을 적용해 유지보수성과 확장성을 확보했습니다.

---
## 🧭 프로젝트 개요

기업의 창고 관리 업무는 재고의 정확성과 실시간 입출고 관리가 핵심입니다.
본 시스템은 가구류 제품을 대상으로 다음과 같은 문제를 해결하는 것을 목표로 합니다.

📉 재고 불일치 문제 해소

🕒 입출고 이력의 실시간 관리

👤 사용자 권한에 따른 접근 제어

🧩 창고별, 섹션별 물류 관리 체계화
---

## 🛠️ 기술 스택

- Language : Java (JDK 17)
- Database : MySQL 8.0.22
- Database Access : JDBC
- Tooling : IntelliJ IDEA, GitHub, Workbench, Railway

---

## 📂 프로젝트 구조

```
src/
 ┣ controller/      # 사용자 요청 처리 (입출고, 재고, 회원, 창고 등)
 ┣ service/         # 비즈니스 로직 인터페이스
 ┣ serviceImpl/     # Service 구현체 (실제 로직 수행)
 ┣ dao/             # 데이터 접근 인터페이스
 ┣ daoImpl/         # DAO 구현체 (JDBC 활용)
 ┣ domain/          # VO, DTO 클래스 (데이터 객체)
 ┣ Session/         # 사용자 로그인 및 세션 관리
 ┗ view/            # CLI 기반 UI (콘솔 입출력 담당)
```

---

## 🔀 Git Flow 전략

우리 팀(4명)의 협업을 위해 Git Flow 전략 및 커밋 컨벤션을 사용했습니다.
**feature → develop → main** 순서로 merge 진행

- main: 실제 서비스 배포용 안정 브랜치
- develop: 기능 통합 브랜치
- feature/: 새로운 기능 개발 브랜치
    - feature/inbound-outbound : 입출고 관리
    - feature/inventory : 재고 관리
    - feature/member-board : 회원/로그인 관리
    - feature/warehouse : 창고 관리

---

## ✨ 주요 기능

🧾 입출고 관리 (Inbound / Outbound)

상품 입고 및 출고 내역 등록

상품별 입출고 이력 조회

입출고 상태 변경 및 수정 기능

📦 재고 관리 (Inventory)

창고별 재고 현황 조회

상품별 재고 수량 관리

재고 실사 및 이상 수량 감지 기능

👤 회원 / 로그인 관리 (Member & Auth)

신규 사용자 등록

로그인 / 로그아웃 처리

관리자, 일반 사용자 등 권한별 접근 제어

🏭 창고 관리 (Warehouse)

창고 및 섹션 등록 / 수정 / 삭제

창고별 상품 분류 및 위치 관리

창고 용량 및 섹션 정보 조회

---

##🔀 Git Flow 전략

4인 팀 프로젝트로 진행되었으며, 체계적인 협업과 코드 통합을 위해 Git Flow 전략을 사용했습니다.
모든 기능은 feature 브랜치에서 개발 후 develop에 통합, 이후 안정화 단계를 거쳐 main으로 병합합니다.

main : 실제 서비스 배포용 안정 브랜치

develop : 통합 개발 브랜치

feature/ : 개별 기능 단위 개발 브랜치

feature/inbound-outbound : 입출고 관리

feature/inventory : 재고 관리

feature/member-board : 회원 및 로그인 관리

feature/warehouse : 창고 관리

💡 커밋 컨벤션

feat: 새로운 기능 추가

fix: 버그 수정

refactor: 코드 리팩토링

chore: 환경 설정 및 기타 수정

docs: 문서 수정

---

##💡 개발 포인트

MVC 아키텍처를 통한 계층적 구조 설계

JDBC 커넥션 관리 최적화로 효율적 DB 접근

Service / DAO 분리를 통한 비즈니스 로직 독립성 확보

Git Flow 기반 협업으로 코드 충돌 최소화 및 역할 분담 명확화

---

##🚀 향후 개선 방향

GUI 기반 화면으로 확장 (JavaFX or Spring Boot Web)

입출고 내역 및 재고 통계 시각화 기능 추가

REST API 도입을 통한 외부 시스템 연동

사용자 권한 세분화 (예: 관리자 / 창고 담당자 / 일반 사용자)


