# 🍳 Chef's Market (셰프마켓)

> **레시피 공유, 식재료 거래, 공동구매를 한 곳에서!** 요리를 사랑하는 사람들을 위한 커뮤니티 기반 푸드 플랫폼

[![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115.6-009688?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)

---

## 📑 목차

- [소개](#-소개)
- [주요 기능](#-주요-기능)
- [기술 스택](#️-기술-스택)
- [프로젝트 구조](#-프로젝트-구조)
- [설치 방법](#-설치-방법)
- [실행 방법](#-실행-방법)
- [API 문서](#-api-문서)
- [환경 변수 설정](#-환경-변수-설정)


---

## 🌟 소개

**Chef's Market**은 요리 애호가들을 위한 종합 커뮤니티 플랫폼입니다. 레시피를 공유하고, 남는 식재료를 이웃과 거래하며, 공동구매를 통해 신선한 재료를 합리적인 가격에 구매할 수 있습니다.

AI 기반 레시피 추천 시스템이 사용자의 보유 식재료와 영양 목표에 맞는 최적의 레시피를 제안해 드립니다.

---

## ✨ 주요 기능

### 📖 레시피 관리 & AI 추천
- 레시피 CRUD (다중 이미지 지원)
- 영양 정보 관리 (칼로리, 탄수화물, 단백질, 지방, 나트륨)
- **Q-Learning 기반 맞춤형 레시피 추천**
- 보유 식재료 기반 레시피 매칭

### 🥬 식재료 관리
- 개인 식재료 재고 관리 (유통기한, 수량 추적)
- **영수증 OCR 스캔** (CLOVA OCR + OpenAI 연동)
- 500+ 한국 식재료 표준 데이터베이스
- 식재료 요청/제안 시스템

### 🛒 식재료 마켓플레이스
- 위치 기반 식재료 거래 (GPS 좌표 활용)
- 실시간 1:1 채팅 시스템
- 거래 상태 관리 및 약속 예약

### 👥 공동구매
- 공동구매 그룹 생성 및 참여
- 참여 인원에 따른 동적 가격 책정
- 절약 금액 자동 계산
- 그룹 채팅방 시스템

### 👤 사용자 시스템
- JWT 기반 인증
- 역할별 등급 (CHEF, MASTER, EXPERT, NEWBIE)
- 신뢰도 점수 시스템
- 개인 영양 목표 설정

---

## 🛠️ 기술 스택

### Backend
| 기술 | 버전 | 설명 |
|------|------|------|
| **FastAPI** | 0.115.6 | 비동기 REST API 프레임워크 |
| **Python** | 3.12 | 런타임 환경 |
| **Uvicorn** | 0.34.0 | ASGI 서버 |
| **Pydantic** | 2.10.5 | 데이터 검증 |

### Database
| 기술 | 설명 |
|------|------|
| **PostgreSQL** | 메인 관계형 데이터베이스 |
| **SQLAlchemy** | ORM |
| **GeoAlchemy2** | 위치 기반 쿼리 지원 |
| **Alembic** | 데이터베이스 마이그레이션 |

### Cloud & AI
| 기술 | 설명 |
|------|------|
| **AWS S3** | 이미지 스토리지 |
| **OpenAI API** | 영수증 파싱 및 AI 기능 |
| **CLOVA OCR** | 영수증 이미지 텍스트 추출 |

### Security
| 기술 | 설명 |
|------|------|
| **python-jose** | JWT 토큰 관리 |
| **Passlib + Bcrypt** | 비밀번호 암호화 |

---

## 📁 프로젝트 구조

```
Chef-s-Market/
├── 📄 main.py                 # 애플리케이션 진입점
├── 📄 requirements.txt        # Python 의존성
├── 📄 dockerfile              # Docker 설정
├── 📄 alembic.ini             # DB 마이그레이션 설정
│
├── 📂 core/                   # 핵심 설정
│   ├── config.py              # 환경 변수 & 설정
│   └── security.py            # JWT & 비밀번호 유틸리티
│
├── 📂 db/                     # 데이터베이스 설정
│   ├── base.py                # SQLAlchemy 베이스
│   └── session.py             # 비동기 DB 세션
│
├── 📂 models/                 # SQLAlchemy ORM 모델
│   └── models.py              # User, Recipe, Sale 등
│
├── 📂 schemas/                # Pydantic 스키마
│   ├── auth.py                # 인증 스키마
│   ├── users.py               # 사용자 스키마
│   ├── recipes.py             # 레시피 스키마
│   └── ...                    # 기타 스키마
│
├── 📂 api/                    # API 라우트
│   ├── dependencies.py        # 의존성 주입
│   └── routes/                # 엔드포인트
│       ├── auth.py            # 인증 (회원가입, 로그인)
│       ├── recipes.py         # 레시피 CRUD & 추천
│       ├── sale.py            # 마켓플레이스
│       └── ...                # 기타 라우트
│
├── 📂 crud/                   # 데이터 액세스 레이어
├── 📂 services/               # 비즈니스 로직 레이어
├── 📂 utils/                  # 유틸리티 함수
├── 📂 data/                   # 데이터 파일
│   └── standard_ingredients.json  # 식재료 DB
│
└── 📂 alembic/                # DB 마이그레이션
    └── versions/              # 마이그레이션 파일
```

---

## 💿 설치 방법

### 사전 요구사항

- Python 3.12+
- PostgreSQL
- Docker (선택사항)
- AWS S3 버킷
- OpenAI API 키
- CLOVA OCR API 키

### 방법 1: 직접 설치

```bash
# 저장소 클론
git clone https://github.com/your-username/Chef-s-Market.git
cd Chef-s-Market

# 가상환경 생성 및 활성화
python3.12 -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 의존성 설치
pip install -r requirements.txt

# 환경 변수 설정 (.env 파일 생성)
cp .env.example .env
# .env 파일 수정

# 데이터베이스 마이그레이션
alembic upgrade head
```

### 방법 2: Docker 설치

```bash
# Docker 이미지 빌드
docker build -t chefs-market .

# 컨테이너 실행
docker run -p 8000:8000 --env-file .env chefs-market
```

---

## 🚀 실행 방법

### 개발 서버 실행

```bash
# Python 직접 실행
python main.py

# 또는 Uvicorn으로 실행 (핫 리로드)
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

### 프로덕션 서버 실행

```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4
```

---

## 📚 API 문서

서버 실행 후 아래 주소에서 API 문서를 확인할 수 있습니다:

| 문서 | URL |
|------|-----|
| **Swagger UI** | http://localhost:8000/docs |
| **ReDoc** | http://localhost:8000/redoc |

