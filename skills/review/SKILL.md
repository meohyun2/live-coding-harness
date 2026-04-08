---
name: review
description: 제출 전 변경사항 전체를 검토하고 평가자용 요약을 작성하는 커맨드
argument-hint: [특정 검토 포커스]
allowed-tools: [Read, Glob, Grep, Bash]
user-invocable: true
---

# /review $ARGUMENTS

## Step 1 — Diff 요약
- `git diff`(또는 `git diff HEAD`) 실행으로 수정된 파일 전체 확인
- 각 파일의 변경 유형 나열 (버그 수정 / 기능 추가 / 리팩토링 / 타입 수정)

## Step 2 — TypeScript 상태
- `npx tsc --noEmit` 실행
- 에러가 있으면 수정 후 진행
- 에러가 없으면 명시적으로 확인

## Step 3 — 코드 품질 체크리스트
변경된 각 파일에서 확인:
- [ ] `console.log` 없음
- [ ] `any` 타입 없음
- [ ] 주석 처리된 코드 블록 없음
- [ ] 불필요한 `// TODO` 없음
- [ ] 사용하지 않는 import 없음
- [ ] Props 인터페이스명은 `ComponentNameProps` 형식

## Step 4 — 동작 회귀 확인
- 수정한 버그 각각: 수정 내용과 인접 동작에 영향 없음 확인
- 추가한 기능 각각: 접근 가능하고 기존 기능과 충돌 없음 확인
- 리팩토링 각각: 동작 동일함 확인

## Step 5 — 평가자용 요약 작성

### 변경 사항
(파일명과 한 줄 설명으로 구성된 bullet 목록)

### 선택 근거
(각 변경에 대해 이 접근법을 선택한 이유 한 문장)

### 미완료 사항 / 가정
(완료하지 못한 것, 처리하지 않은 엣지 케이스, 가정한 사항)

### 검증 방법
(평가자가 따라할 수 있는 단계별 수동 테스트 계획)
