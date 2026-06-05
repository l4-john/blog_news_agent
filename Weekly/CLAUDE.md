# 📊 주간 경제 총정리 AI 비서 시스템

## 개요
매주 월요일 오전 7:12 KST, 지난주 주요 경제 기사를 수집해 주간 총정리 글을 자동 작성·저장하는 5개 비서 시스템입니다.

## 실행 방법
이번 주 주간 총정리 시작해줘

## 비서 구성 및 실행 순서
순서 | 비서 이름 | 역할 | 모델
1 | weekly-search | 주간 기사 수집 | Sonnet
2 | weekly-selector | 핵심 테마 3가지 선정 + 글쓰기 개요 작성 | Sonnet
3 | weekly-writer | 개요 기반 티스토리·네이버 본문 + SEO 메타 작성 | Sonnet
4 | weekly-editor | 오타·수치 형식 교정 (저장 전 텍스트 교정) | Haiku
5 | weekly-saver | 노션 DB 저장 + 완료 보고 | Sonnet

## 오케스트레이터 실행 지침

### STEP 0: 시작 전 정리 (필수)
`Weekly/temp_weekly.md` 파일이 있으면 삭제. 이전 실행 잔여 파일 제거.

### STEP 1~2: 순차 실행
1. weekly-search 실행 → 주간 기사 목록 수집
2. weekly-selector 실행 → 핵심 테마 3개 + 개요 작성

### STEP 3: 본문 작성
3. weekly-writer 실행 → 스스로 `write_file` 도구를 사용하여 결과를 `Weekly/temp_weekly.md`에 저장.

### STEP 4: 교정
4. weekly-editor: 스스로 `read_file`로 `Weekly/temp_weekly.md` 읽기 → 교정 후 `write_file`로 덮어쓰기.

### STEP 5: 저장 및 종료
5. weekly-saver: 스스로 `read_file`로 `Weekly/temp_weekly.md` 읽어 노션 저장 → 완료 후 `Weekly/temp_weekly.md` 삭제.
보고 출력 후 즉시 종료. 추가 설명·작업 일절 금지.

## 토큰 절약 원칙
- 각 단계 결과물을 대화창에 전체 출력 금지.
- 중간 결과물은 임시 파일(`Weekly/temp_weekly.md`)에 저장.
- 대화창에는 진행 상태만 아주 짧게 보고. (예: `[STEP 3] 주간 본문 작성 완료`)

## 노션 DB
- DB: 📰 해외 경제 기사 초안
- Data Source ID: ae7e2fac-80f3-4ccc-928e-5ff059a854c9

## 필수 원칙 (전 비서 공통)
- 투자 권유 표현 절대 금지
- 특정 종목·ETF·상품명 언급 금지
- 번역투 없이 자연스러운 한국어
- % 앞 띄어쓰기 없이
- 억·조 단위 한국식 변환
- 수치는 반드시 이모지 + 항목명 + 수치 형식으로 별도 표기
- 소제목과 내용 사이 빈 줄 금지

## Cowork 스케줄러 설정
- 실행 시각: 매주 월요일 오전 07:12 KST
- 트리거 프롬프트: 이번 주 주간 총정리 시작해줘.