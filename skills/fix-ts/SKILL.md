---
name: fix-ts
description: TypeScript 에러를 체계적으로 찾아 수정하는 커맨드
argument-hint: [특정 에러 또는 파일]
allowed-tools: [Read, Glob, Grep, Bash, Edit]
user-invocable: true
---

# /fix-ts $ARGUMENTS

인자가 없으면 `npx tsc --noEmit`을 실행하여 발견된 모든 에러를 수정한다.

## Step 1 — 에러 수집
- `npx tsc --noEmit` 실행 후 전체 출력 캡처
- 파일별로 에러 그룹화
- 수정 전 에러 총 개수 기록

## Step 2 — 분류
각 에러를 다음 중 하나로 분류:
- **타입 미정의 / implicit any** — 인터페이스 또는 명시적 타입 주석 필요
- **타입 불일치** — 잘못된 타입으로 값이 사용됨 (소스 파일에서 정확한 타입 확인)
- **누락된 속성** — 인터페이스 업데이트 또는 잘못된 사용
- **null/undefined 미처리** — guard, optional chaining, 또는 근거 있는 non-null assertion
- **모듈 not found** — import 경로 또는 타입 선언 오류

## Step 3 — 의존성 역순으로 수정
- 다른 파일이 import하는 파일(하위)부터 먼저 수정
- `any` 사용 금지 — `unknown` + narrowing 또는 올바른 타입 사용
- `// @ts-ignore` 사용 금지 — 실제 에러 해결
- 인터페이스에 새 속성 추가 시 해당 인터페이스를 생성하는 모든 위치도 업데이트

## Step 4 — 클린 확인
- `npx tsc --noEmit` 재실행
- 에러 0개 확인 또는 기존에 있던 에러(범위 외)라면 그 이유 설명

## Step 5 — 설명
- 비자명한 수정 각각에 대해 에러가 무엇이었고 수정이 왜 올바른지 한 문장으로 서술
