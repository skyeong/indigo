---
title: "영어를 매개로 하지 않고 100개 언어를 직접 번역하는 AI 모델"
layout: post
date: 2020-10-28 22:08
blog: true
author: skyeong
categories: [AI, machine learning]
tags: [AI, machine learning]
summary: "영어를 매개로 하지 않고 100개 언어를 직접 번역하는 AI 모델"
---

![image](https://about.fb.com/wp-content/uploads/2024/10/NRP-Machine_Translation_Milestone_banner.jpg?w=1920)

- Facebook AI가 영어 데이터에 의존하지 않고 100 개 언어 쌍을 번역 할 수 있는 최초의 다국어 기계 번역 (MMT) 모델 인 M2M-100을 소개했습니다. [여기](https://github.com/pytorch/fairseq/tree/master/examples/m2m_100)에서 오픈 소스 코드를 확인할 수 있습니다.

- 예를 들어 중국어를 프랑스어로 번역 할 때 대부분의 영어 중심의 다국어 모델은 영어 학습 데이터가 가장 널리 사용 가능하기 때문에 중국어에서 영어로, 영어에서 프랑스어로 학습합니다. Facebook AI 모델은 의미를 더 잘 보존하기 위해 중국어에서 프랑스어 데이터로 직접 학습합니다. 기계 번역을 평가하는 데 널리 사용되는 BLEU 측정 항목에서 영어 중심 시스템보다 10 점 더 우수한 성능을 보입니다.

- M2M-100은 총 2,200 개의 언어 방향으로 교육을 받았으며, 이는 이전 최고의 영어 중심의 다국어 모델보다 10 배 더 많은 것입니다. M2M-100을 배포하면 수십억 명의 사람들, 특히 리소스가 부족한 언어를 사용하는 사람들의 번역 품질이 향상됩니다.

- 아래 내용은 100 개 언어에 대한 보다 다양한 MMT 학습 데이터 세트 및 모델을 구축 한 방법에 대한 세부 정보를 설명입니다. 또한 다른 연구자들이 다국어 모델을 재현하고 발전시킬 수 있도록 모델, [교육 및 평가 설정](https://github.com/pytorch/fairseq/tree/master/examples/)을 출시합니다.




[INFO](https://about.fb.com/news/2020/10/first-multilingual-machine-translation-model/)



