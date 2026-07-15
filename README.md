# 칼로그 (Callog) — 식단 칼로리 AI 분석

사진 한 장으로 식사 칼로리와 영양 정보를 추정하는 [앱인토스](https://toss.im) 미니앱입니다.

> 코드는 비공개(상용 앱). 이 저장소는 프로젝트 설명·스크린샷입니다.

<p>
  <img src="screenshots/01_today.png" width="220">
  <img src="screenshots/02_analysis.png" width="220">
</p>

## 핵심

- **사진 → AI 영양 추정** — 멀티모달 vision 모델로 음식을 인식하고, 항목별 위치와 칼로리·영양소를 구조화
- **5단계 정확도 파이프라인** — 기준물체 보정, 식약처 영양 DB 그라운딩, CalorieCLIP 앙상블, 도메인 규칙, 저신뢰 요청의 상위 모델 전송
- **운영 안정성** — 전역 rate limit, 비용 상한, 저신뢰 결과의 사용자 확인 경로, 서버리스 환경의 실패 처리
- **데이터 기반** — 식약처 영양 DB 약 28.2만 건과 Nutrition5k 소규모 외부 벤치마크로 반복 오차를 확인

## Nutrition5k 벤치마크

50개 요리의 promotion benchmark에서 다음 변화를 확인했습니다.

- 중앙 절대 백분율 오차(MdAPE): **31% → 19%**
- 허용 오차 통과율: **70% → 88%** (`44/50`)

> 이 수치는 50개 샘플의 중앙값과 통과율입니다. 전체 음식에 대한 일반 정확도나 평균 MAPE로 확대해 해석하지 않습니다.

## 기술

React 19 · TypeScript · Vite · 앱인토스(Granite) · Vercel serverless · Supabase Postgres · OpenAI vision · Railway(CalorieCLIP 워커)

## 상태

앱인토스 미니앱으로 출시·운영 중입니다.
