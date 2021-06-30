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

