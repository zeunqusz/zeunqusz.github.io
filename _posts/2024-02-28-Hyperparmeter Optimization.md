---
layout: post
title: Hyperparameter Optimization
date: 2025-02-28
categories: [Machine Learning, Theory]
tags: [Hyperparameter, Grid Search, Random Search, Bayesian Optimization, Optuna]
---

# 하이퍼파라미터 최적화 기법 중 대표적인 4가지 방법
하이퍼파라미터 최적화 기법 중 대표적인 4가지 방법에는 Grid Search, Random Search, Bayesian Optimization, Optuna가 있다. 

하이퍼파라미터(Hyperparameter)란 모델 학습 전 사용자가 직접 설정해야 하는 값으로, 모델의 성능과 학습 과정에 큰 영향을 미친다. 이는 모델이 학습을 통해 자동으로 최적화하는 파라미터와 구별된다.
### 하이퍼파라미터 VS 파라미터 비교
| 구분 | 하이퍼파라미터 (Hyperparameter) | 파라미터 (Parameter) |
|------|--------------------------------|----------------------|
| **정의** | 사용자가 직접 설정하는 값 | 모델이 학습을 통해 자동으로 최적화하는 값 |
| **예시** | 학습률 (Learning Rate), 배치 크기 (Batch Size), 은닉층 개수 | 가중치 (Weight), 편향 (Bias) |
| **조정 방법** | Grid Search, Random Search, Bayesian Optimization | 역전파 (Backpropagation), Gradient Descent |
| **학습 과정** | 학습 전에 결정됨 | 학습하면서 업데이트됨 |

## 하이허파라미터 최적화의 필요성

하이퍼파라미터를 최적화하면 모델의 성능을 극대화하고 일반화 성능을 향상시킬 수 있다. 적절한 하이퍼파라미터를 설정하지 않으면 과적합(Overfitting) 또는 과소적합(Underfitting)이 발생할 수 있으며, 모델의 성능이 저하된다.


- 모델 성능 극대화
  - 잘 조정된 하이퍼파라미터는 모델의 예측 성능을 크게 향상시킬 수 있음
  - 학습률(learning rate),  배치크기(batch size), 정규화 계수(lambda) 등은 모델의 성능에 직접적인 영향을 미침
- 과적합(Overfitting) 방지
- 과소적합(Underfitting) 방지
- 학습 속도 최적화
- 일반화 성능 향상

## 주요 하이퍼파라미터 최적화 방법
![하이퍼파라미터 최적화 비교](/assets/images/hyperparameter_optimization.png)

1. Grid Search
- 미리 정의된 하이퍼파라미터 후보 값들의 모든 조합을 탐색하는 방식
- Ex) 두 개의 하이퍼파라미터  (x, y) 에 대해  x \in [0.1, 0.01, 0.001] ,  y \in [1, 10, 100] 이면 총  3 \times 3 = 9 개의 경우를 탐색

장점
- 탐색이 체계적으로 이루어져 최적의 하이퍼파라미터를 보장할 수 있음
- 설정한 범위 내에서 ::*모든 조합을 탐색하므로 재현성 높음*::

단점
- 조합이 많아질수록 탐색 시간이 급격히 증가(차원의 저주)
- 중요한 하이퍼파라미터 영역보다 절 중요한 영역에도 같은 연산 수행

2. Random Search
- 하이퍼파라미터 공간에서 무작위로 값을 선택하여 탐색하는 방식
- 일정한 반복 횟수(N) 동안 랜덤하게 하이퍼파라미터 값을 선택하여 모델을 평가

장점
- 탐색 공간이 커질수록 Grid Search보다 효율적
- 특정 영역에서 좋은 하이퍼파라미터를 찾을 확률이 높음
- 병렬 처리가 용이하여 실행 속도를 빠르게 할 수 있음

단점
- 최적의 하이퍼파라미터를 보장하지 않음
- 불필요한 탐색이 발생할 수 있음

Grid Search는 고정된 그리드에서 샘플링하지만, Random Search는 랜덤하게 샘플링하여 더 넓은 영역을 효율적으로 탐색할 수 있음

Ex) 100개의 실험을 한다면, Grid Search는 특정한 100개의 위치에서 평가하지만, Random Search는 더 고르게 분포된 100개 위치에서 평가됨.

3. Bayesian Optimization(베이지안 최적화)
- 이전 실험 결과를 바탕으로 확률 모델(Gaussian Process, Tree-based 모델 등)을 학습하여 탐색을 효율적으로 수행하는 방식
- 탐색랄 하이퍼파라미터를 확률적으로 예측하여 유망한 영역을 집중적으로 탐색

장점
- 기존 정보(이전 결과)를 활용하여 효율적인 탐색 가능
- 연산 비용을 줄이면서도 좋은 하이퍼파라미터를 찾을 가능성이 높음
- Random Search보다 적은 연산으로 더 나은 결과를 찾을 가능성이 큼

단점
- 구현이 복잡하고 계산량 많을 수 있음
- 고차원 공간에서 탐색이 어려울 수 있음

4. Optuna
- Bayesian Optimization을 기반으로 하는 Python 하이퍼파라미터 최적화 라이브러리
- Tree-structured Parzen Estimator(TPE) 알고리즘을 사용하여 Bayesian Optimization보다 효율적인 탐색을 지원
- Grid Search, Random Search, Bayesian Optimization의 단점을 보완하여 다양한 전략을 지원

장점
- 하이퍼파라미터 중요도를 자동으로 학습하여 최적화
- Early Stopping과 같은 기능을 활용하여 불필요한 계산 줄임
- 병렬 처리를 지원하여 계산 속도 빠르게 할 수 있음
- Pruning(비효율적인 탐색 조기 종료) 기능 지원

단점
- 학습 곡선이 일정하지 않을 수 있음
- Bayesian Optimization 보다 더 많은 하이퍼파라미터 조합이 필요할 수 있음

**실무에서는 Grid Search보다는 Random Search 또는 Bayesian Optimization을 더 많이 사용하며, 최근에는 Optuna 같은 라이브러리를 활용하여 자동화된 하이퍼파라미터 최적화를 수행하는 것이 일반적이다.**


### 1. Grid Search
그리드서치(Grid Search)는 머신러닝 모델의 하이퍼파라미터 최적화에서 사용되는 기법으로, 모든 가능한 하이퍼파라미터 조합을 체계적으로 탐색하여 최적의 조합을 찾는 방법이다. 이 방법은 각 하이퍼파라미터에 대해 미리 정의된 값들의 집합을 생성하고, 이들의 모든 가능한 조합을 평가하여 모델 성능을 극대화하는 데 사용된다.

Grid Search는 전수 조사(exhaustive search) 방식을 채택하여, 가능한 모든 하이퍼파라미터 조합을 평가한다. 이러한 접근 방식은 탐색 공간(search space) 내의 모든 지점을 격자 형태로 나누어 각 지점에서 모델을 학습시키고 검증하여 최적의 하이퍼파라미터를 찾는다.

Grid Search의 특징
- 체계적 탐색: 모든 하이퍼파라미터 조합을 일정한 간격으로 탐색하여 최적의 조합을 찾는다
- 병렬화 가능: 각 조합의 평가가 독립적이므로 병렬 처리를 통해 탐색 시간을 단축할 수 있다
- 계산 비용: 하이퍼파라미터의 수와 각 하이퍼파라미터의 후보 값이 많을수록 계산 비용이 기하급수적으로 증가하는 단점이 있다

Grid Search는 단순하고 구현이 용이하지만, 고차원의 하이퍼파라미터 공간에서는 계산 비용이 급격히 증가하는 문제가 있다. 이러한 문제를 해결하기 위해 Random Search나 Bayesian Optimization과 같은 방법이 제안되었다. 특히 Random Search는 하이퍼파라미터 공간에서 무작위로 조합을 선택해 탐색하는 방법으로, 고차원 공간에서 더 효율적일 수 있다. 또한 Bayesian Optimization은 이전의 탐색 결과를 기반으로 하이퍼파라미터 공간을 모델링하여 효율적으로 최적의 조합을 찾는 방법이다.

결국 Grid Search는 하이퍼파라미터 최적화의 기본적인 방법으로, 모든 가능한 조합을 체계적으로 탐색하여 최적의 하이퍼파라미터를 찾는다. 그러나 탐색 공간이 커질수록 계산 비용이 증가하므로, 이런 경우 Random Search나 Bayesian Optimization과 같은 대안적인 방법을 고려하는 것이 좋다.


### 2. Random Search
하이퍼파라미터 공간에서 무작위로 조합을 선택하여 최적의 하이퍼파라미터를 찾는 방법으로, Grid Search에 비해 계산 효율성을 높일 수 있는 장점이다.

전통적으로 Grid Search가 사용되어 왔으나, 하이퍼파라미터의 수와 각 하이퍼파라미터의 후보 값이 많을수록 계산 비용이 기하급수적으로 증가하는 문제가 있다. 이러한 문제를 해결하기 위해 Bergstra와 Bengio(2012)는 Random Search를 제안했다. 이들은 Random Search for Hyper-Parameter Optimization 논문에서, Random Search가 Grid Search보다 효율적이고 효과적일 수 있음을 입증했다.

Random Search 특징
- 하이퍼파라미터 공간의 일부를 무작위로 샘플링하여 탐색하므로, 계산 비용 줄일 수 있음
- 무작위 샘플링을 통해 하이퍼파라미터 공간의 다양한 영역 탐색 가능
- 구현이 간단하며, 병렬화가 용이함

Random Search는 효율적이지만, 탐색 과정에서 중요한 하이퍼파라미터 조합을 놓칠 수 있는 가능성이 있다. 이러한 한계를 보완하기 위해 Bayesian Optimization과 같은 기법이 제안되었다. Bayesian Optimization은 이전의 탐색 결과를 기반으로 하이퍼파라미터 공간을 모델링하여, 더 효율적으로 최적의 조합을 찾는 방법이다.

결론은, Random Search는 하이퍼파라미터 최적화에서 단순하면서도 효율적인 방법으로, 특히 하이퍼파라미터 공간이 클 때 유용하다. 그러나 중요한 조합을 놓칠 수 있는 가능성이 있어 Bayesian Optimization과 같은 기법과 함께 사용하여 최적화를 수행하는 것이 바람직하다.

### 3. Bayesian Optimization
비용이 많이 드는 블랙박스 함수의 전역 최적화를 위한 효율적인 방법으로, 하이퍼파라미터 최적화 등 다양한 분야에서 활용되고 있다. 이 기법은 베이지안 통계학을 기반으로, 서로게이트 모델(surrogate model)과 획득 함수(acquisition function)를 사용하여 목적 함수의 최소값 또는 최대 값을 찾는다.

베이지안 최적화는 미지의 목적 함수를 확률적 모델로 취급하여, 주어진 데이터에 따라 업데이트되는 사후 분포(posterior distribution)를 형성한다. 이러한 접근은 베이지안 정리를 기반으로 하며, 새로운 데이터가 추가될 때마다 모델이 업데이트되어 목적 함수의 형태를 점진적으로 추정한다. 이를 통해 함수 평가 횟수를 최소화하면서 최적점을 찾아낼 수 있다. 

Bayesian Optimization의 구성 요소
- 1. 서로게이트 모델
     - 실제 목적 함수를 근사하는 모델로, 주로 **가우시안 프로세스(Gaussian Process)**가 사용됨
     - 이 모델은 주어진 데이터로부터 목적 함수의 분포를 추정하여, 함수의 불확실성을 표현함
- 2. 획득 함수
    - 서로게이트 모델을 기반으로, 다음 평가할 지점을 결정하는 함수
    - 기대 향상(Expected Improvement), 최대 확률 개선(Probability of Improvement), 상한 신뢰 한계(Upper Confidence Bound) 등의 방법이 사용됨
    - 획득 함수는 탐색(exploration)과 활용(exploitation)의 균형을 조절하여 최적화를 효율적으로 진행함

Bayesian Optimization의 장점과 한계
장점
- 함수 평가 비용이 높은 문제에서 적은 평가 횟수로 최적해를 찾을 수 있음
- 하이퍼파라미터 최적화, 로브틱스, 과학 실험 설계 등 다양한 분야에 적용 가능

한계
- 고차원 공간에서는 서로게이트 모델의 복잡ㄱ성이 증가하여 효율성이 저하될 수 있음
- 잡음이 많은 함수나 비정상성을 가진 함수에서 모델링 어려울 수 있음
  
### 4. Optuna
Oputna는 하이퍼파라미터 최적화를 위한 차세대 프레임워크로, 사용자가 동적으로 탐색 공간을 정의하고 효율적인 최적화 과정을 수행할 수 있도록 설계되었다. 2019년 Akiba 등(2019)에 의해 소개되었으며, 다양한 머신러닝 및 딥러닝 모델 성능 향상을 위해 널리 사용되고 있다.

Optuna의 주요 특징
- 사용자가 코드 실행 중 **탐색 공간을 동적으로 구성**할 수 있어, 복잡한 모델이나 조건부 하이퍼파라미터 설정에 유연하게 대응할 수 있다.
- Optuna는 Tree-Structured Parzen Estimator(TPE)와 같은 샘플링 기법을 통해 하이퍼파라미터 공간을 효율적으로 탐색하며, 비효율적인 시도를 조기에 중단(pruning)하여 자원을 절약한다.
- TensorFlow, PyTorch, XGBoost, LightGBM 등 다양한 라이브러리와의 통합을 지원하며, 단일 머신부터 분산 환경까지 다양한 설정에서 활용할 수 있다.


## 참고문헌 (References)

<details>
  <summary>참고문헌 보기 📖</summary>

  - Liashchynskyi, P., & Liashchynskyi, P. (2019). **Grid Search, Random Search, Genetic Algorithm: A Big Comparison for NAS.**  
    *arXiv preprint arXiv:1912.06059.*  
    [[논문 링크]](https://arxiv.org/abs/1912.06059?utm_source=chatgpt.com)

  - **Scikit-learn: GridSearchCV**  
    [[공식 문서]](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html)

  - **Dremio: What is Grid Search?**  
    [[참고 자료]](https://www.dremio.com/wiki/grid-search/)

  ---

  - **Bergstra, J., & Bengio, Y. (2012).**  
    *Random Search for Hyper-Parameter Optimization.*  
    *Journal of Machine Learning Research, 13, 281-305.*  
    [[논문 링크]](https://www.jmlr.org/papers/volume13/bergstra12a/bergstra12a.pdf?utm_source=chatgpt.com)

  - **HyperParameter Optimization Algorithm (feat. GP / TPE) - Hoonst**  
    [[블로그 링크]](https://hoonst.github.io/2020/11/15/Algorithms-for-Hyperparameter-Optimization/?utm_source=chatgpt.com)

  - **[논문세미나 002] 하이퍼파라미터 최적화 목표를 정의하고 모델에 의존적이지 않은 Grid Search, Random Search 방법 등을 설명합니다 (김도형 연구원)**  
    [[영상 링크]](https://www.youtube.com/watch?v=U6bohNT-O5M&utm_source=chatgpt.com)

  ---

  - **Wang, X., Jin, Y., Schmitt, S., & Olhofer, M. (2022).**  
    *Recent Advances in Bayesian Optimization.*  
    *arXiv preprint arXiv:2206.03301.*  
    [[논문 링크]](https://arxiv.org/abs/2206.03301?utm_source=chatgpt.com)

  - **Paulson, J. A., & Tsay, C. (2024).**  
    *Bayesian Optimization as a Flexible and Efficient Design Framework for Sustainable Process Systems.*  
    *arXiv preprint arXiv:2401.16373.*  
    [[논문 링크]](https://arxiv.org/abs/2401.16373?utm_source=chatgpt.com)

  - **Wikipedia contributors. (2023).**  
    *Bayesian Optimization.*  
    *Wikipedia, The Free Encyclopedia.*  
    [[위키백과 링크]](https://en.wikipedia.org/wiki/Bayesian_optimization?utm_source=chatgpt.com)

  - **Brochu, E., Cora, V. M., & de Freitas, N. (2010).**  
    *A Tutorial on Bayesian Optimization of Expensive Cost Functions, with Application to Active User Modeling and Hierarchical Reinforcement Learning.*  
    *arXiv preprint arXiv:1012.2599.*  
    [[논문 링크]](https://arxiv.org/abs/1012.2599?utm_source=chatgpt.com)

  ---

  - **Akiba, T., Sano, S., Yanase, T., Ohta, T., & Koyama, M. (2019).**  
    *Optuna: A Next-generation Hyperparameter Optimization Framework.*  
    *arXiv preprint arXiv:1907.10902.*  
    [[논문 링크]](https://arxiv.org/abs/1907.10902?utm_source=chatgpt.com)

  - **Shekhar, S., Bansode, A., & Salim, A. (2022).**  
    *A Comparative Study of Hyper-Parameter Optimization Tools.*  
    *arXiv preprint arXiv:2201.06433.*  
    [[논문 링크]](https://arxiv.org/abs/2201.06433?utm_source=chatgpt.com)

  - **Optuna 기초 사용법.**  
    [[블로그 링크]](https://velog.io/%40kyyle/Optuna-%EA%B8%B0%EC%B4%88?utm_source=chatgpt.com)

</details>
