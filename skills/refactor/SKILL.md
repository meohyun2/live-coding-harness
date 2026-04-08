---
name: refactor
description: 동작을 유지하면서 코드 품질을 개선하는 리팩토링 커맨드
argument-hint: <리팩토링 대상>
allowed-tools: [Read, Glob, Grep, Bash, Edit]
user-invocable: true
---

# /refactor $ARGUMENTS

**원칙**: 리팩토링 전후 동작은 동일해야 한다. 기능 변경 금지.

## Step 1 — 현재 상태 파악
- 대상 코드 전체 읽기
- 문제점 구체적으로 특정 (중복, 복잡성, 나쁜 네이밍, 잘못된 추상화)
- 리팩토링 목표 한 문장: "X를 Y 목적으로 변경"

## Step 2 — 의존 파일 파악
- 대상 코드를 import하거나 사용하는 파일 전체 목록 작성
- 이 파일들이 리팩토링 후에도 정상 동작해야 함

## Step 3 — 리팩토링
- 변경 적용
- 모든 의존 파일을 같은 패스에서 업데이트
- 깨진 import나 dead code 남기지 않기

## Step 4 — 검증
- `npx tsc --noEmit`으로 새로운 TypeScript 에러 없음 확인
- 이 코드를 커버하는 기존 테스트 실행하여 통과 확인
- 테스트가 없다면 수동 검증 방법 서술

## Step 5 — 요약
- 무엇이 변경되었고 무엇이 더 나아졌는지 서술
- 변경되지 않은 것 (동작, 공개 API, 테스트 커버리지) 명시
