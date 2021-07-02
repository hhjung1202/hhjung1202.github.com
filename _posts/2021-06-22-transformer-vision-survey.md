---
title: "Paper : Transformers in Vision: A Survey 논문 리뷰(1)"
categories:
  - Transformer
tags:
  - Transformer
  - Vision
  - Survey Paper
use_math: true
comments: true
---

###### 2021년에 발표한 Transformers in Vision: A Survey 리뷰 1편을 시작하겠습니다. 
###### 해당 포스트에서는 Transformer를 Vision에서 어떻게 적용해왔는지를 설명하고자 합니다.

먼저 소개할 내용은 Image Recognition을 위한 Transformers 에 대한 내용입니다.
- Non Local Neural Networks
- Criss Cross Attention
- Stand-Alone Self-Attention
- Local Relation Networks
- Attention Augmented Convolutional Networks
- Vectorized Self-Attention
- Vision Transformer
- Data-Efficient Image Transformers
- CLIP: Contrastive Language–Image Pre-training

* Non Local Neural Networks
논문의 제목은 "Non Local Neural Networks" 이며 CVPR 2018에 발표된 논문입니다. 

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/1-1.jpg){: .align-center}


![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/1-2.jpg){: .align-center}


기존의 Non Local Means 연산은 Bottom-up 연산을 진행하는 Image Denoising에서 사용하던 기법으로 이미지 내의 각 픽셀과 자신을 포함한 나머지 픽셀들과의 연관성(유사성)을 계산하고, 계산된 값을 토대로 weighted sum을 진행하여 spatial long-range dependency를 얻어냈습니다. 이에 영갑을 받아 논문에서 제시하는 Non Local Block은 spatial축 뿐만 아니라 temporal 축에도 이를 적횽하여 long-range dependency를 확보하였습니다. 3D 데이터인 Video에서는 여러 프레임에 걸쳐서 오브젝트의 움직임이 천천히 일어나기 때문에 temporal dependency를 극대화시킬 수 있었습니다.

* Criss Cross Attention
논문의 제목은 "CCNet: Criss-Cross Attention for Semantic Segmentation" 이며 ICCV 2019에 발표된 논문입니다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/2-1.jpg){: .align-center}

위의 그림에서 보듯이 Non Local Neural Networks 에서 사용된 Non local block 의 경우, 픽셀간의 연관성을 학습하기 위해서 자신을 포함한 모든 픽셀들과 비교하는 반면 Criss-Cross Attention block의 경우 픽셀의 가로축과 세로축의 연관성만을 고려하여 연산량을 $O(N^2)$ 에서 $O(2 \times sqrt(N))$ 으로 만듭니다. Non local block 에서처럼 full-image contextual information을 모델링 하기 위해서 Attention 2번 진행하여 전체 픽셀과의 연관성을 고려할 수 있게 하였습니다.

* Stand-Alone Self-Attention
논문의 제목은 "Stand-Alone Self-Attention in Vision Models" 이며 NIPS 2019에 발표된 논문입니다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/3-1.jpg){: .align-center}

CNN 연산을 기반으로 된 ResNet 모델에서 Convolutional Layer을 Local Self-Attention Layer로 바꾸어 모델을 경량화한 연구입니다.

* Local Relation Networks
논문의 제목은 "Local Relation Networks for Image Recognition" 이며 ICCV 2019에 발표된 논문입니다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/4-1.jpg){: .align-center}

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/4-2.jpg){: .align-center}

학습이 완료된 CNN의 경우 입력 이미지의 특성과 관계없이 고정된 Weight를 가지게 되는데, 이 논문에서는 Local Relation Layer을 제안하며 입력 이미지의 특징에 따라 Adaptive한 Weight Aggregation을 수행합니다. 아래의 Local Relation Layer을 자세히 살펴보면, 한 픽셀의 정보를 계산하기 위해 $7 \times 7$ 픽셀을 사용합니다. $1 \times 1$ CNN을 통과한 Query Map과 Key Map은 각각 비교 주체와 대상이 되어 연관성을 계산하고 Geometry 정보를 포함시킨 후 $Softmax$를 통해 Aggregation Weight을 계산하고 이를 Feature Map에 적용하는 과정을 통해 Weight Aggregation을 수행하게 됩니다.

* Attention Augmented Convolutional Networks

