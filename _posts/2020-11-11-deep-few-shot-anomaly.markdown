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
  <img src="/assets/images/posts/1_2ybgBHythwQXdSPrF2_caw" alt="Sample data"/>
</p>




