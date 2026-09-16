# bumbilkka-data

`붐빌까` 앱이 내려받는 예보 데이터. 사람이 직접 고치지 않는다 —
앱 저장소의 `.github/workflows/update-forecast.yml` 이 매일 KST 05:40에 갱신한다.

```
public/            ← CDN이 서빙하는 것 (앱이 받아가는 파일)
  index.json         지역·시군구 목록, 등급 임계값, 전국 하이라이트, 요일 프로필
  area/{시도}.json   관광지 × 30일 집중률 + 사진·좌표·연관 관광지
  festivals.json     45일 내 축제
  search.json        관광지 이름 색인
cache/             ← 회차 간 재사용 (CDN 제외). 지우면 보강이 처음부터 다시 돈다
state.json         ← 마지막 성공일·호출량·커버리지 (CDN 제외)
```

## 확인

```bash
curl -s https://bumbilkka-data.pages.dev/index.json | python3 -m json.tool | head -30
```

`base_date`가 오늘(KST)이면 정상이다. 며칠 밀려 있으면 앱 저장소의 Actions 로그를 본다.
