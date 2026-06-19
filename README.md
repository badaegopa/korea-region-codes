# korea-region-codes

> 한국 공공데이터 API별 지역코드 통합 레퍼런스

## ⚠️ 왜 이 레포가 필요한가

한국 공공데이터 API는 **같은 지역인데 API마다 코드가 다르다.**

예시 — 울산광역시 남구:
| API | 코드 |
|-----|------|
| KOSIS 인구표 | 31140 |
| KOSIS 출산율표 | 26020 |
| TAGO 버스 | 26 (광역시 단위) |
| 아파트 RTMS | 31140 |

31계열을 출산율표에 쓰면 **경기도 데이터**가 나온다.  
이 함정을 모르면 진단서가 오진서가 된다.

## 구조
## 사용법

```javascript
// master.json import
const codes = require('./data/master.json')
const cityCode = codes.regions['울산광역시'].codes.TAGO_cityCode // → "26"
```

```python
import json
with open('data/master.json') as f:
    codes = json.load(f)
print(codes['regions']['울산광역시']['codes']['KOSIS_인구계열'])  # → "31"
```

## 수록 지역 현황

| 지역 | 광역 코드 | 기초 코드 | 상태 |
|------|-----------|-----------|------|
| 울산광역시 | ✅ | ✅ | 완료 |
| 서울특별시 | 🔜 | 🔜 | 예정 |
| 부산광역시 | 🔜 | 🔜 | 예정 |
| 전국 17개 광역시도 | 🔜 | 🔜 | 예정 |

## 기여

지역코드 오류 발견 시 Issue 또는 PR 환영.  
행정구역 개편 반영은 `data/master.json` 수정 후 PR.

## 출처

- [KOSIS 국가통계포털](https://kosis.kr)
- [SGIS 통계지리정보서비스](https://sgis.kostat.go.kr)
- [data.go.kr 공공데이터포털](https://data.go.kr)
- [에어코리아](https://www.airkorea.or.kr)
- [TAGO 대중교통정보](https://tago.go.kr)

---
Made by [늘푸른바다 사회동역학 연구소](https://everbluesea.org)  
Seed data: Ulsan Metropolitan City (2026-06-20)
