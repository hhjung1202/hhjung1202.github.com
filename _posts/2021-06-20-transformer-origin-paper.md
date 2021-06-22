---
title: "Paper : Attention is all you need 논문 리뷰"
categories:
  - Transformer
tags:
  - Transformer
  - NLP
  - Vision
  - NIPS 2017
---

###### 2017년에 발표한 Attention is all you need 논문 리뷰를 시작하겠습니다. <br/> 해당 포스트에서는 Transformer을 Vision에서 어떻게 사용되는지를 분석하기 위함이므로 Self Attention과 Multi-Head Attention의 이해를 중심으로 설명하겠습니다.

###### Translator을 구현하기 위해서는 학습 모델이 입력으로 들어온 문장 Sequence에 대해서 이해하는 능력이 필요합니다. <br/> 이전의 RNN 기반의 모델에서도 Long-Term Dependency와 Short-Term Dependency를 고려해 왔자만 직접적으로 단어 간의 연관성을 표현하지 않기 때문에 단어간의 연관성을 직접적으로 시각화하기 어려웠습니다. <br/> 또한 Encoder-Decoder 구조에서 정보가 압축되면서 단어간의 연관 정보가 일부 손실되는 문제가 있었습니다. <br/> 본 논문에서는 Self Attention을 활용하여 문장 내의 단어끼리의 연관성을 직접적으로 나타내는 Transformer을 제안하고 있습니다.


![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/transformer/origin/n1.jpg){: .align-center}

###### 위의 그림은 논문에서 제시한 Transformer 모델 구조입니다. 이를 자세히 살펴보겠습니다.


![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/transformer/origin/n2.jpg){: .align-center}

###### Multi Head Attention을 설명하기 앞서 Self Attention에 대해서 설명하겠습니다. Self Attention은 입력으로 들어온 문장 내에서 단어간의 연관성을 Attention을 활용하여 측정하고 적용하는 것이라고 할 수 있습니다. 예를들어 위의 그림처럼 I am a student 라는 문장이 있을 때, I 라는 단어와 자기 자신을 포함한 나머지 단어들과의 연관성을 계산하고 Softmax로 확률 값으로 만든 후 이를 다시 입력 값에 적용하게 됩니다.


![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/transformer/origin/n3.jpg){: .align-center}

###### Self Attention의 구체적 계산 방식은 다음과 같습니다.
* 먼저 입력으로 들어온 단어들을 Feature Embedding 시켜서 위의 그림의 X처럼 만듭니다.
* X에 각기 다른 Weight Matrix를 곱하여 Q, K, V를 만듭니다.
* 구해진 Q, K, V 를 아래의 수식에 적용하여 노란색 Output을 만들어냅니다.

###### 여기에서 Q(Querys), K(Keys), V(Vectors) 각각의 의미를 설명하겠습니다. <br/> 먼저 Querys 는 비교 주체이고 Keys 는 비교 대상이 됩니다. <br/> 예를 들어 Query가 "I" 일 때, Keys는 ["I","am","a","student"] 가 되어 Dot Product를 통해 연관 정보를 추출합니다. <br/> 연관 정보를 정규화 시키고 Softmax를 진행하여 확률 값을 만들고,<br/> 모델의 Feature에 해당하는 Vector에 이를 곱하여 Attention 정보를 적용하게 됩니다.


![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/transformer/origin/n4.jpg){: .align-center}

###### Multi-Head Attention의 경우, Self Attention을 위한 Matrix Weight을 h개(위의 그림에서는 h=8)로 하여 각기 다른 $$Z_i$$를 만들고 Concat한 후 다시 $$W_0$$를 곱하여 Output $$Z$$를 만들게 됩니다. <br/> 하나의 Self Attention을 사용할 경우 다양한 연관성을 고려하지 못할 것을 대비한 것으로 보입니다.


###### 이후에 Residual을 더하고 Layer Normalization을 수행한후 각각의 단어를 FC Layer을 통과하여 다음 Layer에 전달하게 됩니다.

###### 이상으로 Attention is all you need 논문 리뷰를 마치도록 하겠습니다.