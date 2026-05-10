# 일별 수업 페이지 만들기
이 가이드는 매일 수업이 있는 날 새 일별 페이지를 만드는 표준 절차입니다.
---
## 작업 흐름 요약
1. 정보 입력 받기 (사용자로부터)
2. 이전 일별 페이지 복사
3. 13개 변경 포인트 수정
4. 반별 index의 dayUrls에 새 매핑 추가 (이미 있으면 스킵)
5. GitHub commit + push
6. 학생 발송용 URL 보고
---
## 1단계: 사용자로부터 받아야 할 정보
매번 사용자가 명령에서 알려주는 것:
**필수**:
- 반 (기본반 / 실전반 / 주말 기본반 / 주말 실전반)
- Day 번호 (예: Day 3, Week 2)
- 날짜 (예: 5월 11일 월요일)
- 강의 영상 URL
**선택** (이 항목들은 매주/매월 변경됨):
- 모의고사 URL
- 거만어 보충 주차 (1, 2, 3, 4)
- (실전반만) 후기 핸드아웃 URL 2개
- (주말반만) 주중반 영상 URL 2개
**자동 결정** (코드가 알아서):
- 새 파일명의 랜덤 코드 (4자리)
- 메타데이터 형식
- 진도표 강조 이동
---
## 2단계: 이전 페이지 복사
같은 반의 가장 최근 일별 페이지를 찾아 복사.
예시 (기본반):
- 5/8 페이지가 마지막이면 → 그걸 복사 → 5/11 페이지로 만듦
- 만약 5/6이 처음이면 → 그걸 복사
복사 명령:
```bash
cp basic/2026-05/2026-05-08-m3p2.html basic/2026-05/2026-05-11-XXXX.html
```
(XXXX는 새로 부여하는 4자리 랜덤 코드)
---
## 3단계: 13개 변경 포인트
새 파일 안에서 다음 모든 항목을 변경. 빠뜨리면 안 됨.
### A. 메타데이터 (HTML head)
**1. `<title>`**
```
변경 전: <title>Pattern Book 기본반 · 5월 Day 2 (5/8 금)</title>
변경 후: <title>Pattern Book 기본반 · 5월 Day 3 (5/11 월)</title>
```
**2. Open Graph 메타 태그들** (6개)
```html
<meta property="og:title" content="Pattern Book 기본반 · 5월 Day 3">
<meta property="og:description" content="5월 11일 (월) · 오늘의 강의 자료 — 송종옥 GRE Verbal">
<meta property="og:url" content="https://grammaniac.github.io/gre-class-portal/basic/2026-05/2026-05-11-q5r8.html">
<meta name="twitter:title" content="Pattern Book 기본반 · 5월 Day 3">
<meta name="twitter:description" content="5월 11일 (월) · 오늘의 강의 자료 — 송종옥 GRE Verbal">
<meta name="description" content="5월 11일 (월) · 오늘의 강의 자료 — 송종옥 GRE Verbal">
```
### B. 헤더 영역
**3. 페이지 타이틀**
```
변경 전: <h1 class="title">5월 Day 2</h1>
변경 후: <h1 class="title">5월 Day 3</h1>
```
**4. 날짜 pill (자주 빠뜨림 주의!)**
```
변경 전: <span class="day-pill">2026.05.08 FRI</span>
변경 후: <span class="day-pill">2026.05.11 MON</span>
```
요일은 영문 3자 대문자: MON / TUE / WED / THU / FRI / SAT / SUN
### C. 첫 번째 탭 (영상 자료)
**5. 첫 번째 섹션 라벨 (자주 빠뜨림 주의!)**
```
변경 전: <div class="section-label">오늘의 수업 · DAY 2</div>
변경 후: <div class="section-label">오늘의 수업 · DAY 3</div>
```
(주말반은 "DAY"가 아니라 "WEEK"로)
**6. 강의 영상 카드**
```html
<div class="card-title">Day 3 · 강의 전체 영상</div>
<div class="card-desc">오늘 진도의 본강의 플레이리스트입니다. 예습 영상을 먼저 보신 뒤 시청해주세요.</div>
<a href="[새 강의 영상 URL]" target="_blank" rel="noopener">강의 영상 열기</a>
```
**7. 거만어 보충수업 카드**
```html
<div class="card-title">거만어 보충수업 · 2주차</div>
<div class="card-desc">매주 갱신되는 거만어 어휘 보충 영상입니다.</div>
<a href="[해당 주차 URL]" target="_blank" rel="noopener">보충 플레이리스트 열기</a>
```
거만어 4주차 URL은 `claude.md` 참고.
### D. 모의고사 탭
**8. 모의고사 카드**
```html
<div class="card-title">[5월 N일 모의고사 또는 5월 N주차 모의고사]</div>
<a href="[새 모의고사 URL]" target="_blank" rel="noopener">모의고사 시작</a>
```
라벨은 반에 따라 다름:
- 실전반 (매일): "5월 12일 모의고사"
- 기본반 (주별): "5월 2주차 모의고사"
- 주말반 (주별): "이번 주 모의고사" 또는 "5월 N주차"
### E. 문서 자료 탭 (실전반만)
**9. 후기 핸드아웃 카드**
```html
<div class="section-label" style="margin-top: 32px;">월별 후기 핸드아웃 (2주차)</div>
<div class="card">
  <div class="card-title">5월 2주차 후기 핸드아웃</div>
  <div class="card-desc">매주 갱신되는 후기 정리 자료입니다. 두 개의 후기를 함께 제공합니다.</div>
  <a href="[URL 1]" target="_blank" rel="noopener" style="margin-right: 16px;">후기 ①</a>
  <a href="[URL 2]" target="_blank" rel="noopener">후기 ②</a>
</div>
```
### F. 푸터
**10. 푸터 텍스트**
```
변경 전: <div>Pattern Book · GRE Verbal · 기본반 · 5월 Day 2</div>
변경 후: <div>Pattern Book · GRE Verbal · 기본반 · 5월 Day 3</div>
```
### G. 진도표 탭 (강의 진도표)
**11. 이전 Day의 `current` 클래스 제거 + `오늘` 라벨 제거**
```html
<!-- 변경 전 -->
<div class="day-card current">
  <div class="day-header">
    <span class="day-num">Day 2</span>
    <span class="day-date">May 8 (FRI)</span>
    <span class="day-now">오늘</span>
  </div>
<!-- 변경 후 -->
<div class="day-card">
  <div class="day-header">
    <span class="day-num">Day 2</span>
    <span class="day-date">May 8 (FRI)</span>
  </div>
```
**12. 새 Day에 `current` 클래스 + `오늘` 라벨 추가**
```html
<!-- 변경 전 -->
<div class="day-card">
  <div class="day-header">
    <span class="day-num">Day 3</span>
    <span class="day-date">May 11 (MON)</span>
  </div>
<!-- 변경 후 -->
<div class="day-card current">
  <div class="day-header">
    <span class="day-num">Day 3</span>
    <span class="day-date">May 11 (MON)</span>
    <span class="day-now">오늘</span>
  </div>
```
### H. 파일명
**13. 새 파일명에 4자리 랜덤 코드 부여**
- 형식: `YYYY-MM-DD-XXXX.html`
- XXXX는 영문 소문자 + 숫자 조합 (예: `q5r8`, `m3p2`, `h2n6`)
- 같은 달에 이미 사용된 코드 피하기
---
## 4단계: 반별 index의 dayUrls 매핑 확인
각 반의 `index.html` 안에 `dayUrls` JavaScript 객체가 있음.
예시 (basic/index.html):
```javascript
const dayUrls = {
  "2026-05-06": "2026-05/2026-05-06-k9x7.html",
  "2026-05-08": "2026-05/2026-05-08-m3p2.html",
  "2026-05-11": "2026-05/2026-05-11-q5r8.html",  // ← 새로 만든 페이지
  ...
};
```
만약 새 날짜가 dayUrls에 없으면 → 추가
만약 이미 있으면 → 파일명이 일치하는지 확인 후 다르면 업데이트
---
## 5단계: GitHub commit + push
```bash
git add basic/2026-05/2026-05-11-q5r8.html
git add basic/index.html  # 만약 dayUrls 변경 시
git commit -m "기본반 Day 3 페이지 추가 (2026-05-11)"
git push
```
commit 메시지 형식:
- 새 페이지: `[반] Day N 페이지 추가 (YYYY-MM-DD)`
- 수정: `[반] Day N 페이지 수정 (사유)`
- 다중 변경: `[반] Day N + dayUrls 매핑 추가`
---
## 6단계: 사용자에게 결과 보고
다음 형식으로 보고:
```
✅ 완료!
생성된 파일: basic/2026-05/2026-05-11-q5r8.html
GitHub commit: 기본반 Day 3 페이지 추가 (2026-05-11)
배포 시작됨 (1-2분 후 라이브)
학생 발송용 URL:
https://grammaniac.github.io/gre-class-portal/basic/2026-05/2026-05-11-q5r8.html
```
---
## 주말반 특수 사항
### 주말 기본반
- "Day" 대신 "Week"로 표기
- 진도표는 4주차 + 온라인 (총 5개)
- 강의 영상 카드는 1개
### 주말 실전반
- "Day" 대신 "Week"로 표기
- 진도표는 4주차 + 온라인 (총 5개)
- **강의 영상 카드는 2개** (주중반 Day N + Day N+1)
- 모의고사 카드는 **3개** (주중반과 동일하게 10회 제공)
- 안내 문구: "주말반은 주중반 영상의 80~90%를 제공합니다."
---
## 첫날 페이지 (개강일) 특수 사항
매월 첫 수업일 = 개강일에는 추가 카드:
**첫날 교재 파일 카드** (교재 구입 탭 끝에)
```html
<div class="section-label" style="margin-top: 32px;">첫날 교재 파일 (개강 한정)</div>
<div class="card featured">
  <div class="card-title">Day 1 교재 파일</div>
  <div class="card-desc">개강일 한정으로 제공되는 첫날 교재 파일입니다. 다음 수업부터는 정식 교재로 학습합니다.</div>
  <a href="[첫날 교재 URL]" target="_blank" rel="noopener">교재 파일 열기</a>
</div>
```
또한 헤더에 개강 배지:
```html
<h1 class="title">5월 Day 1<span class="opening-badge">개강</span></h1>
```
(Day 2부터는 개강 배지 제거)
---
## 자주 하는 실수 체크리스트
매번 작업 후 확인:
- [ ] 1. `<title>` 변경됨
- [ ] 2. OG 메타 4종 모두 변경됨
- [ ] 3. `<h1>` 변경됨
- [ ] 4. **`day-pill` 변경됨** (자주 빠뜨림)
- [ ] 5. **첫 섹션 라벨 변경됨** (자주 빠뜨림)
- [ ] 6. 강의 영상 카드 (타이틀 + URL)
- [ ] 7. 거만어 보충 (타이틀 + URL)
- [ ] 8. 모의고사 (타이틀 + URL)
- [ ] 9. (실전반) 후기 카드
- [ ] 10. 푸터
- [ ] 11. 이전 Day의 current 제거
- [ ] 12. 새 Day에 current 추가
- [ ] 13. 파일명에 랜덤 코드
- [ ] 14. dayUrls 매핑 확인
- [ ] 15. GitHub push 성공
---
## 참고: 파일 충돌 방지
같은 날에 여러 번 작업할 때:
1. 항상 작업 시작 전 `git pull` 실행
2. push 실패 시 사용자에게 보고
