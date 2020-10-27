---
title: "Topological Data Analysis (토폴로지 데이터 분석 방법)"
layout: post
date: 2016-02-24 22:44
# tag:
# - markdown
# - elements
blog: true
author: Sunghyon Kyeong
summary: "Topological Data Analysis (토폴로지 데이터 분석 방법) "
permalink: topological-data-analysis-concept

---
토폴로지 데이터 분석은 다양한 분야에서 거대하고 복잡한 데이터로부터 의미있는 정보를 추출하는데 활용된 사례가 많이 있다. 많은 연구자들이 토폴로지 데이터 분석이 어떻게 작동하는지 원리를 알지 못한체 사용하는 사례가 많이 있기 때문에, 이번 포스팅에서는 토폴로지 분석이 왜 데이터 분석에서 효과적인 방법론인지에 대해 설명하고자 한다.

토폴로지 데이터 분석을 둘러싼 한가지 중요한 메세지는 데이터는 모양Shape을 갖고 있고, 그 모양이 우리에게 새로운 통찰을 줄 수 있다는 것이다. 분석을 통해서 완전히 새로운 메세지가 나타났다고 해도, 사실은 우리가 잘 알고 있는 것을 설명하는 것인 경우가 종종 있다.



<img src="https://github.com/skyeong/skyeong.github.io/blob/master/assets/images/posts/TDA/tda_step1.png">

토폴로지 데이터 분석에 대한 방법을 이야기 하기 전에 몇가지 서로 다른 형태의 데이터 분포에 대해서 이야기 하고자 한다. 위에 제시된 그림 중 제일 왼쪽에 보여지는 데이터는 직선 모양으로 대표될 수 있다. 이러한 데이터는 보통 선형회귀 분석을 통해서 데이터의 기울기를 찾을 수 있다. Fitting을 통해서 1차방정식의 계수를 구한다면, 데이터에 대해서 충분히 이해했다고 할 수 있을것이다. 두번째로 보여지는 데이터는 세개의 덩어리로 나뉘어진 데이터이다. 이러한 데이터는 1차 선형 방적식으로 설명할수는 없고, 최소 3개의 선형 방정식이 있어야 세개의 덩어리를 구분할 수 있을것이다. 두번째 예제에서는 데이터가 세군데의 서로 다른 곳을 중심으로 클러스터를 이루고 있기 때문에 평면에서 세개의 point cloud가 하나의 직선으로 대표될 수 없음을 쉽게 알 수 있다. 이러한 데이터를 보는 순간 사람들을 모양이 없는 데이터로군! 이라고 생각할 수도 있겠지만, 곧이어 '아! 이 데이터는 세개의 클러스터로 나눌 수 있겠군.' 이라고 생각할 것이다.  

<img src="https://github.com/skyeong/skyeong.github.io/blob/master/assets/images/posts/TDA/tda_step2.png">

세번째로 원형 모양의 데이터 분포를 생각해 보자. 이 데이터는 가운데 구멍이 뚤려 있는 원형 방정식으로 표현하면 가장 적절할 것이다. 직선 방정식으로 원형 모양의 데이터를 설명하고 싶은 사람은 없을 테니까. 마지막으로 데이터가 Y-모양 처럼 생겼다고 가정하면, 어떻게 할것인가? 이러한 데이터는 직선 방정식으로 표현할 수도 없고, 여러개의 덩어리 형태로 표현하기도 어려울 것이다. 그럼 어떻게 Y-모양 데이터를 설명할 수 있을까? 또는 하나의 방법으로 다양한 형태의 모양을 가진 데이터를 표현할 수 있는 방법은 없을까? 토폴로지 데이터 분석 기법에서 그 해답을 찾을 수 있을 것이다.

토폴로지 데이터 분석은 2007년에 스탠포트 대학교의 계산공학을 전공하는 Gurgeet Singh 박사과정 학생과 위상수학을 전공하는 Gunnar Carlsson 교수에 의해서 방법론이 세상에 처음 소개 되었다 (논문: <a href="http://www.ayasdi.com/wp-content/uploads/2015/02/Topological_Methods_for_the_Analysis_of_High_Dimensional_Data_Sets_and_3D_Object_Recognition.pdf" target="_blank">Topological Methods for the Analysis of High Dimensional Data Sets and 3D Object Recognition</a>). 이후 2011년도에는 스탠포드대학의 Monica Nicolau와 Gunnar Carlsson 교수는 토폴로지 데이터 분석 기법을 이용하여 유방암 환자의 Microarray 데이터를 분석했고, 유방암의 subgroups을 찾아내는데 성공했다 (논문: <a href="http://www.pnas.org/content/108/17/7265.abstract" target="_blank">Topology based data analysis identifies a subgroup of breast cancers with a unique mutational profile and excellent survival</a>).

논문이 소개된 년도를 보면 알겠지만, 수학의 토폴로지가 데이터 분석에 활용되기 시작한것이 2010년 쯔음이고, 데이터로부터 가치를 창출하는 것은 학계와 기업에 많은 관심과 수요가 예상되는 부분이다. 토폴로지 데이터 분석은 기계학습 방법론 측면에서 보면 비지도 기계학습 (unsupervised machine learning)에 해당되고, 보다 구체적으로는 "Partial Clustering"이라고 하는게 더욱 정확할 것이다.



<img src="https://github.com/skyeong/skyeong.github.io/blob/master/assets/images/posts/TDA/tda_step3.png">

토폴로지 데이터 분석은 크게 네 단계로 나눌 수 있다. 첫번째는 필터 함수를 구성하는 것이다. 필터 함수의 역할은 고차원의 데이터의 모양을 가장 잘 표현할 수 있도록 데이터를 Projection하기 위함이라고 할 수 있다. 위의 예제 그림에서는 Y축의 좌표값을 return하도록 필터 함수를 구성하면, Y-모양의 데이터 분포의 토폴로지를 가장 잘 추출할 수 있을 것이다. 두번째는 거리 함수를 정의하는 것이다. 고차원의 데이터가 필터함수를 통해서 하나의 값으로 요약되고 나면, 필터 값을 기준으로 데이터를 구획화 하게 되고, 구획화된 데이터 값들 간의 거리를 계산하게 된다. 거리 함수를 정의하는 방법도 여러가지가 있겠지만, 가장 많이 사용되는 거리함수는 유클리디언 거리 함수 있다. 세번째로 클러스터링 방법이다. 필터값에 따라서 데이터를 구획화 하고, 구획화된 데이터 값들 간에 거리를 구하고 나면, 이후에는 데이터 값들간의 거리를 기준으로 클러스터링을 지행하게 된다. 해당 필터 구간내에 몇개의 데이터들이 서로서로 모여 있는지, 아니면 2~3개의 덩어리로 서로 뭉쳐 있는지 등이 클러스터링을 통해서 계산되게 된다. 마지막으로 데이터를 시각화가 필요하다. 데이터 포인트로부터 결과로 생성된 simplicial complex를 그래프의 형태로 표현하고 나면 위의 그림에서 (C)의 형태가 되는데, 그래프에서 각 노드Node는 Cluster이고, 선Edge는 클러스터간의 교집합이 존재함을 표현한다. 마지막으로 노드의 색은 관심있는 값을 표현하게 되는데, 위의 예제에서는 각 노드 내의 데이터 값이 같는 필터 값의 평균을 표현했다. 


토폴로지 데이터 분석은 다양한 분야의 데이터 분석에서 많이 활용되고 있고, 토폴로지 데이터 분석이 각광받고 있는 이유는 기존의 클러스터링 방법으로는 찾지 못하는 "데이터 내의 특이한 subgroups"을 잘 추출하는데 있다. P.Y. Lum은 미국 NBA 농구선수들의 분당 리바운드, 슈팅, 피스, 파울 등의 수치 값들을 이용해서 토폴로지 데이터 분석을 시행했더니, 기존에 잘 알려진 공격형, 수비형 선수를 구분해 냈을 뿐만이 아니라 All star players들도 하나의 subgroup으로 검출해 냈다. 이는 기존의 고전적 비지도학습 방법으로는 확인할 수 없덨던 결과이다 (논문: <a href="http://www.nature.com/articles/srep01236" target="_blank">Extracting insights from the shape of complex data using topology</a>).

마지막으로 토폴로지 데이터 분석이 뇌영상 데이터 분석에도 적용한 연구도 있다. S. Kyeong은 토폴로지 데이터 분석을 뇌영상 데이터 분석에 적용하여 정상군과 환자군을 구분해 내는데 성공했다. 연구 초기의 목표는 토폴로지 데이터 분석으로 주의력결핍/과잉행동 장애 환자의 아형을 구분해 내는 것 이었는데, 실제 데이터 분석에서는 아형을 구분해 내지는 못했다. 연구 결과는 PLoS One에 게제되었다 (논문: <a href="https://journals.plos.org/plosone/article/metrics?id=10.1371/journal.pone.0137296" target="_blank">A New Approach to Investigate the Association between Brain Functional Connectivity and Disease Characteristics of Attention-Deficit/Hyperactivity Disorder: Topological Neuroimaging Data Analysis</a>). 본 연구는 뇌영상 데이터를 분석하는데 토폴로지 데이터 분석 기법을 처음으로 제기 했다는데 큰 의미가 있다.
