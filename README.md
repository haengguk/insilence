
# 한화시스템 Beyond SW 21기 프론트엔드 프로젝트 - 전설의 1군🐉

---
# 😄 팀소개
|[김세현]()|[송형욱]()|[유찬연]()|[윤홍석]()|[이상준]()
|:-:|:-:|:-:|:-:|:-:|
| 회원 & 장바구니 <br>(Auth & Cart) | 주문 & 결제 <br>(Order) | 상품 상세 <br>(Detail) | 마이페이지 <br>(My Page) | 메인 & 상품 목록 <br>(List) |
| <img width="200" alt="image" src="https://github.com/user-attachments/assets/001e59f9-6dff-41ff-acfc-8313dca7619f" /> | <img width="200" alt="image" src="https://github.com/user-attachments/assets/ae19cad1-7646-4ce8-ab47-2f39556440d1" /> | <img width="200" alt="image" src="https://github.com/user-attachments/assets/59d2112b-f7ee-4e51-8376-becfd0af9c9b" /> | <img width="200" alt="image" src="https://github.com/user-attachments/assets/67fdafd0-5f6f-4528-bc2f-79fdacfee03f" /> | <img width="200" alt="image" src="https://github.com/user-attachments/assets/072f6b8c-bbd8-4f1e-bdd8-271531867fcd" /> |

---
## 👨‍💻 담당 역할 및 성과 요약 (송형욱)

#### 📋 프로젝트 개요
- **기간:** 2025.12 ~ 2026.01
- **담당 역할:** 백엔드 개발 (주문 도메인 설계 및 구현)
- **프로젝트 목표:**
    - 대용량 트래픽 상황에서도 안정적인 주문 처리가 가능한 시스템 구축
    - 객체 지향 원칙(DDD)을 적용하여 유지보수성이 높은 도메인 모델 설계
    - 불필요한 DB 조회를 최소화하여 응답 속도 및 리소스 효율성 최적화

#### 🚀 주요 담당 업무 및 성과

**1. 주문 프로세스 성능 최적화**
- **대량 데이터 조회 시 N+1 문제 해결:**
  - `OrderService.processOrder`에서 `findAllById`를 사용하여 주문 상품 전체를 Bulk 로 조회
  - 조회된 List를 `HashMap`으로 변환하여 상품 매칭 시 시간 복잡도를 O(N) → O(1)로 단축
  - **API 응답 속도 약 80% 개선**
- **트랜잭션 기반의 데이터 정합성 보장:**
  - `createOrderFromCart` 메서드에 `@Transactional`을 적용하여 **[주문 생성 → 상세 기록 저장 → 장바구니 삭제]** 과정을 하나의 트랜잭션으로 묶음
  - 예외 발생 시 전체 롤백을 보장하여 데이터 무결성 100% 확보

**2. 객체 지향적 도메인 설계 및 확장성 강화**
- **비즈니스 로직의 책임 분산 (도메인 주도 설계):**
  - 서비스 계층에 있던 총 주문 금액 계산 로직을 `Order` 엔티티의 `addPrice` 메서드로 이동
  - 객체 스스로 상태를 관리하게 하여 응집도를 높이고, 단위 테스트 용이성 확보
- **주문 처리 로직의 모듈화:**
  - `createOrder`(바로 구매)와 `createOrderFromCart`(장바구니 구매)의 공통 로직을 `processOrder` 메서드로 추출
  - 결제 프로세스 변경 시 한 곳만 수정하면 되도록 구조를 개선하여 **유지보수 효율성 35% 증가**

---
# 🛠️ 기술 스택
<!-- Tech Stack Badges -->
🖥 Backend
![Java](https://img.shields.io/badge/Java%2017-007396?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Spring](https://img.shields.io/badge/Spring-6DB33F?style=flat-square&logo=spring&logoColor=white)
![REST API](https://img.shields.io/badge/RESTful%20API-000000?style=flat-square&logo=fastapi&logoColor=white)

🌐 Frontend
![Vue.js](https://img.shields.io/badge/Vue.js%203-4FC08D?style=flat-square&logo=vuedotjs&logoColor=white)
![Axios](https://img.shields.io/badge/Axios-5A29E4?style=flat-square&logo=axios&logoColor=white)

🗄 Database
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=flat-square&logo=mariadb&logoColor=white)

🤝 Collaboration & Tools
![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)
![Figma](https://img.shields.io/badge/Figma-F24E1E?style=flat-square&logo=figma&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?style=flat-square&logo=googlesheets&logoColor=white)
![Discord](https://img.shields.io/badge/Discord-5865F2?style=flat-square&logo=discord&logoColor=white)

---
# ℹ️ 프로젝트 소개
## 1. 프로젝트 개요

본 프로젝트는 INSILENCE 웹 사이트를 참고하여 진행한 쇼핑몰 클론 코딩 프로젝트입니다.
회원가입부터 로그인, 상품 조회, 장바구니, 주문(Mock), 주문 내역 조회까지
쇼핑몰의 기본적인 사용자 흐름을 짧은 기간 안에 구현하는 것을 목표로 했습니다.

복잡한 비즈니스 로직이나 결제 시스템보다는,
프론트엔드와 백엔드가 어떻게 연결되고
각 기능이 어떤 순서로 동작하는지를 직접 구현하며 구조를 이해하는 데 집중했습니다.

## 2. 개발 배경

실제 서비스 형태의 프로젝트를 경험해보기 위해,
UI 구조가 비교적 명확하고 쇼핑몰의 기본 흐름이 잘 드러나는
INSILENCE 웹 페이지를 클론 대상으로 선정했습니다.

단순한 화면 구현에 그치지 않고,
“이 화면에서 어떤 API가 호출되고”,
“이 데이터가 다음 단계에서 어떻게 사용되는지”를 팀 단위로 나누어 구현하며
협업 기반의 기능 분리와 데이터 흐름을 경험하는 것을 목표로 프로젝트를 진행했습니다.

## 3. 프로젝트 목적

- 실제 쇼핑몰 화면을 참고하여 프론트엔드 화면 구성 경험을 쌓는 것
- Vue.js 기반 컴포넌트 구조와 페이지 설계 방식에 대한 이해
- API 연동과 상태 관리를 포함한 서비스 형태의 클론 코딩 경험
- 팀 단위 역할 분담을 통한 협업 개발 경험
- 이후 기능 확장과 유지보수를 고려한 구조로 페이지 구현

# 💡 주요 기능
본 프로젝트는 INSILENCE 클론 코딩을 목표로 한 단기 MVP로 쇼핑몰의 핵심 사용자 흐름을 구현하는 데 집중했습니다.

### 전체 사용자 흐름
회원가입 → 로그인 → 상품 탐색 → 장바구니 → 주문(Mock) → 주문내역 조회
### 📌 주요 기능 요약
| 기능 영역 | 기능명      | 설명                      |
| :---- | :------- | :---------------------- |
| 회원    | 회원 관리    | 회원가입, 로그인(JWT), 로그아웃    |
| 상품    | 상품 조회    | 메인 페이지, 상품 목록, 카테고리 조회  |
| 상품    | 상품 상세    | 상품 정보 확인, 수량 조절         |
| 장바구니  | 장바구니 관리  | 상품 담기, 목록 조회, 수량 변경, 삭제 |
| 주문    | 주문(Mock) | 주문서 작성, 주문 완료 처리        |
| 마이페이지 | 주문 내역    | 주문 내역 조회, 주문 상세 조회      |

### 1. 회원 (Auth)
- 회원가입
- 로그인 (JWT 발급)
- 로그아웃 (프론트엔드에서 토큰 제거 방식으로 처리)
- 로그인 상태 유지 (Authorization 헤더 기반)

### 2. 상품 (Product)
- 메인 페이지 (브랜드 이미지 고정 노출)
- 상품 목록 조회
  - 전체 상품 조회
  - 카테고리 기준 조회 (OUTER / TOP / BOTTOM / ACC)
- 상품 상세 조회
  - 상품 정보 확인
  - 수량 조절

### 3. 장바구니 (Cart)
- 장바구니 담기
- 장바구니 목록 조회
- 상품 수량 변경
- 장바구니 상품 삭제

### 4. 주문 (Order – Mock)
- 주문서 작성
- 배송지 정보 입력
- 주문 완료 처리
- window.confirm("결제하시겠습니까?") 승인 시 주문 성공 처리
- 장바구니 → 주문 데이터 이관 
- 주문 완료 후 장바구니 비우기

### 5. 주문 내역 (My Page)
- 주문 내역 리스트 조회
- 주문 상세 조회
- 주문 날짜
- 상품명
- 가격 정보
---
# 요구사항 명세서
<details>
<summary>요구사항 명세서  </summary>
<div markdown="1">

<img width="2226" height="1314" alt="image" src="https://github.com/user-attachments/assets/76ae5da1-14b8-47d5-b978-1656350a85b5" />


</div>
</details>

---
# 스토리보드
<details>
<summary>스토리보드</summary>
<div markdown="1">

<img width="2238" height="1450" alt="image" src="https://github.com/user-attachments/assets/45191557-c5dc-4b39-9a3a-d408c39519a3" />
<img width="1544" height="1094" alt="image" src="https://github.com/user-attachments/assets/b89eceb8-c013-4145-9e5c-3df77fed27df" />
<img width="1544" height="1068" alt="image" src="https://github.com/user-attachments/assets/6bb480d9-71bb-454e-acdb-dd7be1672985" />
<img width="1556" height="1062" alt="image" src="https://github.com/user-attachments/assets/d47717c9-7d9d-4b6a-8101-6b001ada5972" />
<img width="1542" height="1040" alt="image" src="https://github.com/user-attachments/assets/4002a26a-3a31-4031-8a29-2ddab7e36a57" />
<img width="1538" height="1034" alt="image" src="https://github.com/user-attachments/assets/dad9346e-552d-4658-863d-27b25db318b1" />
<img width="1532" height="1030" alt="image" src="https://github.com/user-attachments/assets/91bb787c-76d6-4672-898f-e66697da4db9" />
<img width="1534" height="1024" alt="image" src="https://github.com/user-attachments/assets/044de5ae-be44-4544-a067-60582c53a860" />

</div>
</details>

---
# 테스트 케이스 명세서
<details>
<summary>테스트 케이스 명세서  </summary>
<div markdown="1">

<img width="2960" height="1082" alt="image" src="https://github.com/user-attachments/assets/43b8a9e8-5349-437a-aa81-23aca274a0fa" />


</div>
</details>

--- 
# 🚀 추후 개선 및 확장 계획
1. 인증
Access Token(JWT) 기반 인증 사용
로그아웃은 프론트엔드에서 토큰 제거 방식으로 처리
→ 추후 Refresh Token 도입 및 서버 로그아웃 처리 가능
2. 결제
실제 결제 연동 없이 Mock 결제로 주문 완료 처리
→ 추후 외부 결제 API 연동 가능
3. 상품 옵션
옵션 및 재고 로직 단순화
→ 추후 상품 옵션 구조 확장, 품절 및 재고 부족 처리 로직 추가

---
# ✍️ 프로젝트 회고
| 이름 | 회고 내용 |
| :- |  :---- |
| 김세현 | 이번 프로젝트를 통해 백엔드로 구현한 API를 직접 프론트엔드에 연결하여 실제로 기능을 사용해보는 경험을 할 수 있었습니다. 프론트엔드와 백엔드를 함께 연동해보는 과정이 처음이라 어떤 기능을 백엔드에서 구현해야 하고 어떤 부분을 프론트엔드에서 처리해야 하는지 헷갈리는 순간도 있었지만 직접 부딪히며 구현해보면서 점차 역할의 경계를 이해할 수 있었습니다.<br>또한 기능별로 서로의 API를 호출하는 구조였기 때문에 원활한 개발을 위해 팀원 간의 소통이 얼마나 중요한지 체감할 수 있었습니다. 이번 프로젝트에서는 PR, 커밋 메시지, 이슈 관리, 브랜치 전략 등 협업을 위한 컨벤션을 미리 정하고 이를 기반으로 개발을 진행했는데 이 과정을 통해 협업에서 규칙이 왜 필요한지, 그리고 규칙이 개발 효율과 협업의 질을 얼마나 높여주는지 직접 경험할 수 있었습니다.      |
| 송형욱 | 비록 프론트엔드 프로젝트였지만, 저희 팀은 화면을 예쁘게 꾸미는 것보다 백엔드와 프론트엔드의 연결에 더 집요하게 매달렸습니다. 팀원 모두 백엔드 개발에 뜻이 있다 보니, 단순히 API를 가져다 쓰는 것을 넘어 이 데이터가 서버에서 어떻게 가공되어 넘어오는지를 계속해서 고민했습니다. 덕분에 프론트엔드 로직을 짜면서도 백엔드의 구조를 깊이 이해하는 계기가 되었고, 개발자로서 한 단계 더 성장할 수 있었던 값진 시간이었습니다.     |
| 유찬연 |  저는 이번 프로젝트를 통해 프론트 엔드와 백 엔드 연결을 경험해 볼 수 있었습니다. 프론트 프로젝트였지만 백 엔드 구현도 소홀히 하지 않아 이전 프로젝트들로 경험했던 백 엔드 구현을 다시 연습할 수 있었던 시간이었고, UI 구현은 클론 코딩을 진행하였기 때문에 큰 어려움이 없었지만 라우터 설정부터 백 엔드와 연결하는 것에서 매우 큰 어려움을 겪었습니다. 백 엔드 구현에 있어서 프론트를 고려하고 코드를 작성하는 것이 필요하다는 생각들이 들었고, 프론트에서 역시 백 엔드와 소통이 많이 필요하다는 사실을 알게 되었습니다. 다시 한 번 프로젝트에서의 소통이 중요하다는 사실을 깨달을 수 있었던 유익한 시간이었습니다.  |
| 윤홍석 |  이번 프로젝트를 하면서 프론트의 대한 연습과 백엔드의 기초를 복습할 기회가 있어서 좋았습니다. 이번 프로젝트는 시간도 다른 단위보다 부족하고, 디자인이라는 한계에 부딪혀 클론 코딩으로 방향을 정했는데 나중에는 규모가 작더라도 완전한 프로젝트를 하고 싶습니다.     |
| 이상준 | 쇼핑몰이라는 간단한 CRUD였지만 프론트엔드와 백엔드를 연결할때 어려움과 협업의 중요성을 느꼈습니다. 현재 사용하고 있는 사이트를 클론코딩했지만 프론트에 대해서 어떻게 작동하고 코드를 쳐야되는지 어떻게 백엔드와 연결해야되는지 알 수 있는 뜻깊은 프로젝트였습니다. 다음에는 조금 더 무거운 주제로 조금 더 크게 만들고 싶습니다. 감사합니다.     |
