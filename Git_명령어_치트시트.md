# Git/GitHub 명령어 치트시트
## Windows + VSCode 환경

---

## 📌 최초 설정 (컴퓨터당 1회만)

```bash
git config --global user.name "홍길동"
git config --global user.email "hong@example.com"
```
**의미**: Git 커밋에 표시될 이름과 이메일 설정

```bash
git config --list
```
**의미**: 설정된 정보 확인

---

## 🚀 프로젝트 시작하기

### 방법 1: 새 프로젝트 시작
```bash
git init
```
**의미**: 현재 폴더를 Git 저장소로 초기화 (`.git` 폴더 생성)

### 방법 2: GitHub에서 가져오기
```bash
git clone https://github.com/사용자명/저장소명.git
```
**의미**: GitHub 저장소를 내 컴퓨터로 복사

### 방법 3: 로컬 프로젝트를 GitHub에 연결
```bash
git remote add origin https://github.com/사용자명/저장소명.git
```
**의미**: 로컬 저장소와 GitHub 원격 저장소 연결  
**origin**: 원격 저장소의 별칭 (기본 이름)

```bash
git remote -v
```
**의미**: 연결된 원격 저장소 확인

---

## 📝 기본 작업 흐름 (가장 많이 사용)

### 1단계: 현재 상태 확인
```bash
git status
```
**의미**: 변경된 파일, 스테이징된 파일 등 현재 상태 확인  
**👉 작업 전후로 항상 확인하는 습관!**

### 2단계: 변경사항 스테이징 (커밋 준비)
```bash
git add 파일명.py
```
**의미**: 특정 파일만 커밋 준비 영역에 추가

```bash
git add .
```
**의미**: 모든 변경된 파일을 커밋 준비 영역에 추가  
**👉 가장 많이 사용하는 명령어**

```bash
git add *.py
```
**의미**: 특정 확장자 파일만 추가 (예: 모든 .py 파일)

### 3단계: 커밋 (변경사항 저장)
```bash
git commit -m "로그인 기능 추가"
```
**의미**: 스테이징된 변경사항을 로컬 저장소에 저장  
**-m**: 커밋 메시지 (변경 내용 설명)

```bash
git commit -am "버그 수정"
```
**의미**: add + commit 동시에 (단, 새 파일은 불가능)

### 4단계: GitHub에 업로드
```bash
git push origin main
```
**의미**: 로컬 커밋을 GitHub의 main 브랜치에 업로드  
**origin**: 원격 저장소  
**main**: 브랜치 이름

```bash
git push
```
**의미**: 현재 브랜치를 기본 원격 브랜치에 푸시 (간단 버전)

### 5단계: GitHub에서 최신 코드 가져오기
```bash
git pull origin main
```
**의미**: GitHub의 최신 변경사항을 가져와서 현재 브랜치에 병합

```bash
git pull
```
**의미**: 현재 브랜치의 기본 원격 브랜치에서 가져오기

---

## 🔍 변경사항 확인하기

```bash
git status
```
**의미**: 현재 작업 상태 (변경된 파일, 스테이징 상태 등)

```bash
git diff
```
**의미**: 작업 중인 파일의 변경사항 상세 비교 (아직 add 안 한 것)

```bash
git diff --staged
```
**의미**: 스테이징된 파일의 변경사항 비교 (add 했지만 commit 안 한 것)

```bash
git log
```
**의미**: 커밋 히스토리 보기 (길게)

```bash
git log --oneline
```
**의미**: 커밋 히스토리 간단하게 보기 (추천)

```bash
git log --oneline --graph --all
```
**의미**: 모든 브랜치의 커밋을 그래프로 시각화

---

## 🌿 브랜치 (Branch) 작업

### 브랜치란?
독립적인 작업 공간. 원본(main)에 영향 없이 새 기능을 개발할 수 있음

```
main    ──●──●──●──●──●──●  (원본)
             │        ↑
             │      merge
             ↓        │
feature  ──●──●──●──●      (새 기능 개발)
```

### 브랜치 보기
```bash
git branch
```
**의미**: 로컬 브랜치 목록 보기 (* 표시가 현재 브랜치)

```bash
git branch -a
```
**의미**: 로컬 + 원격 브랜치 모두 보기

### 브랜치 생성
```bash
git branch feature/login
```
**의미**: `feature/login` 이름의 새 브랜치 생성 (이동은 안 함)

### 브랜치 이동
```bash
git checkout feature/login
```
**의미**: `feature/login` 브랜치로 이동

```bash
git switch feature/login
```
**의미**: 브랜치 이동 (최신 방식, checkout보다 명확)

### 브랜치 생성 + 이동 (한 번에)
```bash
git checkout -b feature/signup
```
**의미**: 새 브랜치 만들고 바로 이동 (가장 많이 사용)

```bash
git switch -c feature/signup
```
**의미**: 위와 동일 (최신 방식)

### 브랜치 병합
```bash
git checkout main
git merge feature/login
```
**의미**: 
1. main 브랜치로 이동
2. feature/login 브랜치의 변경사항을 main에 합치기

### 브랜치 삭제
```bash
git branch -d feature/login
```
**의미**: 병합이 완료된 브랜치 삭제 (안전한 삭제)

```bash
git branch -D feature/login
```
**의미**: 강제 삭제 (병합 안 됐어도 삭제)

```bash
git push origin --delete feature/login
```
**의미**: 원격(GitHub)의 브랜치 삭제

---

## ⏪ 되돌리기 (실수했을 때)

### 파일 변경 취소 (아직 add 안 함)
```bash
git checkout -- 파일명.py
```
**의미**: 특정 파일의 변경사항 취소 (작업 내용 삭제됨!)

```bash
git restore 파일명.py
```
**의미**: 위와 동일 (최신 방식)

### 스테이징 취소 (add 취소)
```bash
git reset HEAD 파일명.py
```
**의미**: add한 파일을 스테이징에서 제거 (파일 변경사항은 유지)

```bash
git restore --staged 파일명.py
```
**의미**: 위와 동일 (최신 방식)

### 커밋 취소
```bash
git reset --soft HEAD~1
```
**의미**: 최근 커밋 1개 취소, 변경사항은 스테이징 상태로 유지

```bash
git reset --mixed HEAD~1
```
**의미**: 최근 커밋 1개 취소, 변경사항은 작업 디렉토리로 (기본값)

```bash
git reset --hard HEAD~1
```
**의미**: 최근 커밋 1개 취소, 변경사항도 모두 삭제 (위험! 복구 불가)

```bash
git revert 커밋해시
```
**의미**: 특정 커밋을 되돌리는 새 커밋 생성 (안전한 방법)

---

## 🔄 협업 작업 흐름

### 매일 작업 시작 전
```bash
git checkout main
git pull origin main
git checkout -b feature/new-task
```
**순서**:
1. main 브랜치로 이동
2. 최신 코드 받아오기
3. 새 작업용 브랜치 생성

### 작업 완료 후
```bash
git add .
git commit -m "작업 내용 설명"
git push origin feature/new-task
```
**순서**:
1. 변경사항 스테이징
2. 커밋
3. GitHub에 푸시

### Pull Request (PR) 후 병합 완료되면
```bash
git checkout main
git pull origin main
git branch -d feature/new-task
```
**순서**:
1. main으로 이동
2. 병합된 최신 코드 받기
3. 로컬 브랜치 삭제

---

## 🚨 충돌 해결

### 충돌 발생 시
```bash
git merge feature/branch
# CONFLICT 메시지 발생!
```

**해결 방법**:
1. VSCode에서 충돌 파일 열기
2. `<<<<<<< HEAD`, `=======`, `>>>>>>>` 표시 확인
3. 원하는 코드 선택 (VSCode의 "Accept Current Change" 버튼 사용)
4. 충돌 표시 제거 후 저장

```bash
git add .
git commit -m "충돌 해결"
```

---

## 📊 유용한 명령어

```bash
git stash
```
**의미**: 현재 작업을 임시 저장 (커밋하지 않고 브랜치 변경 가능)

```bash
git stash pop
```
**의미**: 임시 저장한 작업 다시 가져오기

```bash
git fetch origin
```
**의미**: 원격 저장소의 변경사항 확인 (병합은 안 함)

```bash
git remote show origin
```
**의미**: 원격 저장소 상세 정보 보기

```bash
git clean -fd
```
**의미**: 추적되지 않는 파일 삭제 (주의!)

---

## 💡 자주 사용하는 조합

### 새 기능 개발 시작
```bash
git checkout main
git pull
git checkout -b feature/login-page
```

### 작업 완료 후 푸시
```bash
git add .
git commit -m "로그인 페이지 UI 완성"
git push origin feature/login-page
```

### 다른 브랜치 작업 중 긴급 수정 필요할 때
```bash
git stash                    # 현재 작업 임시 저장
git checkout main            # main으로 이동
git checkout -b hotfix/bug   # 긴급 수정 브랜치
# 수정 작업...
git add .
git commit -m "긴급 버그 수정"
git push origin hotfix/bug
git checkout feature/login-page  # 원래 작업 브랜치로
git stash pop                # 임시 저장한 작업 복원
```

---

## 🎯 브랜치 이름 규칙 (권장)

- `feature/기능명` - 새 기능 (예: feature/user-authentication)
- `bugfix/버그명` - 버그 수정 (예: bugfix/login-error)
- `hotfix/긴급수정` - 긴급 수정 (예: hotfix/security-patch)
- `docs/문서명` - 문서 작업 (예: docs/readme-update)

---

## ⚙️ VSCode에서 Git 사용하기

### 단축키
- `Ctrl + Shift + G` - 소스 제어 패널 열기
- `Ctrl + Enter` - 커밋 (메시지 입력 후)

### GUI 기능
- 왼쪽 하단 브랜치명 클릭 → 브랜치 전환
- 소스 제어 패널에서 `+` 버튼 → git add
- 파일 우클릭 → "변경 내용 취소" → git checkout

### 추천 확장 프로그램
- **GitLens** - Git 기능 강화
- **Git Graph** - 브랜치 시각화
- **Git History** - 파일별 히스토리

---

## 📚 커밋 메시지 작성 팁

```bash
git commit -m "feat: 로그인 기능 추가"
git commit -m "fix: 회원가입 버그 수정"
git commit -m "docs: README 업데이트"
git commit -m "style: 코드 포맷팅"
git commit -m "refactor: 인증 로직 개선"
```

**규칙**:
- 명령형으로 작성 ("추가했음" ❌, "추가" ✅)
- 간결하고 명확하게
- 한글 or 영어 일관성 유지

---

## 🆘 문제 해결

### "Your branch is ahead of 'origin/main'"
```bash
git push
```
**의미**: 로컬 커밋이 있는데 푸시 안 했음

### "Your branch is behind 'origin/main'"
```bash
git pull
```
**의미**: 원격에 새 커밋이 있음

### push가 거부될 때
```bash
git pull --rebase origin main
git push
```
**의미**: 원격 변경사항 먼저 받고 내 커밋을 그 위에 적용

### 잘못된 커밋 메시지 수정
```bash
git commit --amend -m "올바른 메시지"
```
**의미**: 마지막 커밋 메시지 수정 (아직 푸시 안 한 경우만)

---

## ✅ 체크리스트

### 매일 작업 시작
- [ ] `git pull` - 최신 코드 받기
- [ ] `git checkout -b feature/작업명` - 새 브랜치 생성

### 작업 중
- [ ] `git status` - 자주 확인
- [ ] 의미있는 단위로 커밋

### 작업 완료
- [ ] `git push` - GitHub에 업로드
- [ ] Pull Request 생성
- [ ] 코드 리뷰 받기
- [ ] 병합 후 로컬 브랜치 삭제

---

## 🎓 학습 팁

1. **처음엔 이것만**: `status`, `add .`, `commit`, `push`, `pull`
2. **익숙해지면**: 브랜치 생성, 병합
3. **마스터 단계**: rebase, stash, cherry-pick

**연습 방법**: 테스트 저장소 만들어서 실험해보기!

---

이 파일을 출력하거나 모니터 옆에 두고 참고하세요! 🚀
