# 03_01 · 실행 패키지(MVP) – MediGo

> 문제 3 · 실제로 돌릴 수 있는 패키지

## 1. 실행 방법 요약
- 개발자용(로컬 서버 실행):
  1) `python -m venv .venv`  
  2) `.\.venv\Scripts\activate`  
  3) `pip install -r requirements.txt`  
  4) `uvicorn backend.app.main:app --reload`  
  5) 브라우저에서 `http://localhost:8000` 접속

- 심사용 exe 빌드:
  1) PowerShell에서 `powershell -ExecutionPolicy Bypass -File build-desktop.ps1`  
  2) `dist/mediGo-desktop.exe` 생성 확인

- 최종 사용자:
  - `mediGo-desktop.exe`를 더블클릭 → 내장 웹뷰 창에서 즉시 사용

## 2. 포함물
- `backend/` – FastAPI 앱 + SQLite DB
- `web/` – 정적 프런트(Leaflet, Pretendard 폰트 포함)
- `desktop.py` – 웹뷰 + 백엔드 통합 실행 엔트리포인트
- `build-desktop.ps1` – exe 빌드 스크립트

## 3. 환경 변수
- `MEDIGO_DATA_DIR` (선택): DB/업로드/로그 저장 경로  
  - 기본값: `C:\Users\<계정>\.medigo\`  
  - exe 실행 시 DB(`db.sqlite`), 업로드 파일, `run.log`가 이 경로에 생성됨.

## 4. 시드 데이터
- 첫 실행 시 `pharmacies` 테이블이 비어 있는 경우 `seed.py`를 통해 기본 약국 데이터를 자동 삽입합니다.

