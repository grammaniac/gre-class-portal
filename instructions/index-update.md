# 반별 index 업데이트 가이드
이 가이드는 매월 또는 특수 상황에서 반별 중문(index) 페이지를 업데이트하는 표준 절차입니다.
---
## 언제 업데이트하나?
### 매월 1일경 (정기)
- 새 달 진도표로 변경
- dayUrls를 새 달 페이지로 변경
- 첫 수업일에 `current` 강조 위치 설정
### 비정기
- 진도 변경 (예: 학생 진도 따라 조정)
- 강사 정보 변경
- 추가 자료 링크 변경
- 비밀번호 변경 (이건 `data/passwords.json`만)
---
## 반별 index 구조 이해
각 반의 `index.html`은 다음 영역으로 구성:
1. **헤더**: 반 이름, 시간, 일정
2. **상시 안내**: 매일 메일로 발송 안내
3. **월별 진도표**: Day 1~10 카드 (또는 Week 1~4 + Online)
4. **상시 자료**: 필수청취, 거만어 Quiz, 거만어 보조, Weekly GRE Song, Instagram
5. **교재 구입**: 카피나라 안내
6. **질문 방법**: 이메일, 카카오톡
7. **JavaScript**: dayUrls 매핑 + 시간 기반 활성화
---
## 1. 매월 진도표 변경
### 1-1. 사용자가 알려줄 정보
다음 달 진도표 (PDF 또는 텍스트):
예시:
```
6월 Day 1 (6/1 월): TCSE Triggers X (p.AA-BB), RC 유형 N (p.CC-DD)
6월 Day 2 (6/3 수): TCSE Triggers Y (p.EE-FF), RC 유형 M (p.GG-HH)
...
```
### 1-2. 변경할 위치
각 반 `index.html`의 진도표 카드들:
```html
<a class="day-card" data-date="2026-06-01">
  <div class="day-header">
    <span class="day-num">Day 1</span>
    <span class="day-date">June 1 (MON)</span>
  </div>
  <dl class="day-content">
    <dt>TCSE</dt>
    <dd>...진도 내용... <span class="pages">p.XX–YY</span></dd>
    <dt>RC / CR</dt>
    <dd>...진도 내용... <span class="pages">p.XX–YY</span></dd>
  </dl>
</a>
```
### 1-3. 진도 카테고리
**기본반/주말 기본반**:
- TCSE (Triggers, Practice Questions)
- RC / CR
**실전반/주말 실전반**:
- TCSE (Group 번호로 묶음)
- RCCR (Group 번호로 묶음)
- Part II (TCSE NNN, RCCR NNN)
### 1-4. 영문 날짜 형식
`day-date` 안의 영문은 `Month D (DAY)` 형식:
- May 11 (MON)
- June 3 (WED)
- July 15 (FRI)
---
## 2. dayUrls 매핑 업데이트
### 2-1. 위치
각 반 `index.html` 하단의 `<script>` 안:
```javascript
const dayUrls = {
  "2026-05-06": "2026-05/2026-05-06-k9x7.html",
  "2026-05-08": "2026-05/2026-05-08-m3p2.html",
  // ...
};
```
### 2-2. 새 달로 전환 시
기존 매핑 유지 + 새 달 매핑 추가:
```javascript
const dayUrls = {
  // 5월 (만료 후에도 보관 - 한 달 만료 정책)
  "2026-05-06": "2026-05/2026-05-06-k9x7.html",
  // ...
  
  // 6월 (새로 추가)
  "2026-06-01": "2026-06/2026-06-01-XXXX.html",
  "2026-06-03": "2026-06/2026-06-03-XXXX.html",
  // ...
};
```
XXXX는 미리 결정해도 되고 (월초 일괄 페이지 생성 시), 페이지 만들 때 결정해도 됨.
### 2-3. 만료된 매핑 정리
만료 정책:
- 기본반/실전반: 1개월
- 주말반: 2개월
만료된 자료는 옵션:
- A: dayUrls에 그대로 두기 (페이지는 archive로 이동)
- B: dayUrls에서 제거
현재는 옵션 A (간단함). 자동화 단계에서 옵션 B로 전환 검토.
---
## 3. 진도표 시간 기반 활성화 작동 방식
JavaScript가 자동으로 처리:
```javascript
// 페이지 열릴 때 한국 시간 기준 오늘 날짜 계산
const today = getTodayKST();
// 각 진도표 카드 처리
document.querySelectorAll('.day-card[data-date]').forEach(card => {
  const cardDate = card.dataset.date;
  
  if (cardDate === today) {
    // 오늘 수업: 활성화 + 강조
    card.classList.add('today');
    card.href = dayUrls[cardDate] || '#';
  } else if (cardDate < today) {
    // 지난 수업: 비활성화 + 흐리게
    card.classList.add('past', 'disabled');
  } else {
    // 미래 수업: 비활성화 + "예정"
    card.classList.add('future', 'disabled');
  }
});
```
**즉, 일별 페이지 링크는 그날 자동 노출. 학원 정책상 중간 등록자 차단을 위함.**
---
## 4. 비밀번호 변경
### 4-1. 위치
`data/passwords.json`:
```json
{
  "basic": "pattern2605",
  "advanced": "momozip2605",
  "weekend-basic": "pwknd2605",
  "weekend-advanced": "mwknd2605"
}
```
### 4-2. 변경 방법
1. 파일 직접 수정
2. commit + push
3. **반드시 사용자에게 새 비번을 학생에게 안내하라고 알려줄 것**
### 4-3. 비밀번호 작명 패턴
`{반약자}{년월}` 형식:
- 기본반: `pattern2605` (Pattern + 26년 5월)
- 실전반: `momozip2605` (MoMoZip + 26년 5월)
- 주말 기본반: `pwknd2605` (Pattern Weekend)
- 주말 실전반: `mwknd2605` (MoMoZip Weekend)
매월 새 비번 발급 권장.
---
## 5. 첫 페이지 만들기 (개강 첫날)
매월 첫 수업일에 페이지 만들 때:
### 5-1. 헤더에 개강 배지
```html
<h1 class="title">6월 Day 1<span class="opening-badge">개강</span></h1>
```
### 5-2. 첫날 교재 파일 카드 (교재 구입 탭)
```html
<div class="section-label" style="margin-top: 32px;">첫날 교재 파일 (개강 한정)</div>
<div class="card featured">
  <div class="card-title">Day 1 교재 파일</div>
  <div class="card-desc">개강일 한정으로 제공되는 첫날 교재 파일입니다. 다음 수업부터는 정식 교재로 학습합니다.</div>
  <a href="[첫날 교재 URL]" target="_blank" rel="noopener">교재 파일 열기</a>
</div>
```
이 두 항목은 **Day 1만**. Day 2부터는 둘 다 제거.
---
## 6. 매월 워크플로우 체크리스트
매월 1일경 (또는 직전 주말):
- [ ] 1. 새 달 진도표 정보 받기 (사용자로부터)
- [ ] 2. 새 달 폴더 생성 (예: `basic/2026-06/`)
- [ ] 3. 각 반 index.html의 진도표 카드 업데이트
- [ ] 4. 각 반 index.html의 dayUrls 매핑 추가
- [ ] 5. (선택) 비밀번호 변경
- [ ] 6. (선택) 강의 영상 URL을 모두 받았으면 일별 페이지 일괄 생성
- [ ] 7. GitHub commit + push
- [ ] 8. 사용자에게 보고 + 비번 변경 시 학생 안내 요청
---
## 7. 자주 받는 요청 패턴
### "다음 달 진도표로 업데이트해줘"
→ 진도표 카드 + dayUrls 모두 변경 (이 가이드 1, 2단계)
### "비번 바꿔줘"
→ `data/passwords.json` 수정만
### "특정 Day 진도 변경"
→ 해당 카드만 수정
### "이번 달 모의고사 일괄 변경"
→ 각 일별 페이지의 모의고사 URL 일괄 수정 (instructions/daily-page.md 참고)
### "다음 달 페이지 한 번에 다 만들어줘"
→ 진도표 + dayUrls + 일별 페이지 N개 일괄 생성 (대형 작업)
---
## 8. 주의사항
### 라이트 모드 강제
모든 변경 후에도 다음 4가지 유지:
1. `<meta name="color-scheme" content="light only">`
2. `<meta name="supported-color-schemes" content="light">`
3. CSS `:root { color-scheme: light only !important; }`
4. `@media (prefers-color-scheme: dark)` 오버라이드
### 비밀번호 게이트 유지
4개 유료 반 index에는 항상 비번 게이트 코드 포함되어야 함.
영문분석 두 페이지는 비번 없음 (자유 접근).
### 디자인 토큰 유지
색상 변수 변경 금지. claude.md의 디자인 토큰 표 참고.
