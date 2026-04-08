---
name: orient
description: 낯선 코드베이스를 빠르게 파악하기 위한 구조 분석 커맨드
argument-hint: [분석 포커스]
allowed-tools: [Read, Glob, Grep, Bash]
---

# /orient

$ARGUMENTS 관련 내용을 우선 파악한다. 없으면 전체 코드베이스를 분석한다.

## Step 1 — 프로젝트 기본 정보
- `package.json`을 읽어 의존성, 스크립트, 프로젝트명 파악
- `tsconfig.json`에서 컴파일 옵션과 경로 alias 확인
- `vite.config.ts`, `webpack.config.js`, `next.config.js` 중 존재하는 것으로 빌드 도구 파악

## Step 2 — 소스 구조
- `src/` 최상위 디렉토리 목록 (1단계)
- 진입점(`src/main.tsx`, `src/index.tsx`, `pages/_app.tsx` 등) 파악
- 라우트 또는 페이지 컴포넌트 목록 확인

## Step 3 — 패턴 파악
- 커스텀 훅을 사용하는 컴포넌트 하나와 그 훅을 함께 읽기
- API 호출 패턴 확인 (React Query, SWR, useEffect 등)
- 전역 상태 관리 방식 확인 (Context, Zustand, Redux 등)
- UI 컴포넌트 라이브러리 확인 (shadcn, MUI, Radix 등)

## Step 4 — 테스트 설정
- `vitest.config.ts`, `jest.config.js` 등 존재 여부 확인
- 테스트 파일 패턴 확인 (`*.test.ts`, `*.spec.tsx`)

## Step 5 — 초기 상태 확인
- `npx tsc --noEmit` 실행 후 에러가 있으면 상위 5개 요약
- (코드 수정 전 이미 있던 에러인지 확인하는 것이 목적)

## 출력 형식
- **빌드 도구**: 
- **상태 관리**: 
- **데이터 페칭**: 
- **UI 라이브러리**: 
- **테스트 러너**: 
- **핵심 패턴**: (2-3개 bullet)
- **주의사항**: (수상한 점, 이미 깨진 것)
