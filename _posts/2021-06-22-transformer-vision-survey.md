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
   + Non Local Neural Networks
   + Criss Cross Attention
   + Stand-Alone Self-Attention
   + Local Relation Networks
   + Attention Augmented Convolutional Networks
   + Vectorized Self-Attention
   + Vision Transformer

<br/>
<h1><span style="color:green">1. Non Local Neural Networks</span></h1>


논문의 제목은 "Non Local Neural Networks" 이며 CVPR 2018에 발표된 논문입니다. 

<p align="center"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/1-1.jpg" width="400px"></p>

<p align="center"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/1-2.jpg" width="400px"></p>

기존의 Non Local Means 연산은 Bottom-up 연산을 진행하는 Image Denoising에서 사용하던 기법으로 이미지 내의 각 픽셀과 자신을 포함한 나머지 픽셀들과의 연관성(유사성)을 계산하고, 계산된 값을 토대로 weighted sum을 진행하여 spatial long-range dependency를 얻어냈습니다. 이에 영갑을 받아 논문에서 제시하는 Non Local Block은 spatial축 뿐만 아니라 temporal 축에도 이를 적횽하여 long-range dependency를 확보하였습니다. 3D 데이터인 Video에서는 여러 프레임에 걸쳐서 오브젝트의 움직임이 천천히 일어나기 때문에 temporal dependency를 극대화시킬 수 있었습니다.

<br/>
<h1><span style="color:green">2. Criss Cross Attention</span></h1>

논문의 제목은 "CCNet: Criss-Cross Attention for Semantic Segmentation" 이며 ICCV 2019에 발표된 논문입니다.

<p align="center"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/2-1.jpg" width="400px"></p>

위의 그림에서 보듯이 Non Local Neural Networks 에서 사용된 Non local block 의 경우, 픽셀간의 연관성을 학습하기 위해서 자신을 포함한 모든 픽셀들과 비교하는 반면 Criss-Cross Attention block의 경우 픽셀의 가로축과 세로축의 연관성만을 고려하여 연산량을 $O(N^2)$ 에서 $O(2 \times sqrt(N))$ 으로 만듭니다. Non local block 에서처럼 full-image contextual information을 모델링 하기 위해서 Attention 2번 진행하여 전체 픽셀과의 연관성을 고려할 수 있게 하였습니다.

<br/>
<h1><span style="color:green">3. Stand-Alone Self-Attention</span></h1>
논문의 제목은 "Stand-Alone Self-Attention in Vision Models" 이며 NIPS 2019에 발표된 논문입니다.

<p align="center"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/3-1.jpg" width="400px"></p>

CNN 연산을 기반으로 된 ResNet 모델에서 Convolutional Layer을 Local Self-Attention Layer로 바꾸어 모델을 경량화한 연구입니다.

<br/>
<h1><span style="color:green">4. Local Relation Networks</span></h1>
논문의 제목은 "Local Relation Networks for Image Recognition" 이며 ICCV 2019에 발표된 논문입니다.

<p align="center"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/4-1.jpg" width="400px"></p>

<p align="center"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/4-2.jpg" width="400px"></p>

학습이 완료된 CNN의 경우 입력 이미지의 특성과 관계없이 고정된 Weight를 가지게 되는데, 이 논문에서는 Local Relation Layer을 제안하며 입력 이미지의 특징에 따라 Adaptive한 Weight Aggregation을 수행합니다. 아래의 Local Relation Layer을 자세히 살펴보면, 한 픽셀의 정보를 계산하기 위해 $7 \times 7$ 픽셀을 사용합니다. $1 \times 1$ CNN을 통과한 Query Map과 Key Map은 각각 비교 주체와 대상이 되어 연관성을 계산하고 Geometry 정보를 포함시킨 후 $Softmax$를 통해 Aggregation Weight을 계산하고 이를 Feature Map에 적용하는 과정을 통해 Weight Aggregation을 수행하게 됩니다.

<br/>
<h1><span style="color:green">5. Attention Augmented Convolutional Networks</span></h1>
논문의 제목은 "Attention Augmented Convolutional Networks" 이며 ICCV 2019에 발표된 논문입니다.

<p align="center"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/5-1.jpg" width="600px"></p>

위의 논문은 Transformer 를 직접적으로 적용했다고 보기는 어렵지만 CNN의 translation equivariance (입력의 위치가 변하면 출력도 동일하게 위치가 변하는 성질)은 유지하면서 Self-Attention 메커니즘을 적용하기 위한 Relative Position Encoding 기반의 연산을 제안했습니다.

<br/>
<h1><span style="color:green">6. Vectorized Self-Attention</span></h1>
논문의 제목은 "Exploring Self-attention for Image Recognition" 이며 CVPR 2020에 발표된 논문입니다. 일반적으로 CNN이 수행하는 Feature Aggregation과 Transformation을 분리하여 Self Attention을 통한 Feature Aggregation과 Element-wise perceptrons을 활용한 Feature Transformation을 진행합니다.

<p align="center"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/6-1.jpg" width="400px"></p>

논문에서는 Feature Aggregation을 위한 Self Attention으로 Pairwise Self-Attention과 Patch-wise Self-Attention을 제안합니다. 그림의 연산 과정을 살펴보면 먼저 $1 \times 1$ CNN Layer(=Point wise Linear)을 통과하여 $\phi, \psi$ Relation 연산을 통해서 $\delta$를 만듭니다. 이 때 Relation은 $+, -, Concat$ 등으로 정의하였습니다. 만들어진 Relation과 $1 \times 1$ CNN Layer를 통과하여 만든 $\beta$에 Aggregation을 진행하여 spatial과 channel에 대한 weight를 학습하는 Vector Attention을 만들었습니다. 이렇게 구성한 Self-Attention Networks (SAN)을 통해 더 적은 수의 parameter로 ImageNet 데이터 셋에서 ResNet보다 우수한 성능을 거둘 수 있었다고 합니다.


<br/>
<h1><span style="color:green">7. Vision Transformer</span></h1>
논문의 제목은 "An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale" 이며 ICLR 2021에 발표된 논문입니다. 

<p align="center"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/transformer/survey1/7-1.jpg" width="400px"></p>


