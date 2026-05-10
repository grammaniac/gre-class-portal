# GRE Class Portal — 프로젝트 헌법
이 문서는 Cowork이 이 프로젝트에서 작업할 때 항상 따라야 하는 규칙입니다.
새로운 작업을 시작하기 전에 반드시 이 문서를 먼저 읽으세요.
---
## 프로젝트 개요
**프로젝트명**: GRE Class Portal (gre-class-portal)
**소유자**: 송종옥 선생님 (John, grammaniac@gmail.com)
**목적**: GRE Verbal 학원 수강생을 위한 수업 자료 포털 사이트
**호스팅**: GitHub Pages (https://grammaniac.github.io/gre-class-portal/)
**호칭**: 사용자에게는 "선생님"으로 호칭 (사장님 X)
---
## 운영 정책
**5월 (2026년)**: 수동 운영 단계, 워크플로우 검증 중
**6월~**: 본격 자동화 단계 진입 예정
---
## 사이트 구조
### 4개 유료 반 (비밀번호 보호)
| 반 | 폴더 | 시간 | 일정 | 교재 |
|---|---|---|---|---|
| Pattern Book 기본반 | `basic/` | 10:00–13:50 | 월수금 | Pattern Book |
| MoMoZip 실전반 | `advanced/` | 10:00–12:50 | 화목금 | TCSE · RCCR Volume |
| Pattern Book 주말 기본반 | `weekend-basic/` | 14:00–17:50 | 토 | Pattern Book |
| MoMoZip 주말 실전반 | `weekend-advanced/` | 09:00–12:50 | 토 | TCSE · RCCR Volume |
### 2개 무료 강의 (자유 접근)
| 강의 | 폴더 |
|---|---|
| 영문분석 짝수달 | `analysis-even/` |
| 영문분석 홀수달 | `analysis-odd/` |
### 어휘 도구 (외부 링크)
- 거만어 퀴즈: https://buly.kr/DPVsswA
- Vocarain: https://grammaniac.github.io/vocarain
---
## 폴더 구조
```
gre-class-portal/
├── index.html                    # 대문 (랜딩 페이지)
├── og-image.png                  # Open Graph 이미지
├── README.md
├── data/
│   └── passwords.json            # 반별 비밀번호 (평문)
├── basic/
│   ├── index.html                # 반별 중문 (월별 진도표 + 안내)
│   └── 2026-05/                  # 월별 일별 페이지 폴더
│       └── 2026-05-DD-XXXX.html  # 일별 수업 페이지
├── advanced/ (동일 구조)
├── weekend-basic/ (동일 구조)
├── weekend-advanced/ (동일 구조)
├── analysis-even/
│   └── index.html
├── analysis-odd/
│   └── index.html
└── archive/                      # 만료된 자료 보관용
```
---
## 디자인 토큰
### 공통 (모든 페이지)
```
--ink: #1a1a1a;
--paper: #fafaf7;
--paper-2: #f3f1ea;
--rule: #d8d4c7;
--muted: #6b6557;
```
### 반별 색상
| 반 | accent | accent-soft | highlight |
|---|---|---|---|
| 기본반 (basic) | `#1e3a5f` (잉크 블루) | `#4a6b8c` | `#e3eaf2` |
| 실전반 (advanced) | `#8b3a2e` (적갈색) | `#c4654d` | `#f5e9d3` |
| 주말 기본반 | `#1e3a5f` | `#4a6b8c` | `#e3eaf2` |
| 주말 실전반 | `#8b3a2e` | `#c4654d` | `#f5e9d3` |
| 영문분석 짝수달 | `#4a5d4f` (그린 그레이) | `#6b8270` | `#e8ede5` |
| 영문분석 홀수달 | `#8a6d3b` (황토색) | `#b08e57` | `#f0e8d8` |
| 거만어 퀴즈 | `#6b4c8a` (보라) | – | `#ece5f3` |
| Vocarain | `#3e7a85` (청록) | – | `#dbecef` |
| 반 선택 모의고사 | `#3a3a3a` (차콜) | – | `#e8e6e0` |
### 폰트 스택
- 헤드라인 (영문): `'Fraunces', serif`
- 본문 (한글): `'IBM Plex Sans KR', sans-serif`
- 메타정보 (영문/숫자): `'JetBrains Mono', monospace`
### 라이트 모드 강제 (4중 방어)
모든 페이지에 다음 4가지가 있어야 함:
1. `<meta name="color-scheme" content="light only">`
2. `<meta name="supported-color-schemes" content="light">`
3. CSS `:root { color-scheme: light only !important; }`
4. `@media (prefers-color-scheme: dark)` 오버라이드
---
## 절대 규칙
### 1. 라이트 모드 강제
다크 모드 호환 절대 금지. 위의 4중 방어를 모든 새 페이지에 포함시킬 것.
### 2. URL 파일명 규칙
일별 페이지는 추측 불가능한 랜덤 코드 포함 필수:
- 형식: `YYYY-MM-DD-XXXX.html` (XXXX = 4자리 영문/숫자 랜덤)
- 예: `2026-05-08-m3p2.html`, `2026-05-13-h2n6.html`
### 3. 일별 페이지 만들기 = 이전 페이지 복사 후 수정
0부터 새로 만들지 말고, 같은 반의 가장 최근 일별 페이지를 복사한 뒤 수정.
### 4. 비밀번호 보호 (반별 중문 페이지만)
4개 유료 반 중문 페이지는 비번 게이트 필수.
일별 페이지 + 영문분석 + 어휘 도구는 비번 없음.
### 5. 학생 대상 호칭
페이지 본문에서 학생을 부를 때:
- "수강생", "학생" 일반 호칭 사용
- 강사 본인은 "송종옥 강사" 또는 "선생님"
### 6. GitHub commit 메시지
한국어로 명확하게 작성. 예시:
- `기본반 Day 3 페이지 추가 (2026-05-11)`
- `실전반 Day 2 모의고사 링크 변경`
- `대문 index에 모의고사 카드 추가`
### 7. 시간대
모든 날짜/시간 처리는 **Asia/Seoul (KST, UTC+9)** 기준.
---
## 일별 페이지 (가장 자주 만드는 작업)
상세 가이드는 `instructions/daily-page.md` 참조.
**핵심 13개 변경 포인트** (절대 빠뜨리지 말 것):
1. `<title>`
2. OG 메타 4종 (`og:title`, `og:description`, `og:url`, `twitter:title`, `twitter:description`, `description`)
3. `<h1 class="title">5월 Day N</h1>`
4. `<span class="day-pill">YYYY.MM.DD DAY</span>` ← 자주 빠뜨림!
5. `오늘의 수업 · DAY N` 라벨 ← 자주 빠뜨림!
6. 강의 영상 카드 타이틀 + URL
7. 거만어 보충수업 카드 타이틀 + URL
8. 모의고사 카드 타이틀 + URL
9. (실전반만) 후기 카드 타이틀 + URL 2개
10. 푸터 (`Day N` 표기)
11. 진도표 카드 `current` 클래스 이동
12. 진도표 카드 `오늘` 라벨 이동
13. 새 파일명에 랜덤 코드 부여
---
## 외부 자료 링크 (자주 변경되지 않는 것들)
### 고정 링크 (모든 페이지 공통)
- 필수청취 예습: `https://www.youtube.com/playlist?list=PL2LRXEvdvh4fn27PivLtNWt19OyOZ-Pb5`
- 거만어 Quiz: `https://buly.kr/DPVsswA`
- 거만어 보조 자료: `https://drive.google.com/drive/folders/1mwNhYWAitvG6zhoASrGgh-bZE8Jta3o5`
- Weekly GRE Song: `https://www.youtube.com/playlist?list=PL2LRXEvdvh4fX91VHXc-2KU2BX0r9mWko`
- 거만어 카드뉴스 (Instagram): `https://www.instagram.com/gre_song`
- 카카오톡 오픈챗: `https://open.kakao.com/o/s0ifxj1f`
- 카피나라: 02-532-9660, dhyoon@copynara.co.kr
### 거만어 보충 4주차 (주별로 사용)
- 1주차: `https://www.youtube.com/playlist?list=PL2LRXEvdvh4fy7aBtI898MZ8YWyZJmfWI`
- 2주차: `https://www.youtube.com/playlist?list=PL2LRXEvdvh4cwNycDmnwtszg2ZHdIweiq`
- 3주차: `https://www.youtube.com/playlist?list=PL2LRXEvdvh4ez7AdVbRek48laREcHQ1bk`
- 4주차: `https://www.youtube.com/playlist?list=PL2LRXEvdvh4cwvT6311G8Xgjstyt1f1wl`
### 반별 종합 Drive 폴더
- 실전반 Day별 핸드아웃 / 모든 교재 정답: `https://drive.google.com/open?id=1zB6k_71a5cELWVHqxvhT4Ab1mux98GnK&usp=drive_fs`
- 기본반 Day별 핸드아웃 / 교재 정답: `https://drive.google.com/open?id=1kibJimwgm8wvJ28s4gueJPKek_-61C-r&usp=drive_fs`
- 주말 기본반 Week별 핸드아웃 / 정답 (홀수달): `https://drive.google.com/open?id=1ER4yKiY8_G1us2svX9Cs4RXgwSYStTeR&usp=drive_fs`
---
## 비밀번호 (data/passwords.json)
평문 저장. 학원 자료 보호 목적이라 충분한 보안 수준.
변경 방법: 파일 직접 수정 → commit → 학생들에게 메일 안내.
---
## GitHub 워크플로우
### 자동 commit 규칙
작업 완료 후 항상:
1. 변경 파일 확인 (`git status`)
2. add (`git add <파일>`)
3. 한국어 commit 메시지 작성 (`git commit -m "..."`)
4. push (`git push`)
### 단일 commit 단위
한 번의 작업 = 한 번의 commit.
예: "Day 3 페이지 만들기"는 새 파일 생성 + index의 dayUrls 업데이트까지 한 commit으로.
---
## 작업 시 자주 묻는 정보
매번 새로 묻지 않도록, 사용자가 명령에서 반드시 알려주는 정보:
**일별 페이지 만들기**:
- 반 (기본반/실전반/주말 기본반/주말 실전반)
- Day 번호 + 날짜
- 강의 영상 URL
- 모의고사 URL
- 거만어 보충 몇 주차
- (실전반만) 후기 핸드아웃 URL 2개
**그 외 자동 처리**:
- 폴더 위치, 파일명 랜덤 코드, 진도표 강조 이동, 메타데이터, GitHub commit 등.
---
## 참고: Cowork 작업 패턴
작업 요청 받으면:
1. 이 `claude.md` 다시 한 번 점검
2. `instructions/` 안의 해당 작업 가이드 확인
3. 작업 수행
4. 변경 사항 보고 + GitHub commit/push
5. 학생 발송용 URL이 있으면 마지막에 명확히 표시
