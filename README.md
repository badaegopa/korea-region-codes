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

```
data/
└── master.json
    ├── meta          # 버전, 최종 업데이트, 경고문
    └── regions
        └── {지역명}
            ├── name_en       # 영문명
            ├── type          # 특별시 / 광역시 / 도 등
            ├── codes         # 광역 단위 API별 코드
            └── districts
                └── {구/군명}
                    └── ...   # 기초 단위 API별 코드
```

수록 API 코드 목록:

| 키 | API | 비고 |
|----|-----|------|
| `KOSIS_인구계열` | KOSIS 국가통계포털 — 인구 통계 | 31계열 |
| `KOSIS_출산율계열` | KOSIS — 출산율·혼인·이혼 통계 | 26계열 |
| `KOSIS_고령화계열` | KOSIS — 고령화 통계 | 26계열 |
| `KOSIS_의사수계열` | KOSIS — 의사 수 통계 | 26계열 |
| `KOSIS_노사분규` | KOSIS — 노사분규 통계 | 05계열 |
| `KOSIS_인터넷이용률` | KOSIS — 인터넷 이용률 | A09 계열 |
| `SGIS_adm_cd` | SGIS 통계지리정보서비스 | 행정구역 코드 |
| `TAGO_cityCode` | TAGO 대중교통정보 | 버스 API |
| `에어코리아_sidoName` | 에어코리아 대기질 API | 시도명 문자열 |
| `아파트RTMS_LAWD_CD` | 국토부 아파트 실거래가 API | LAWD_CD |

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
