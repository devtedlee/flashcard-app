# Flashcard App

SM-2 간격반복 기반 학습 카드 앱. GitHub Pages로 배포, Gist API로 진도 동기화.

## 구조

- `index.html` — 앱 전체 (CSS + HTML + JS, 단일 파일)
- `cards.json` — 모든 카드 데이터 (플랫 배열)
- `.github/workflows/deploy.yml` — GitHub Pages 자동 배포

## cards.json 카드 추가 가이드

### 카드 형식

```json
{
  "id": "op-050",
  "deck": "연산자 · C/C++/Java",
  "front": "★ 질문 텍스트",
  "back": "답변 첫째 줄§답변 둘째 줄§→ 보충 설명",
  "tags": ["증감"]
}
```

### 필드 규칙

| 필드 | 규칙 |
|------|------|
| `id` | 덱 내에서 유일. 접두사-번호 형식 권장 (예: `op-050`, `db-001`) |
| `deck` | 홈 화면 목록 단위. 같은 값의 카드끼리 한 덱으로 묶임 |
| `front` | 질문. `★`로 시작하면 핵심 카드로 필터링 가능 |
| `back` | 답변. `§`로 줄 구분. `` `코드` ``는 `<code>` 태그로 렌더링. `→`로 시작하는 줄은 강조 표시 |
| `tags` | 덱 내 주제 필터용. 칩 UI에 표시됨 |

### 새 덱 추가

`deck` 값만 다른 카드를 추가하면 홈 화면에 자동 노출. 코드 수정 불필요.

```json
{"id": "db-001", "deck": "데이터베이스 · SQL", "front": "DDL의 종류는?", "back": "CREATE§ALTER§DROP§TRUNCATE", "tags": ["DDL"]}
```

### 기존 덱에 카드 추가

같은 `deck` 값으로 `id`만 유일하게 추가.

### SM-2 상태

학습 진도는 `localStorage` + GitHub Gist에 저장. `cards.json`과 독립적이라 카드를 추가/삭제해도 기존 진도에 영향 없음.
