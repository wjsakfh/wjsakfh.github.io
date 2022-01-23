---
layout: category
title:  "머신러닝 엔지니어링 실전 1 - 모델 선정과 Variance, Bias 문제파악"
categories: Research
tag: [Machine Learning, Andrew Ng, Engineering, Machine Learning Engineering, Engineer, Model Selection, Varince, Bias, Over-fitting, Under-fitting]
toc: true
author_profile: true
search: true
---

# 머신러닝 엔지니어링 실전 1 - 모델 선정과 Variance, Bias 문제파악

## Model Selection - 어떻게 모델을 선정할 것인가

- 머신러닝 모델을 잘 만들었다고 머신러닝 Task가 끝나는 것은 아니다. 그 많은 하이퍼 파라미터를 어떻게 고칠 것인가 ?부터 시작해서 나의 모델은 어떤 문제가 있는가? 파악하고 어떻게 개선할 것인가?를 결정하는 일련의 과정이 필요하다. 하지만 많은 사람들은 모델을 만들고 단순히 gut feeling (직감) 으로 개선 해야할 방향을 결정한다.  이는 논리적이지 않은 판단일뿐더러 개인 또는 팀에 막대한 시간소요를 줄 수도 있다. 실제로 많은 팀에서 아직 이러한 실수를 반복하는 것으로 안다.

- 따라서 내가 만든 알고리즘 또는 모델이 잘 작동하는지 평가하는 방법 필요하다. (debugging a learning algorithm)

  - 머신러닝에서 평가하는 방법은 간단하다. 

    1) 데이터셋을 Training set과 Test set으로 나눈다

    2) Training set으로 모델의 학습파라미터들을 학습시킨다. 

    3) Test set 에서 학습된 모델을 테스트하여 에러를 산정한다.

- 산정된 에러로부터 우리는 최적의 모델을 선택할 수 있다. (model selection)

  - Test set으로만 에러를 계산하고 그 중 가장 낮은 에러를 갖는 모델(가장 Generalized 잘된 모델)을 선택해도 되지만, 이 경우에 Test set에만 피팅된 모델이 선택될 수 있기에, 우리는 추가적으로 Cross-Validation set (=Dev set)을 준비해야한다.

  - 따라서 다음과 같은 과정으로 모델을 선택한다.

    1. 데이터셋을 Training set / Dev set / Test set으로 나눈다.

    2. Training set으로 모델의 학습파라미터들을 학습시킨다.

    3. Dev set에서 모델의 에러를 산정하고 가장 낮은 에러를 갖는 모델을 선택한다.

    4. Test set에서 모델의 에러를 산정하고 Dev set과 유사한 에러가 나오면 OK, 더 큰 에러가 나오면 Dev set에 오버피팅이 되었기 때문에 다시 모델을 선택한다. 

       ** 주의해야할 점은 Dev set과 Test set의 데이터분포는 동일해야한다는 것이다.

       

## Bias / Variance 문제 진단 - 어떻게 최적의 모델을 선정할 것인가

- 우리는 위와 같은 방법으로 모델을 선택할 수 있지만 모델을 선택하고 나서도 최적의 모델을 선택하기 위한 노력이 필요하다. 
- 머신러닝에서 최적의 모델은 다음과 같은 문제를 갖지 않는 것을 우선으로 한다.
  - Bias 문제 : 학습데이터에 과도하게 Underfit된 상황으로 Training set에러가 크고, Dev set에러도 역시 큰 경우이다.
  - Variance 문제 : 학습데이터에 과도하게 Overfit된 상황으로 Training set 에러가 작고, Dev set에러는 큰 경우이다.

![image-20220121054812761](../Blog/wjsakfh.github.io/images/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D%20%EC%97%94%EC%A7%80%EB%8B%88%EC%96%B4%EB%A7%81%20%EC%8B%A4%EC%A0%84%201%20-%20%EB%AA%A8%EB%8D%B8%20%EC%84%A0%EC%A0%95%EA%B3%BC%20Variance,%20Bias%20%EB%AC%B8%EC%A0%9C%ED%8C%8C%EC%95%85/image-20220121054812761.png)

[Coursera Machine Learning Lecture 10 p.16]

- Bias 문제와 Variance문제를 판별하는 방법은 다음과 같은 요소들로부터 에러의 추세를 보는 것이다. 
  - 모델의 복잡도 (예로 Degree of polynomial)
    - ![image-20220120061029750](../Blog/wjsakfh.github.io/images/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D%20%EC%97%94%EC%A7%80%EB%8B%88%EC%96%B4%EB%A7%81%20%EC%8B%A4%EC%A0%84%201%20-%20%EB%AA%A8%EB%8D%B8%20%EC%84%A0%EC%A0%95%EA%B3%BC%20Variance,%20Bias%20%EB%AC%B8%EC%A0%9C%ED%8C%8C%EC%95%85/image-20220120061029750.png)
    - [Coursera Machine Learning Lecture 10 p.17]

  - 모델의 하이퍼파라미터 (예로 Regularization \lambda)
    - ![image-20220120060957750](../Blog/wjsakfh.github.io/images/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D%20%EC%97%94%EC%A7%80%EB%8B%88%EC%96%B4%EB%A7%81%20%EC%8B%A4%EC%A0%84%201%20-%20%EB%AA%A8%EB%8D%B8%20%EC%84%A0%EC%A0%95%EA%B3%BC%20Variance,%20Bias%20%EB%AC%B8%EC%A0%9C%ED%8C%8C%EC%95%85/image-20220120060957750.png)
    - [Coursera Machine Learning Lecture 10 p.23]
  - Training set의 사이즈에 따라 모델 문제 파악 (=Learning Curves)
    - ![image-20220120062624625](../Blog/wjsakfh.github.io/images/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D%20%EC%97%94%EC%A7%80%EB%8B%88%EC%96%B4%EB%A7%81%20%EC%8B%A4%EC%A0%84%201%20-%20%EB%AA%A8%EB%8D%B8%20%EC%84%A0%EC%A0%95%EA%B3%BC%20Variance,%20Bias%20%EB%AC%B8%EC%A0%9C%ED%8C%8C%EC%95%85/image-20220120062624625.png)
    - [Coursera Machine Learning Lecture 10 p.26]
    - ![image-20220120062724424](../Blog/wjsakfh.github.io/images/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D%20%EC%97%94%EC%A7%80%EB%8B%88%EC%96%B4%EB%A7%81%20%EC%8B%A4%EC%A0%84%201%20-%20%EB%AA%A8%EB%8D%B8%20%EC%84%A0%EC%A0%95%EA%B3%BC%20Variance,%20Bias%20%EB%AC%B8%EC%A0%9C%ED%8C%8C%EC%95%85/image-20220120062724424.png)
    - [Coursera Machine Learning Lecture 10 p.27]



- Bias문제와 Variance문제 해결 방안은 다음과 같다.
  - High Bias
    - Feature를 추가한다.
    - Lambda를 줄인다.
  - High Variance
    - 학습셋을 더 모은다
    - Feature의 수를 줄인다.
    - Lambda를 늘린다.

- 결론적으로 머신러닝 엔지니어링을 하기 위한 가장 첫번째 단계는 데이터셋의 분할을 세가지(Training set/Dev set/Test set)로 나눈다. 두번째는 모델을 평가할 지표를 선정한다. 세번쨰는 모델을 평가하고 선정한다. 네번쨰는 모델의 문제를 진단한다. 다섯번째는 해결방안을 모색하고 적용한다.
- 추후에는 데이터셋을 일반적으로 어떤 비율로 분할하고 데이터분포가 다른 경우는 어떻게 분할할 것인지 알아보고, 모델을 평가할 지표에 대해서도 자세히 알아본다. 또 모델의 문제를 진단하기 위한 방법론인 Error Analysis에 대해서도 알아본다.