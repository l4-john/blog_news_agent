# 📥 Prompt Sync 비서 시스템

## 개요
노션에 저장된 프롬프트 페이지를 가져와 로컬 md 파일을 최신 상태로 업데이트합니다.

## 실행 방법
- **트리거 프롬프트:** 프롬프트 동기화해줘 / 노션 프롬프트 가져와

## 노션 DB
- **URL:** https://app.notion.com/p/fd448d67133741ebb7bd09d040942c6c
- **위치:** Blog > Agents > Prompt Sync

## 노션 DB 구조
각 페이지는 다음 속성을 가져야 합니다:
- **Name (제목):** 식별 이름 (예: `WallStreet Tistory Search`)
- **file_path (텍스트):** 로컬 상대 경로 (예: `Blog_Tistory_Report/1_WallStreet_Report/1-wallstreet-tistory-search.md`)
- **page_url (URL):** 실제 프롬프트 내용이 담긴 노션 페이지 URL

## 오케스트레이터 실행 지침 (순차 실행 절대 엄수)
당신은 아래 2단계 비서 호출을 순차적으로 통제하는 오케스트레이터입니다. 한 비서의 작업이 완전히 끝난 후 다음 비서를 호출하십시오.

**[STEP 1: 노션 데이터 수집]** `prompt-sync-fetcher` 비서를 호출하여 노션 DB에서 모든 프롬프트 페이지를 조회하고 파일 경로 및 본문 내용을 추출하도록 지시하십시오.

**[STEP 2: 로컬 파일 업데이트]** Fetcher 결과를 받으면 `prompt-sync-updater` 비서를 호출하여 각 md 파일을 업데이트하도록 지시하십시오. Updater의 최종 결과 보고 후 작업을 종료하십시오.
