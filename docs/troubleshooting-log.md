# Troubleshooting Log

Git 트러블슈팅 4종 시나리오를 실제로 수행하고 기록합니다.

## 작성 규칙

- 4개 시나리오는 **팀 전체가 모두** 수행하고, 각 섹션을 채웁니다.
- 팀원은 **최소 1개 시나리오**에 참여하며, 참여자란에 **이름과 역할**을 적습니다.
  - 역할 예: 수행, 기록, 검증(리뷰)
- 명령은 실제로 실행한 순서대로, 출력(일부)과 함께 남겨 다른 사람이 재현할 수 있게 합니다.
- 공유 브랜치(`main`)에서는 히스토리 재작성(`reset`, `amend` 후 force push)을 하지 않습니다.
  - `amend`, `reset --soft`, `stash`는 **push 전 개인 feature 브랜치**에서 수행합니다.
  - `revert`는 이미 `main`에 병합된 커밋을 대상으로, **revert 커밋을 담은 PR**로 병합합니다.

> 담당/상태는 각 시나리오를 수행하는 **작업 PR에서 담당자가 직접 갱신**합니다(⬜ 미수행 → ✅ 완료).

| 시나리오 | 명령 | 담당 | 상태 |
|---|---|---|---|
| 1. amend | `git commit --amend` | TBD | ⬜ |
| 2. reset --soft | `git reset --soft HEAD~1` | TBD | ⬜ |
| 3. revert | `git revert <commit>` | TBD | ⬜ |
| 4. stash | `git stash` / `git stash pop` | TBD | ⬜ |

---

## 시나리오 1: amend (최근 커밋 메시지 수정)

### 참여자
- <name> (역할)

### 상황
- 문제가 무엇이었는지(재현 가능한 설명)

### 시도한 명령/절차
```bash
git log --oneline -1
git commit --amend -m "<수정한 메시지>"
git log --oneline -1
```

### 결과
- 무엇이 어떻게 해결됐는지
- 주의할 점(원격 히스토리/협업 영향)

### 왜 이 방법을 선택했는가(Why)
- 

---

## 시나리오 2: reset --soft (로컬 커밋 취소 + 변경 유지)

### 참여자
- <name> (역할)

### 상황
- 

### 시도한 명령/절차
```bash
git log --oneline -2
git reset --soft HEAD~1
git status
```

### 결과
- 
- 주의할 점: 

### 왜 이 방법을 선택했는가(Why)
- `--soft` / `--mixed` / `--hard` 중 `--soft`를 고른 이유

---

## 시나리오 3: revert (원격에 push된 커밋 취소)

### 참여자
- <name> (역할)

### 상황
- 

### 시도한 명령/절차
```bash
git switch -c feature/<name>-revert-<topic> main
git revert <commit>
git push -u origin feature/<name>-revert-<topic>
# PR 생성 → 리뷰 → 병합
```

### 결과
- 
- 관련 PR: <url>

### 왜 이 방법을 선택했는가(Why)
- `reset` 대신 `revert`를 선택한 이유

---

## 시나리오 4: stash / stash pop (작업 보관 후 전환)

### 참여자
- <name> (역할)

### 상황
- 

### 시도한 명령/절차
```bash
git stash push -m "<보관 이유>"
git switch <other-branch>
# 다른 작업 수행
git switch <original-branch>
git stash pop
```

### 결과
- 
- 주의할 점: 

### 왜 이 방법을 선택했는가(Why)
- 임시 커밋 대신 `stash`를 쓴 이유
