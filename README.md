# K-평균 군집화 모델 구현 (Iris 데이터셋)

## 📌 프로젝트 목적
**K-Means 군집화 알고리즘의 작동 원리**를 이해하기 위해 Scikit-learn 라이브러리의 구현체를 사용하지 않고, **Python으로 구현**한 코드입니다.

## 🎯 학습 목표
- K-Means 군집화 알고리즘의 핵심 개념 이해
- 유클리드 거리 기반 클러스터 할당 메커니즘 학습
- 중심점(Centroid) 업데이트 및 수렴 조건 이해

## 🛠️ 주요 특징 및 구현 세부 사항

### 1. 의존성
- `scikit-learn`: Iris 데이터셋 로드
- `matplotlib`: 군집화 결과 시각화
- `math`: 유클리드 거리 계산
- `random`: 초기 중심점 무작위 선택

### 2. 데이터 및 하이퍼파라미터

#### 데이터셋
- **데이터**: Iris 데이터셋 (총 150개 샘플)
- **사용 특징**: Petal Length, Petal Width (2차원)
  - `X = iris.data[:, 2:]` (인덱스 2, 3)
  - **선택 이유**: 2차원 시각화가 용이하며, 이 두 특징만으로도 종 구분이 잘 되기때문

#### 하이퍼파라미터
- **클러스터 개수(k)**: 3
- **최대 반복 횟수**: 100
- **수렴 임계값**: 1e-4 (중심점 변화가 이보다 작으면 수렴으로 판단)

### 3. K-Means 핵심 로직

#### 알고리즘 단계
```
1. 초기화 (Initialization)
   └─ 데이터에서 k개 샘플을 무작위로 선택하여 초기 중심점으로 설정

2. 할당 단계 (Assignment Step)
   └─ 각 데이터 포인트를 가장 가까운 중심점의 클러스터에 할당

3. 업데이트 단계 (Update Step)
   └─ 각 클러스터에 속한 데이터 포인트들의 평균으로 중심점 갱신

4. 수렴 확인 (Convergence Check)
   └─ 중심점 변화량 < 임계값(1e-4) → 종료
   └─ 그렇지 않으면 2번으로 돌아감 (최대 100회까지 반복)
```

### 4. 코드 구조
```
euclidean_distance(point1, point2)  # 두 점 사이의 유클리드 거리 계산
│
└─ K-Means 메인 루프
   ├─ 1. 초기 중심점 설정 (random.sample)
   ├─ 2. 반복 (최대 100회)
   │   ├─ 할당: 각 점을 가장 가까운 중심점에 할당
   │   ├─ 업데이트: 클러스터 평균으로 중심점 갱신
   │   └─ 수렴 확인: 중심점 변화 < 1e-4
   └─ 3. 시각화 (matplotlib)
```

## 🖥️ 실행 방법

### 1. 환경 설정
```bash
!pip install scikit-learn matplotlib
```

### 2. 실행
Jupyter Notebook 환경에서 `sun_kmeans.ipynb` 파일의 셀을 순서대로 실행합니다.

### 3. Google Colab에서 실행
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1Oq8mDO2fEaB0v2Lvne8oU91O81kdIO1X?usp=sharing)

## 📈 실행 결과

### 수렴 정보
- **총 반복 횟수**: 11회
- **수렴 이유**: 중심점 변화량이 임계값(1e-4) 미만으로 감소
- **종료 조건**: 조기 수렴 (최대 반복 100회 중 11회에서 완료)

### 클러스터 분포
| 클러스터 | 데이터 개수 | 비율 |
|---------|-----------|------|
| Cluster 0 | 50개 | 33.3% |
| Cluster 1 | 54개 | 36.0% |
| Cluster 2 | 46개 | 30.7% |
| **합계** | **150개** | **100%** |

### 실제 라벨과의 비교
```
클러스터 0: Setosa 50개 (순도 높음)
클러스터 1: Virginica 50개 (일부 Versicolor 혼합)
클러스터 2: Versicolor 50개 (일부 Virginica 혼합)
```
