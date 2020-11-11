---
title: "Deep Few-Shot 이상탐지"
layout: post
date: 2020-11-11 21:00
# tag:
# - markdown
# - elements
blog: true
categories: [few-shot learning,anomaly detection, deep learning, data science]
tags: [few-shot learning, anomaly detection, deep learning, data science]
author: skyeong
summary: "Deep Few-Shot 이상탐지"
---

## 라벨이 정의된 몇 개의 anomaly 예제를 활용하는 이상탐지 수행

일반적으로 기존의 이상탐지 기법은 레이블 있는 anomaly 테이터가 부족하기 때문에 비지도 학습 (완전히 레이블이 지정되지 않은 데이터에 대해 학습 됨) 또는 반지도 학습 (배타적으로 레이블이 지정된 정상 데이터에 대해 학습 됨)을 이용했습니다. 결과적으로 실제 많은 이상탐지 애플리케이션은 레이블 정보가 있다 하더라도 이와 같은 사전 지식이 탐지 기술에 지렛대 역할을 하지 못합니다. 이렇게 제한된 labeled anomalies 정보는 배포 된 감지 시스템(예 : 성공적으로 감지 된 네트워크 침입 기록 몇 개)에서 비롯되거나 고객이보고하고 은행에서 확인한 소수의 사기성 신용 카드 거래와 같은 사용자로부터 발생할 수 있습니다. 매우 적은 수의 라벨링 된 이상 징후 만dl 훈련에 사용할 수 있다고 가정하므로이 연구 라인의 접근 방식은 'Few-Shot 이상탐지'라는 개념으로 접근할 수 있습니다. 하지만 일반적인 Few-Shot 학습과 몇 가지 근본적인 차이점이 있습니다. 글의 말미에 그 차이점에 대해 자세히 설명하겠습니다. 이 포스팅에서는 Few-Shot 이상탐지 문제를 해결하기 위한 딥 러닝 기술에 대해  공유해 드리겠습니다.

## 심층 거리-기반 이상탐지 기법
REPEN [1]은 아마도 몇 가지 라벨이 붙은 anomalies을 활용하여 이상탐지 모델을 학습하도록 설계된 최초의 심층 이상탐지 기법일 것입니다. REPEN의 핵심 아이디어는 이상 현상이 일반 데이터 인스턴스보다 무작위 데이터 서브 샘플에서 nearest neighbor 거리를 더 크게 갖도록하는 특성을 학습하는 것입니다. 이 임의의 nearest neighbor 거리는 [2, 3]에서 볼 수 있듯이 가장 효과적이고 효율적인 이상 현상 측정 방법 중 하나입니다. REPEN은이 최첨단 이상탐지에 맞게 조정 된 feature representation을 학습하는 것을 목표로합니다. REPEN의 프레임 워크는 다음과 같습니다.

<p align="center">
  <img src="/assets/images/posts/1_4K1teK6loh-Qlfbh0Iya8g.png" alt="Sample data"/>
</p>

REPEN은 임의 데이터 하위 집합 $x_i,…, x_{i + n-1}$에서 정상 인스턴스 $x+$보다 anomaly $x-$의 nearest neighbor 거리가 더 크도록 학습시킵니다. 학습의 목적함수는 다음과 같습니다.

<p align="center">
  <img src="/assets/images/posts/1_EbWQ0Kxt4qOGFpyvdypvvg.png" alt="Sample data"/>
</p>


여기서 $Q$는 unlabeled/normal 훈련 데이터에서 샘플링 된 랜덤 데이터 하위 집합이고, $f$는 신경망 학습 함수이며, $nn\_dist$는 데이터 하위 집합 $Q$에서 $x$의 가장 가까운 이웃 거리를 반환합니다.

위에서 볼 수 있듯이 REPEN은 큰 훈련 데이터에 정상 데이터만 있거나 모든 데이터의 레이블이 지정되지 않은 경우에만 작동합니다. 후자의 경우 라벨이 붙은 anomaly 데이터가 없는 경우 REPEN은 기존 이상 탐지기를 사용하여 pseudo-labeled anomaly 데이터를 생성합니다. 따라서 REPEN은 온전한 비지도학습 환경에서도 작동 할 수 있습니다.

레이블이 지정된 anomaly 데이터는 매우 제한적이지만 REPEN은 비지도학습 버전과 비교할 때 매우 뛰어난 정확도를 달성 할 수 있습니다. AUC 성능은 labeled anomalies의 항목 수가 1에서 80으로 증가함에 따라 빠르게 증가합니다.


<p align="center">
  <img src="/assets/images/posts/1_2ybgBHythwQXdSPrF2_caw.png" alt="Sample data"/>
</p>


REPEN의 소스 코드는 아래에서 확인 가능합니다.
[https://github.com/GuansongPang/deep-outlier-detection](https://github.com/GuansongPang/deep-outlier-detection)

## Deep Deviation Network : End-to-End 이상 탐지 최적화 접근 방식

거리 기반 이상 측정에 기반한 REPEN과 달리 편차 네트워크(DevNet [4])는 한정된 정보의 anomaly 데이터를 활용하여 end-to-end 이상 점수를 학습하도록 설계되었습니다. 주요 차이점은 아래 그림에서 확인할 수 있습니다. 전자는 feature representation을 최적화하고 후자는 이상 점수를 최적화합니다.

<p align="center">
  <img src="/assets/images/posts/1_v3cU6HSlbDqQVMD5lNh0ug.png" alt="Representation learning-focused approach vs. end-to-end anomaly detection approach"/>
</p>


구체적으로, 아래 프레임 워크에 표시된대로 학습 데이터 인스턴스 세트가 주어지면 DevNet은 먼저 신경 이상 점수 학습자를 사용하여 이상 점수를 할당 한 후에, 다음을 기반으로 일부 일반 데이터 인스턴스의 이상 점수 평균을 정의합니다. 후속 변칙 점수 학습을 안내하기 위한 참조 점수 역할을 할 사전 확률. 마지막으로, DevNet은 편차 손실이라고하는 손실 함수를 정의하여 상단 꼬리에 있는 정상 데이터 개체의 이상 항목 점수와 통계적으로 유의 한 편차를 적용합니다. DevNet 구현에서 Gaussian prior는 Z-Score 기반 편차 손실을 사용하여 이상 점수를 직접 최적화 하는데 사용됩니다.

<p align="center">
  <img src="/assets/images/posts/1_uyk6byvUPgGFrsJWW1cl2g.png" alt=""/>
</p> 


DevNet의 손실 함수는 다음과 같습니다.
<p align="center">
  <img src="/assets/images/posts/1_-HP47f24ca8_4rUXfn2new.png" alt=""/>
</p> 

여기서 dev는 Z-Score 기반 편차 함수이며 다음과 같이 정의됩니다.
<p align="center">
  <img src="/assets/images/posts/1_oU2d191kPiNoUwHRb3zp4g.png" alt=""/>
</p> 

여기서 $\phi$는 입력 $x$를 스칼라 출력으로 투영하는 신경망 기반 매핑 함수이며 $\mu$ 및 $\sigma$는 Gaussian prior에서 가져옵니다. 이러한 손실은 DevNet이 정상 인스턴스의 이상 점수를 가능한 $\mu$에 가깝게 하면서 $\mu$와 anomalies의 anomaly scores 사이에 최소 a의 편차를 적용하게 합니다.

DevNet을 다양한 실제 데이터 세트를 통해서 평가해본 결과는 다음과 같습니다. DevNet은 REPEN, deep one-class classifier, few-shot classifier 및 unsupervised method iForest를 포함한 여러 최첨단 경쟁 방법에 비해 향상된 성능을 보여줍니다. 더욱 자세한 실험 결과는 [4]에서 찾을 수 있습니다.

<p align="center">
  <img src="/assets/images/posts/1_-1_oG7DOCB5mcIAy_ukFtiPag.png" alt=""/>
</p>

DevNet의 소스 코드는 아래에서 확인 가능합니다.
[https://github.com/GuansongPang/deviation-network](https://github.com/GuansongPang/deviation-network)


## Few-shot 이상탐지 vs. Few-shot 분류

Few-shot 이상탐지에서 극히 적은 labeled anomaly 데이터는 서로 다른 형태의 anomaly를 나타낼 수 있으므로 완전히 다른 manifold/class 특성을 보일 수 있습니다. 이것은 제한된 예시가 클래스에 따라 다르며 동일한 manifold/class 구조를 공유한다고 가정하는 일반적인 Few-shot(주로 분류 작업)과 근본적으로 다릅니다. 따라서 Few-shot 이상탐지에서 일부 새로운 유형의 이상 클래스에서 발생하는 알려지지 않은 이상을 처리하려면주의를 기울여야합니다. 이 문제를 해결하기 위해 두 가지 방법[5, 6,7]에 대한 연구결과가 있습니다.

## References
1.  Pang, G., Cao, L., Chen, L., & Liu, H. (2018, July). Learning representations of ultrahigh-dimensional data for random distance-based outlier detection. In Proceedings of the 24th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining (pp. 2041–2050).
2.  Pang, G., Ting, K. M., & Albrecht, D. (2015, November). LeSiNN: Detecting anomalies by identifying least similar nearest neighbours. In 2015 IEEE international conference on data mining workshop (ICDMW) (pp. 623–630). IEEE.
3.  Sugiyama, M., & Borgwardt, K. (2013). Rapid distance-based outlier detection via sampling. In Advances in Neural Information Processing Systems (pp. 467–475).
4.  Pang, G., Shen, C., & van den Hengel, A. (2019, July). Deep anomaly detection with deviation networks. In Proceedings of the 25th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining (pp. 353–362).
5. Pang, G., Shen, C., Jin, H., & Hengel, A. V. D. (2019). Deep Weakly-supervised Anomaly Detection. arXiv preprint:1910.13601.
6. Pang, G., Hengel, A. V. D., Shen, C., & Cao, L. (2020). Deep Reinforcement Learning for Unknown Anomaly Detection. arXiv preprint:2009.06847.
7. Pang, G., Shen, C., Cao, L., & Hengel, A. V. D. (2020). Deep learning for anomaly detection: A review. arXiv preprint:2007.02500.

**원문 보기**:\>> [click](https://towardsdatascience.com/deep-few-shot-anomaly-detection-b33f130d1f80)

