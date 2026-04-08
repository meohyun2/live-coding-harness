# live-coding-harness

React + TypeScript 라이브 코딩 전형 대응 Claude Code 플러그인.

## 포함 커맨드

| 커맨드 | 용도 |
|---|---|
| `/orient [포커스]` | 코드베이스 구조 파악 |
| `/debug <버그 설명>` | 버그 원인 추적 및 수정 |
| `/feature <기능 설명>` | 기존 패턴 따라 기능 추가 |
| `/refactor <대상>` | 동작 유지 리팩토링 |
| `/fix-ts [파일/에러]` | TypeScript 에러 일괄 수정 |
| `/review` | 제출 전 코드 검토 + 평가자용 요약 |

## 훅

- **UserPromptSubmit**: 모든 프롬프트를 `~/harness/prompt-log.md`에 자동 기록

## 설치

### 1. 이 저장소를 마켓플레이스로 등록

`~/.claude/settings.json`의 `extraKnownMarketplaces`에 추가:

```json
"live-coding-harness-marketplace": {
  "source": {
    "source": "github",
    "repo": "<YOUR_USERNAME>/live-coding-harness"
  }
}
```

### 2. Claude Code에서 설치

```
/plugins → live-coding-harness-marketplace → install
```

### 3. 프롬프트 로그 파일 초기화

```bash
touch ~/harness/prompt-log.md
```

## 사용 순서 (라이브 코딩 전형)

1. 코드베이스 수령 → `/orient`
2. 과제 파악 → `/debug` / `/feature` / `/refactor`
3. TS 에러 발생 시 → `/fix-ts`
4. 제출 전 → `/review`
