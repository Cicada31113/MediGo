<div style="background: linear-gradient(135deg, rgba(255, 255, 255, 0.15) 0%, rgba(255, 255, 255, 0.05) 100%); backdrop-filter: blur(15px); -webkit-backdrop-filter: blur(15px); border: 1px solid rgba(255, 255, 255, 0.3); border-radius: 25px; padding: 40px; box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.2), inset 0 1px 0 rgba(255, 255, 255, 0.3);">

<table>
<tr>
<td width="60%" valign="top">

<div align="center">

<img src="Assets/images/medi_go_logo_compressed2.png" alt="MediGo Logo" width="300">

# 메디-고 (Medi-Go) 🏥💊

**AI 기반 약 배달 및 복약 지도 서비스**

[![License](https://img.shields.io/badge/license-Private-red.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104+-green.svg)](https://fastapi.tiangolo.com/)
[![React](https://img.shields.io/badge/React-18+-61dafb.svg)](https://reactjs.org/)

</div>

</td>
<td width="40%" valign="top">

<div align="center">

## 👥 팀 우리동네약배달

<table>
  <tr>
    <td align="center">
      <img src="Assets/images/LEE.png" alt="이현민" width="100"><br/>
      <b>이현민</b><br/>
      <sub>팀장</sub>
    </td>
    <td align="center">
      <img src="Assets/images/NAM.png" alt="남상훈" width="100"><br/>
      <b>남상훈</b><br/>
      <sub>팀원</sub>
    </td>
    <td align="center">
      <img src="Assets/images/KWON.png" alt="권덕현" width="100"><br/>
      <b>권덕현</b><br/>
      <sub>팀원</sub>
    </td>
  </tr>
</table>

</div>

</td>
</tr>
</table>

---

## 프로젝트 개요

처방전 사진을 앱으로 전송하면, 운영팀이 약국 조제 및 배달을 대행하고, 복약 지도 메시지를 앱을 통해 텍스트로 전달하는 서비스입니다.

### 시연 영상

<div align="center">

[![시연 영상 재생하기](https://img.shields.io/badge/▶️-시연_영상_재생하기-FF6B6B?style=for-the-badge&logo=github)](https://cicada31113.github.io/MediGo/)

</div>

### 사용자 플로우

```mermaid
graph LR
    A[병원 진료] --> B[처방전 발급]
    B --> C[MediGo 앱<br/>처방전 업로드]
    C --> D[OCR 처리]
    D --> E[주문 생성]
    E --> F[약국 조제]
    F --> G[배달 시작]
    G --> H[약 배달 완료]
    H --> I[복약 지도<br/>카카오톡 발송]
    
    style C fill:#e3f2fd
    style D fill:#fff9c4
    style I fill:#c8e6c9
```

### 시스템 아키텍처

```mermaid
graph TB
    subgraph "Frontend"
        A[React 사용자 앱]
        B[React Admin 대시보드]
    end
    
    subgraph "Backend"
        C[FastAPI 서버]
        D[PostgreSQL DB]
        E[AWS S3]
    end
    
    subgraph "AI/ML"
        F[OCR Service]
        G[LLM Model<br/>향후 구현]
    end
    
    subgraph "External"
        H[카카오 OAuth]
        I[카카오톡 채널]
    end
    
    A --> C
    B --> C
    C --> D
    C --> E
    C --> F
    F --> G
    C --> H
    C --> I
    
    style C fill:#e3f2fd
    style F fill:#fff9c4
    style G fill:#fff9c4
```

MVP 단계에서는 Wizard of Oz 방식으로 운영하며, 사용자에게 서비스 가치를 제공하면서 동시에 AI 모델 학습을 위한 데이터를 수집합니다.

### Wizard of Oz 운영 방식

```mermaid
graph TB
    A[사용자 주문] --> B[OCR 자동 처리]
    B --> C[운영자 수동 검토]
    C --> D[복약 지도 수동 작성]
    D --> E[카카오톡 발송]
    C --> F[학습 데이터 저장]
    F --> G[향후 AI 자동화]
    
    style B fill:#e3f2fd
    style C fill:#fff9c4
    style D fill:#fff9c4
    style G fill:#c8e6c9
    
    classDef manual fill:#fff9c4,stroke:#f57c00
    classDef auto fill:#c8e6c9,stroke:#388e3c
    classDef future fill:#e1bee7,stroke:#7b1fa2
    
    class C,D manual
    class B,E auto
    class G future
```

**현재 (MVP)**: 운영자가 수동으로 복약 지도 작성 → 데이터 수집  
**향후**: AI가 자동으로 복약 지도 생성

### 핵심 기능 (MVP)

```mermaid
mindmap
  root((MediGo<br/>핵심 기능))
    사용자 기능
      카카오 소셜 로그인
      처방전 사진 업로드
      약 배달 주문
      주문 상태 추적
      복약 지도 수신
    관리자 기능
      주문 관리
      복약 지도 작성
      고객 관리
    AI 기능
      OCR 처리
      데이터 수집
      향후 LLM 자동화
    통합 기능
      카카오톡 채널 연동
      AWS S3 이미지 저장
```

**주요 기능:**
- 카카오 소셜 로그인
- 처방전 사진 업로드
- 약 배달 주문 및 상태 추적
- 맞춤형 복약 지도 메시지 수신
- 카카오톡 채널 메시지 발송
- 고객 관리 (카카오톡 채널 고객파일)
- 관리자 대시보드 (주문 관리, 복약 지도 작성)
- AI 학습 데이터 수집 (OCR + 복약 지도 페어)

## 기술 스택

### 기술 스택 다이어그램

```mermaid
graph TB
    subgraph "Frontend"
        FE1[React 18]
        FE2[TypeScript]
        FE3[Material-UI]
    end
    
    subgraph "Backend"
        BE1[FastAPI]
        BE2[Python 3.11+]
        BE3[PostgreSQL]
        BE4[SQLAlchemy]
    end
    
    subgraph "AI/ML"
        ML1[EasyOCR]
        ML2[PyTorch]
        ML3[Transformers]
    end
    
    subgraph "Infrastructure"
        INF1[AWS EC2/S3]
        INF2[Docker]
        INF3[Docker Compose]
    end
    
    FE1 --> BE1
    BE1 --> BE3
    BE1 --> ML1
    ML1 --> ML2
    BE1 --> INF1
    
    style FE1 fill:#61dafb
    style BE1 fill:#009688
    style ML1 fill:#ff9800
    style INF1 fill:#ff9900
```

### Backend
- **Framework**: FastAPI 0.104+
- **Language**: Python 3.11+ (권장)
- **Database**: PostgreSQL 15+
- **ORM**: SQLAlchemy 2.0+
- **Migration**: Alembic
- **Authentication**: JWT + OAuth 2.0 (Kakao)
- **Image Storage**: AWS S3
- **OCR**: EasyOCR (한글 지원)

### Frontend (User App)
- **Framework**: React 18+
- **Language**: TypeScript 5+
- **UI Library**: Material-UI (MUI)
- **State Management**: React Query + Zustand
- **HTTP Client**: Axios
- **Build Tool**: Vite

### Admin Dashboard
- **Framework**: React 18+
- **Language**: TypeScript 5+
- **UI Library**: Material-UI (MUI) + React Admin
- **State Management**: React Query + Zustand

### AI/ML
- **OCR**: EasyOCR
- **Framework**: PyTorch 2.0+
- **Model**: Transformers (Hugging Face)
- **Target Model**: LLaMA 3 기반 한국어 모델 (향후)

### Infrastructure
- **Cloud**: AWS (EC2, S3, RDS)
- **Container**: Docker
- **Orchestration**: Docker Compose

## 프로젝트 구조

```
medigo/
├── 01 - Docs/              # 기술 문서
│   ├── API.md
│   ├── SETUP.md
│   └── DEPLOYMENT.md
├── 01 - Documents/         # 프로젝트 문서
│   ├── 01 - 기획/
│   ├── 02 - 설계/
│   └── 03 - 구현/
├── 02 - Backend/           # FastAPI 백엔드 서버
│   ├── app/
│   │   ├── api/           # API 엔드포인트
│   │   ├── core/          # 설정, 보안, 의존성
│   │   ├── models/        # SQLAlchemy 모델
│   │   ├── schemas/       # Pydantic 스키마
│   │   ├── services/      # 비즈니스 로직
│   │   └── utils/        # 유틸리티 함수
│   ├── alembic/           # DB 마이그레이션
│   └── requirements.txt
├── 03 - Frontend/          # 사용자 웹앱 (React)
├── 04 - Admin/            # 관리자 대시보드 (React)
├── 05 - ML/               # AI/ML 모듈
│   ├── ocr/              # OCR 서비스
│   ├── models/           # 학습된 모델
│   └── training/         # 학습 스크립트
├── 06 - Docker/           # Docker 설정
├── 07 - Scripts/          # 유틸리티 스크립트
└── docker-compose.yml
```

## 빠른 시작

### 1단계: 필수 프로그램 설치 확인

```bash
# Python 버전 확인 (3.11 이상 권장)
python --version

# Node.js 버전 확인 (18 이상)
node --version

# PostgreSQL 확인
psql --version
```

### 2단계: 데이터베이스 생성

```bash
# PostgreSQL 접속
psql -U postgres

# 데이터베이스 생성
CREATE DATABASE medigo_db;
\q
```

### 3단계: Backend 실행

```bash
# 백엔드 디렉토리로 이동
cd "02 - Backend"

# 가상환경 생성 및 활성화
python -m venv venv

# Windows
venv\Scripts\activate

# Mac/Linux
source venv/bin/activate

# 패키지 설치
pip install -r requirements.txt

# 환경 변수 복사
copy env.example .env    # Windows
cp env.example .env      # Mac/Linux

# .env 파일 편집 (데이터베이스 연결 정보 입력)

# 데이터베이스 마이그레이션
alembic upgrade head

# 서버 실행
uvicorn app.main:app --reload
```

Backend API: http://localhost:8000/docs

### 4단계: Frontend 실행 (새 터미널)

```bash
# 프론트엔드 디렉토리로 이동
cd "03 - Frontend"

# 패키지 설치
npm install

# 개발 서버 실행
npm run dev
```

사용자 앱: http://localhost:3000

### 5단계: 로그인

1. http://localhost:3000 접속
2. "데모 로그인" 버튼 클릭
3. 홈 화면으로 이동

## 완료

다음 기능을 테스트할 수 있습니다:
- 처방전 업로드 (이미지 파일)
- 주문 생성
- 주문 목록 조회
- 프로필 관리

## 상세 설치 가이드

### Python 환경 (Backend + ML)

```bash
# 1. 가상환경 생성
python -m venv venv

# 2. 가상환경 활성화
# Windows:
venv\Scripts\activate
# Mac/Linux:
source venv/bin/activate

# 3. 전체 패키지 설치
pip install -r requirements.txt
```

### Node.js 환경 (Frontend + Admin)

```bash
# Frontend 설치
cd "03 - Frontend"
npm install

# Admin 설치
cd "../04 - Admin"
npm install
```

### 필수 시스템 요구사항

- **Python**: 3.11 이상 (권장) - Python 3.13은 호환성 문제 가능
- **Node.js**: 18 이상
- **PostgreSQL**: 15 이상
- **운영체제**: Windows 10/11, macOS 10.15+, Ubuntu 20.04+

## 카카오톡 채널 설정

### 1단계: 카카오톡 채널 생성 (2분)

1. https://center-pf.kakao.com/ 접속
2. "새 채널 만들기" 클릭
3. 채널명: 메디-고
4. 채널 URL에서 프로필 ID 확인 (예: `_ZeUTxl`)

### 2단계: 카카오 디벨로퍼스 설정 (2분)

1. https://developers.kakao.com/ 접속
2. **내 애플리케이션** > **애플리케이션 추가하기**
3. 앱 정보 입력 후 생성
4. **제품 설정** > **카카오톡 채널** > 채널 추가
5. **고객 관리 API 정책 동의** 체크 (중요!)
6. **앱 설정** > **앱 키**에서 다음 키 복사:
   - REST API 키
   - Admin 키

### 3단계: 환경 변수 설정 (1분)

`02 - Backend/.env` 파일에 추가:

```env
# Kakao Talk Channel
KAKAO_REST_API_KEY=복사한_REST_API_키
KAKAO_ADMIN_KEY=복사한_Admin_키
KAKAO_CHANNEL_PUBLIC_ID=_ZeUTxl
KAKAO_CHANNEL_API_URL=https://kapi.kakao.com
```

### 완료 체크리스트

- [ ] 카카오 디벨로퍼스 앱 생성 완료
- [ ] REST API 키 발급 완료
- [ ] Admin 키 확인 완료
- [ ] 카카오톡 채널 연결 완료
- [ ] 고객 관리 API 정책 동의 완료
- [ ] `02 - Backend/.env` 파일에 키 입력 완료

더 자세한 설정은 [`01 - Docs/KAKAO_CHANNEL_SETUP.md`](01%20-%20Docs/KAKAO_CHANNEL_SETUP.md)를 참고하세요.

## 문제 해결

### Python 버전 문제

**문제**: Python 3.13은 최신 버전이어서 일부 패키지 호환성 문제가 발생할 수 있습니다

**해결**: Python 3.11 사용 (권장)

```bash
# Python 3.11로 새 가상환경 생성
py -3.11 -m venv venv

# 활성화
venv\Scripts\activate

# 패키지 설치
pip install -r requirements.txt
```

### 데이터베이스 연결 오류

```bash
# PostgreSQL이 실행 중인지 확인
# Windows
services.msc → PostgreSQL 서비스 확인

# Mac
brew services list

# Linux
sudo systemctl status postgresql
```

### 포트 이미 사용 중 오류

```bash
# Windows: 포트 사용 중인 프로세스 종료
netstat -ano | findstr :8000
taskkill /PID <PID번호> /F

# Mac/Linux
lsof -ti:8000 | xargs kill -9
```

### Python 패키지 설치 오류

```bash
pip install --upgrade pip
pip install -r requirements.txt --no-cache-dir
```

### PyTorch 설치 오류

**CPU 버전만 필요한 경우**:
```bash
pip install torch torchvision --index-url https://download.pytorch.org/whl/cpu
```

**GPU (CUDA) 버전**:
```bash
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu118
```

### 카카오 API 오류

- **401 Unauthorized**: REST API 키 또는 Admin 키 확인
- **403 Forbidden**: 고객 관리 API 정책 동의 확인
- **404 Not Found**: 채널 프로필 ID 확인 (앞에 `_` 포함)

## 데이터베이스 스키마

### ERD (Entity Relationship Diagram)

```mermaid
erDiagram
    USERS ||--o{ ORDERS : "주문"
    ORDERS ||--|| PRESCRIPTIONS : "처방전"
    ORDERS ||--o| MEDICATION_GUIDANCE : "복약지도"
    PRESCRIPTIONS ||--o{ TRAINING_DATA : "학습데이터"
    
    USERS {
        int id PK
        string kakao_id UK
        string name
        string email
        string phone
        string delivery_address
        datetime created_at
    }
    
    ORDERS {
        int id PK
        int user_id FK
        enum status
        string delivery_address
        string delivery_phone
        datetime created_at
        datetime updated_at
    }
    
    PRESCRIPTIONS {
        int id PK
        int order_id FK
        string image_url
        text ocr_text
        datetime created_at
    }
    
    MEDICATION_GUIDANCE {
        int id PK
        int order_id FK
        text guidance_text
        boolean is_ai_generated
        datetime sent_at
        datetime created_at
    }
    
    TRAINING_DATA {
        int id PK
        int prescription_id FK
        string image_url
        text ocr_text
        text guidance_text
        datetime created_at
    }
```

### 주요 테이블 설명

- `users` - 사용자 정보 (카카오 OAuth 정보, 배달 주소)
- `orders` - 주문 정보 (상태: submitted → processing → delivering → completed)

### 주문 상태 플로우

```mermaid
stateDiagram-v2
    [*] --> submitted: 주문 생성
    submitted --> processing: 운영자 확인
    processing --> delivering: 약국 조제 완료
    delivering --> completed: 배달 완료
    completed --> [*]
    
    processing --> cancelled: 취소
    delivering --> cancelled: 취소
    cancelled --> [*]
    
    note right of submitted
        처방전 업로드 완료
        OCR 처리 대기
    end note
    
    note right of processing
        약국 조제 중
        복약 지도 작성 중
    end note
    
    note right of delivering
        배달원 배정 완료
        배달 진행 중
    end note
    
    note right of completed
        약 수령 완료
        복약 지도 발송 완료
    end note
```
- `prescriptions` - 처방전 정보 (이미지 S3 URL, OCR 텍스트)
- `medication_guidance` - 복약 지도 (텍스트, AI 생성 여부, 발송 정보)
- `training_data` - AI 학습 데이터 (약봉투 이미지, OCR 텍스트, 복약 지도)

## API 문서

Backend 서버 실행 후:
- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc

### API 플로우

```mermaid
sequenceDiagram
    participant U as 사용자
    participant F as Frontend
    participant B as Backend API
    participant D as Database
    participant O as OCR Service
    participant K as 카카오톡
    
    U->>F: 카카오 로그인
    F->>B: POST /auth/kakao
    B->>D: 사용자 정보 저장
    B-->>F: JWT 토큰 발급
    
    U->>F: 처방전 업로드
    F->>B: POST /orders (이미지)
    B->>O: OCR 처리 요청
    O-->>B: OCR 텍스트 반환
    B->>D: 주문 저장
    B-->>F: 주문 생성 완료
    
    B->>D: 주문 상태 업데이트
    B->>K: 복약 지도 메시지 발송
    K-->>U: 카카오톡 알림
```

### 주요 엔드포인트

**인증**
- `POST /api/v1/auth/kakao` - 카카오 로그인
- `POST /api/v1/auth/refresh` - 토큰 갱신

**사용자**
- `GET /api/v1/users/me` - 내 프로필 조회
- `PUT /api/v1/users/me` - 내 프로필 수정

**주문**
- `POST /api/v1/orders` - 주문 생성
- `GET /api/v1/orders` - 내 주문 목록
- `GET /api/v1/orders/{order_id}` - 주문 상세

**관리자**
- `GET /api/v1/admin/orders` - 전체 주문 목록
- `PUT /api/v1/admin/orders/{order_id}` - 주문 수정
- `POST /api/v1/admin/medication-guidance` - 복약 지도 작성

더 자세한 API 문서는 [`01 - Docs/API.md`](01%20-%20Docs/API.md)를 참고하세요.

## 보안

- HTTPS - 모든 통신 암호화
- JWT - 토큰 기반 인증 (Access + Refresh)
- S3 암호화 - 서버 사이드 암호화 (AES256)
- DB 암호화 - 민감 정보 암호화
- 접근 제어 - RBAC (Role-Based Access Control)

## 개발 로드맵

### 로드맵 타임라인

```mermaid
gantt
    title MediGo 개발 로드맵
    dateFormat YYYY-MM-DD
    section Phase 1: MVP
    프로젝트 구조 설정    :done, 2024-01-01, 2024-01-07
    백엔드 API 개발        :active, 2024-01-08, 2024-02-15
    프론트엔드 개발        :active, 2024-01-15, 2024-02-20
    관리자 대시보드        :2024-02-01, 2024-02-25
    OCR 통합              :2024-02-10, 2024-02-28
    카카오 로그인 연동     :2024-02-15, 2024-03-01
    
    section Phase 2: AI 모델
    데이터 수집 (500+)     :2024-03-01, 2024-05-01
    OCR 전처리            :2024-04-01, 2024-05-15
    LLM 파인튜닝          :2024-05-01, 2024-07-01
    모델 배포             :2024-07-01, 2024-07-15
    
    section Phase 3: 고도화
    실시간 배달 추적      :2024-07-15, 2024-08-15
    인앱 결제 연동        :2024-08-01, 2024-09-01
    복약 알림 기능        :2024-08-15, 2024-09-15
    약국 전용 어드민      :2024-09-01, 2024-10-01
```

### Phase 1: MVP (현재)
- [x] 프로젝트 구조 설정
- [ ] 백엔드 API 개발
- [ ] 프론트엔드 개발
- [ ] 관리자 대시보드 개발
- [ ] OCR 통합
- [ ] 카카오 로그인 연동

### Phase 2: AI 모델 개발
- [ ] 데이터 수집 (500+ 주문)
- [ ] OCR 데이터 전처리
- [ ] LLM 파인튜닝 (LLaMA 3 기반)
- [ ] 모델 배포

### Phase 3: 고도화
- [ ] 실시간 배달 추적
- [ ] 인앱 결제 연동
- [ ] 복약 알림 기능
- [ ] 약국 전용 어드민

## 주요 URL

| 서비스 | URL | 설명 |
|--------|-----|------|
| Backend API | http://localhost:8000 | FastAPI 서버 |
| API 문서 | http://localhost:8000/docs | Swagger UI |
| 사용자 앱 | http://localhost:3000 | React 앱 |
| 관리자 대시보드 | http://localhost:3001 | Admin 패널 |
| OCR 서비스 | http://localhost:8001 | OCR API |

## 법적 고지

서비스 운영 시 다음 법규를 준수해야 합니다:
- 약사법 - 약 배달 관련 규제
- 의료법 - 비대면 진료 관련 규제
- 개인정보보호법 - 민감 의료정보 처리
- 규제 샌드박스 - 서비스 운영 범위

MVP 개발 전 법률 전문가와 보건복지부 유권해석을 받는 것을 권장합니다.

## 추가 문서

- [상세 설정 가이드](01%20-%20Docs/SETUP.md)
- [API 문서](01%20-%20Docs/API.md)
- [배포 가이드](01%20-%20Docs/DEPLOYMENT.md)
- [프로젝트 문서](01%20-%20Documents/)

## 문의

이슈로 문의 바랍니다.

## 라이선스

Private - All Rights Reserved

---

**버전**: 1.0.0  
**최종 업데이트**: 2024-01-16

</div>
