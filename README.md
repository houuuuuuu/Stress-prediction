# 🧠 스트레스 지수 예측 (Stress Score Prediction)

AI 대회용 스트레스 지수 예측 프로젝트입니다.  
SVR, XGBoost, CatBoost, LightGBM 등 다양한 모델의 앙상블 + 스태킹으로 최적 MAE를 달성합니다.

---

## 📁 프로젝트 구조

```
stress-prediction/
├── README.md                  # 프로젝트 설명
├── requirements.txt           # 패키지 의존성
├── .gitignore                 # Git 제외 파일
├── data/                      # 데이터 (Git 추적 X)
│   ├── train.csv
│   ├── test.csv
│   └── sample_submission.csv
├── notebooks/                 # 실험용 노트북
│   └── 스트레스지수_예측.ipynb
├── src/                       # 모듈화된 소스코드
│   ├── preprocess.py          # 전처리 + 피처 엔지니어링
│   ├── models.py              # 모델 정의
│   ├── train.py               # 학습 파이프라인
│   └── config.py              # 설정값 관리
├── outputs/                   # 제출 파일 (Git 추적 X)
└── models/                    # 저장된 모델 (Git 추적 X)
```

---

## 🚀 시작하기

### 1. 저장소 클론
```bash
git clone https://github.com/<팀계정>/stress-prediction.git
cd stress-prediction
```

### 2. 환경 설정
```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 3. 데이터 준비
`data/` 폴더에 `train.csv`, `test.csv`, `sample_submission.csv`를 넣어주세요.  
(데이터는 .gitignore로 제외되어 있습니다)

### 4. 학습 실행
```bash
python src/train.py
```

---

## 🔀 Git 협업 워크플로우

### 브랜치 전략 (GitHub Flow)

```
main ─────────────────────────────────────────── (배포용, 보호)
  ├── feature/fe-bmi-interaction    ← 피처 엔지니어링
  ├── feature/model-catboost-tune   ← 모델 튜닝
  ├── feature/stacking-meta         ← 스태킹 실험
  └── fix/data-leakage              ← 버그 수정
```

### 작업 흐름

```bash
# 1. 최신 main 가져오기
git checkout main
git pull origin main

# 2. 작업 브랜치 생성
git checkout -b feature/내작업이름

# 3. 코드 수정 후 커밋
git add .
git commit -m "feat: BMI 교호작용 피처 추가"

# 4. 원격에 푸시
git push origin feature/내작업이름

# 5. GitHub에서 Pull Request 생성 → 팀원 코드리뷰 → Merge
```

### 커밋 메시지 규칙

| 접두사 | 용도 | 예시 |
|--------|------|------|
| `feat:` | 새 기능/피처 | `feat: 혈압 파생변수 3종 추가` |
| `fix:` | 버그 수정 | `fix: LabelEncoder 순서 통일` |
| `refactor:` | 코드 개선 | `refactor: 전처리 함수 모듈화` |
| `exp:` | 실험 | `exp: SVR gamma=0.1 시도` |
| `docs:` | 문서 | `docs: README 업데이트` |

---

## 🤝 협업 규칙

1. **main 브랜치에 직접 push 금지** → 반드시 PR을 통해 merge
2. **PR에 실험 결과(MAE) 포함** → CV 점수 비교표 첨부
3. **데이터/모델 파일은 Git에 올리지 않기** → .gitignore 활용
4. **노트북은 실험용, 최종 코드는 src/에 모듈화**
5. **충돌 시 `git rebase`보다 `git merge` 사용 권장** (초보자 친화적)

---

## 📊 현재 성능

| 모델 | CV MAE | 비고 |
|------|--------|------|
| SVR (RBF) | - | C=10, epsilon=0.01 |
| XGBoost | - | lr=0.03, depth=4 |
| CatBoost | - | lr=0.03, depth=5 |
| LightGBM | - | lr=0.03, leaves=20 |
| **Stacking+Blend** | - | 최종 제출 |

🎉 Optimization Results
Best MAE (CV) : 0.138088
C             : 21.246601
gamma         : 0.976670
epsilon       : 0.000010

Strategy           | OOF MAE Score  
----------------------------------------
Full (Single)      | 0.138090
K-Fold             | 0.138090
Multi-Seed         | 0.139143
Blend              | 0.138483

> PR 시 위 표를 업데이트해 주세요!

---

## 👥 팀원

| 이름 | 담당 | 브랜치 |
|------|------|--------|
| - | 전처리/피처 | `feature/fe-*` |
| - | 모델 튜닝 | `feature/model-*` |
| - | 앙상블/스태킹 | `feature/stacking-*` |
