# 📋 글로벌 경제 브리핑 AI 비서 시스템

## 개요
매일 오전 9:27 KST, 기사 비서 완료 후 노션에 저장된 기사를 불러와 브리핑 페이지를 자동 작성하는 5개 비서 시스템입니다.

## 실행 방법
오늘 브리핑 작업 시작해줘

## 비서 구성 및 실행 순서
순서 | 비서 이름 | 역할 | 모델
1 | briefing-loader | 노션에서 오늘 기사 불러오기 | Haiku
2 | briefing-validator | 슬롯 완전성 검증 + 빈 슬롯 긴급 보충 | Sonnet
3 | briefing-writer | 티스토리·네이버 브리핑 본문 + SEO 메타 작성 | Sonnet
4 | briefing-editor | 오타·수치 형식 교정 (저장 전 텍스트 교정) | Haiku
5 | briefing-saver | 노션 DB 저장 + 완료 보고 | Sonnet

## 오케스트레이터 실행 지침

### STEP 0: 시작 전 정리 (필수)
`Briefing/temp_briefing.md` 파일이 있으면 삭제. 이전 실행 잔여 파일 제거.

### STEP 1~2: 순차 실행
1. briefing-loader 실행 → 기사 목록 수집
2. briefing-validator 실행 → [HOLD] 출력 시 즉시 파이프라인 중단. 3번 이후 비서 호출 금지.

### STEP 3: 브리핑 본문 작성
3. briefing-writer 실행 → 스스로 `write_file`로 `Briefing/temp_briefing.md`에 저장.

### STEP 4: 교정
4. briefing-editor: 스스로 `read_file`로 `Briefing/temp_briefing.md` 읽기 → 교정 후 `write_file`로 덮어쓰기.

### STEP 5: 저장 및 종료
5. briefing-saver: 스스로 `read_file`로 `Briefing/temp_briefing.md` 읽어 노션 저장 → 완료 후 `Briefing/temp_briefing.md` 삭제.
보고 출력 후 즉시 종료. 추가 설명·작업 일절 금지.

## 토큰 절약 원칙
- 각 단계 결과물을 대화창에 전체 출력 금지.
- 중간 결과물은 임시 파일(`Briefing/temp_briefing.md`)에 저장.
- 대화창에는 진행 상태만 아주 짧게 보고. (예: `[STEP 3] 브리핑 작성 완료`)

## 실행 순서 (기사 비서와 연계)
1. 기사 비서: 오늘 기사 작업 시작해줘 → 노션에 기사 7개 저장
2. 브리핑 비서: 오늘 브리핑 작업 시작해줘 → 저장된 기사로 브리핑 페이지 생성

## 노션 DB
- DB: 📰 해외 경제 기사 초안
- Data Source ID: ae7e2fac-80f3-4ccc-928e-5ff059a854c9

## 필수 원칙 (전 비서 공통)
- 투자 권유 표현 절대 금지
- 특정 종목·ETF·상품명 언급 금지
- 번역투 없이 자연스러운 한국어
- % 앞 띄어쓰기 없이
- 억·조 단위 한국식 변환
- 수치는 반드시 문장 안에 녹여서 텍스트로만 서술. 이모지·별도 줄 나열 금지.
- 노션 페이지 본문(content)에는 아무것도 입력하지 말 것

## Cowork 스케줄러 설정
- 실행 시각: 매일 오전 09:27 KST (화~토)
- 트리거 프롬프트: 오늘 브리핑 작업 시작해줘.