# 02_02 · API 명세 – MediGo (로컬 단독)

> 문제 2 · 핵심 엔드포인트 정의(OpenAPI 문서와 병행)

## 공통
- Base URL (로컬): `http://localhost:8000`
- 응답 포맷: `application/json; charset=utf-8`

## 1. 헬스 체크
### GET `/health`
- 응답 예시:
```json
{ "status": "ok", "time": "2025-11-24T12:00:00Z" }
```

## 2. 약국(Pharmacies)
### 2.1 GET `/api/pharmacies`
- 설명: 모든 약국 목록 + 지도 중심 좌표
- 응답:
```json
{
  "center_lat": 37.5665,
  "center_lng": 126.9780,
  "pharmacies": [
    { "id": 1, "name": "시청약국", "lat": 37.5667, "lng": 126.9788, "available": false, "checked": false }
  ]
}
```

### 2.2 GET `/api/pharmacies/search?query=...`
- 설명: 이름 포함 검색, 미매칭 시 전체 반환 후 거리순 정렬.

### 2.3 POST `/api/pharmacies/{id}/check`
- 설명: 재고/배달 가능 여부 확인.
- 응답:
```json
{
  "pharmacy": { "id": 2, "name": "광화문약국", "...": "..." },
  "message": "배달 가능한 약국 확인"
}
```

## 3. 처방전 업로드(Prescriptions)
### POST `/api/prescriptions`
- Content-Type: `multipart/form-data`
- 필드:
  - `file`: 이미지 파일
  - `patient_name` (옵션, 기본값: "데모 사용자")
  - `birth` (옵션)
- 응답:
```json
{ "id": "uuid", "filename": "원본파일명.jpg", "uploaded_at": "..." }
```

## 4. 주문(Orders)
### 4.1 POST `/api/orders`
- 설명: 선택한 약국/주소로 주문 생성.
- 요청:
```json
{
  "pharmacy_id": 2,
  "address": "서울 중구 세종대로 110 (서울시청)",
  "recipient": "데모 사용자",
  "note": "경비실에 맡겨주세요"
}
```
- 응답:
```json
{
  "id": "uuid",
  "status": "assigned",
  "pharmacy": { "...": "..." },
  "address": "...",
  "recipient": "...",
  "eta_minutes": 15,
  "route": { "leg1": [...], "leg2": [...], "start": [...], "pharmacy": [...], "dest": [...] }
}
```

### 4.2 GET `/api/orders/{id}`
- 설명: 주문 상세 + 상태/ETA.

### 4.3 PATCH `/api/orders/{id}/status`
- 설명: 상태를 수동 변경(테스트용).
- 요청:
```json
{ "status": "delivered" }
```

