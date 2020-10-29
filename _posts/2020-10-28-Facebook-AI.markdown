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


## 영어를 매개로 하지 않고 100개 언어를 직접 번역하는 AI 모델

![image](https://about.fb.com/wp-content/uploads/2024/10/NRP-Machine_Translation_Milestone_banner.jpg?w=1920)

- Facebook AI가 영어 데이터에 의존하지 않고 100 개 언어 쌍을 번역 할 수 있는 최초의 다국어 기계 번역 (MMT) 모델 인 M2M-100을 소개했습니다. [여기](https://github.com/pytorch/fairseq/tree/master/examples/m2m_100)에서 오픈 소스 코드를 확인할 수 있습니다.

- 예를 들어 중국어를 프랑스어로 번역 할 때 대부분의 영어 중심의 다국어 모델은 영어 학습 데이터가 가장 널리 사용 가능하기 때문에 중국어에서 영어로, 영어에서 프랑스어로 학습합니다. Facebook AI 모델은 의미를 더 잘 보존하기 위해 중국어에서 프랑스어 데이터로 직접 학습합니다. 기계 번역을 평가하는 데 널리 사용되는 BLEU 측정 항목에서 영어 중심 시스템보다 10 점 더 우수한 성능을 보입니다.

- M2M-100은 총 2,200 개의 언어 방향으로 교육을 받았으며, 이는 이전 최고의 영어 중심의 다국어 모델보다 10 배 더 많은 것입니다. M2M-100을 배포하면 수십억 명의 사람들, 특히 리소스가 부족한 언어를 사용하는 사람들의 번역 품질이 향상됩니다.

- 아래 내용은 100 개 언어에 대한 보다 다양한 MMT 학습 데이터 세트 및 모델을 구축 한 방법에 대한 세부 정보를 설명입니다. 또한 다른 연구자들이 다국어 모델을 재현하고 발전시킬 수 있도록 모델, [교육 및 평가 설정](https://github.com/pytorch/fairseq/tree/master/examples/)을 출시합니다.

최근 Facebook은 적은 자원을 사용하는 기계 번역을 개발한 덕분에 뉴스 피드에서 매일 평균 200 억 건의 번역을 지원하고 있습니다.

일반적인 MT 시스템은 각 언어 및 각 작업에 대해 별도의 AI 모델을 구축하는 방법을 채용하고 있으며,이러한 접근 방식은 사람들이 수십억 개의 게시물에 160 개 이상의 언어로 콘텐츠를 게시하는 Facebook에는 효과적으로  못한 방법입니다. 고급 다국어 시스템은 한 번에 여러 언어를 처리 할 수 있지만, 영어 데이터에 의존하여 출발어와 도착어 간의 오류를 최소화 하는 방법으로 정확성이 떨어집니다. 커뮤니티에 더 나은 서비스를 제공하기 위해 모든 언어를 번역 할 수있는 하나의 다국어 기계 번역 (MMT) 모델이 필요합니다. 그 중 거의 3 분의 2는 영어 이외의 언어를 사용합니다.

Facebook에서 수년간의 MT 연구의 정점에서, 영어 중심 데이터에만 의존하지 않고 모든 방향으로 100x100 언어를 직접 번역 할 수있는 최초의 단일 대규모 MMT 모델을 발표하게되어 기쁩니다. 우리의 단일 다국어 모델은 기존의 이중 언어 모델만큼의 성능을 발휘하며 영어 중심의 다국어 모델에 비해 10 BLEU 포인트의 성능 향상을 달성했습니다.


INFO: <a href="https://about.fb.com/news/2020/10/first-multilingual-machine-translation-model/" target="_blank">https://about.fb.com/news/2020/10/first-multilingual-machine-translation-model/</a>)



