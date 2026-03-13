# 🔀 Git 협업 퀵스타트 가이드

이 문서는 Git을 처음 사용하는 팀원을 위한 실전 가이드입니다.

---

## 📋 최초 1회 세팅

### 1단계: Git 설치 확인
```bash
git --version
# git version 2.xx.x 가 나오면 OK
```

### 2단계: 사용자 정보 등록
```bash
git config --global user.name "홍길동"
git config --global user.email "gildong@email.com"
```

### 3단계: GitHub 저장소 생성
1. https://github.com 에서 **New Repository** 클릭
2. Repository name: `stress-prediction`
3. **Private** 선택 (대회 코드이므로)
4. "Add a README file" 체크 **해제** (우리가 올릴 거임)
5. **Create repository** 클릭

### 4단계: 로컬 → GitHub 연결
```bash
cd stress-prediction    # 프로젝트 폴더로 이동

git init
git add .
git commit -m "init: 프로젝트 초기 구조 세팅"
git branch -M main
git remote add origin https://github.com/<팀계정>/stress-prediction.git
git push -u origin main
```

### 5단계: 팀원 초대
GitHub 저장소 → **Settings** → **Collaborators** → 팀원 GitHub ID 추가

### 6단계: 팀원이 클론
```bash
git clone https://github.com/<팀계정>/stress-prediction.git
cd stress-prediction
```

---

## 🔄 매일 작업 흐름 (반복)

### 시작할 때 (최신 코드 받기)
```bash
git checkout main
git pull origin main
```

### 내 작업 브랜치 만들기
```bash
# 피처 작업 예시
git checkout -b feature/fe-cholesterol-bins

# 모델 튜닝 예시
git checkout -b feature/model-xgb-depth6
```

### 작업 중 저장 (커밋)
```bash
git add .
git commit -m "feat: 콜레스테롤 구간 피처 추가"
```

### GitHub에 올리기
```bash
git push origin feature/fe-cholesterol-bins
```

### Pull Request 생성 (GitHub 웹)
1. GitHub 저장소 페이지에서 **"Compare & pull request"** 버튼 클릭
2. PR 템플릿에 **실험 결과(MAE)** 기록
3. 팀원에게 리뷰 요청
4. 승인 후 **Merge** 클릭

### 머지 후 정리
```bash
git checkout main
git pull origin main
git branch -d feature/fe-cholesterol-bins    # 로컬 브랜치 삭제
```

---

## ⚠️ 자주 겪는 상황별 대처

### 상황 1: push 했더니 거부됨
```bash
# 다른 팀원이 먼저 push한 경우
git pull origin main --rebase
git push origin feature/내브랜치
```

### 상황 2: 같은 파일을 동시에 수정 (충돌)
```bash
git pull origin main

# 충돌 발생 시 파일에 아래 같은 표시가 생김:
# <<<<<<< HEAD
# 내 코드
# =======
# 상대방 코드
# >>>>>>> main

# 1. 파일 열어서 원하는 코드만 남기고 마커 삭제
# 2. 저장 후:
git add .
git commit -m "fix: config.py 충돌 해결"
git push
```

### 상황 3: 실수로 main에 직접 커밋함
```bash
# 아직 push 안 했으면:
git branch feature/실수구제      # 현재 커밋을 새 브랜치로 복사
git checkout main
git reset --hard origin/main    # main을 원래대로 되돌림
git checkout feature/실수구제    # 새 브랜치에서 작업 계속
```

### 상황 4: 데이터 파일을 실수로 커밋함
```bash
# .gitignore에 있지만 이미 추적 중이면:
git rm --cached data/train.csv
git commit -m "fix: 데이터 파일 추적 제거"
```

---

## 🗂️ 누가 뭘 수정하나?

| 파일 | 담당 | 수정 시점 |
|------|------|----------|
| `src/config.py` | 모두 | 하이퍼파라미터 변경할 때 |
| `src/preprocess.py` | 피처 담당 | 새 피처 추가/전처리 변경 |
| `src/models.py` | 모델 담당 | 새 모델 추가/앙상블 변경 |
| `src/train.py` | 가급적 미수정 | 파이프라인 변경 필요 시만 |
| `notebooks/` | 자유 | 개인 실험 |

> 💡 **충돌 최소화 팁**: 각자 담당 파일만 수정하면 충돌이 거의 안 납니다!

---

## 📌 필수 명령어 요약

```bash
git status              # 현재 상태 확인
git log --oneline -10   # 최근 커밋 10개 확인
git diff                # 변경 내용 확인
git stash               # 임시 저장 (브랜치 전환 전)
git stash pop           # 임시 저장 복원
git branch              # 브랜치 목록
git checkout main       # main으로 이동
git checkout -b 이름    # 새 브랜치 생성 + 이동
```
