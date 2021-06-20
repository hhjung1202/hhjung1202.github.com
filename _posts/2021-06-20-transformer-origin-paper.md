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

2017년에 발표한 Attention is all you need 논문 리뷰를 시작하겠습니다. 
Translator을 구현하기 위해서는 학습 모델이 입력으로 들어온 문장 Sequence에 대해서 이해하는 능력이 필요합니다.
이전의 RNN 기반의 모델에서도 Long-Term Dependency와 Short-Term Dependency를 고려해 왔자만 직접적으로 
단어 간의 연관성을 표현하지 않기 때문에 단어간의 연관성을 직접적으로 시각화하기 어려웠습니다. 
Encoder-Decoder 구조에서 정보가 압축되면서 단어간의 연관 정보가 일부 손실되는 문제가 있었습니다.
본 논문에서는 Self Attention을 활용하여 문장 내의 단어끼리의 연관성을 직접적으로 나타내는 Transformer을 제안하고 있습니다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/transformer/origin/n1.jpg){: .align-center}

위의 그림은 논문에서 제시한 Transformer 모델 구조인데 이를 세분화하여 분석해보겠습니다.

