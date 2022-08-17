# Style Transfer 논문정리

* paper:[Style Transfer](https://ieeexplore.ieee.org/document/7780634)
<p align="left">
    <img src="images/1.PNG">
</p>

# 01. Pre-trained Model
- MNIST(0~9를 나타내는 흑백 이미지)를 높은 정확도로 인식하기 위해서는 최소 3개의 Convolution layer와 1개의 fully connected layer가 필요하며 이때 전체 학습에 소요되는 시간은 1개의 CPU 환경에서 약 1시간 10분 소요

<p align="center">
    <img src="images/2.PNG">
</p>
<p align="center">
    <img src="images/3.PNG">
</p>
<p align="center">
    <img src="images/4.PNG">
</p>
<p align="center">
    <img src="images/5.PNG">
</p>
<p align="center">
    <img src="images/6.PNG">
</p>
<p align="center">
    <img src="images/7.PNG">
</p>
<p align="center">
    <img src="images/8.PNG">
</p>

# 08. Style Transfer
- 스타일 전송을 위해서 사전 학습된(Pre-trained) CNN 모델을 사용합니다. (특징 추출 모델로 VGG19를 사용했습니다.)
- 네트워크의 가중치를 고정시키고 이미지를 변경시키는 방법을 사용합니다.
- 아래 사진과 같이 이미지를 업데이트하여 원하는 정보를 입힙니다.

<p align="center">
    <img src="images/9.PNG">
</p>

- 이미지 스타일 트랜스퍼를 조금 더 수식적으로 표현하기 위해서 논문의 수식을 살펴보면, 각각의 이미지를 이헐게 벡터로 표현한 이유는 사실 한 장의 이미지는 이런식으로 세로축과 가로축으로 구성된 한 장의 행렬과 같은 데이터라고 볼 수 있지만 이런 이미지 또한 그냥 왼쪽 위부터 쭉 일렬로 나열하는 방식으로 하나의 벡터로써 표현할 수 있기 때문에 하나의 미이지를 표현할 때 벡터 형태의 변수로써 표현하게 됩니다.

<p align="center">
    <img src="images/10.PNG">
</p>

- 일반적으로 CNN에서 layer가 깊어질수록 채널의 수가 많아지고 너비와 높이는 줄어들며 convolution layer의 서로 다른 필터들은 각각 적절한 특징(feature)값을 추출하도록 학습합니다.

<p align="center">
    <img src="images/11.PNG">
</p>
<p align="center">
    <img src="images/12.PNG">
</p>

# 12. Style Loss
- 스타일(Style)은 서로 다른 특징(feature) 간의 상관관계(correlation)을 의미합니다.
- Gij = 특징 i와 특징 j의 상관관계(correlation)
- 논문에서는 스타일은 서로 다른 특징들간의 상관관계로 정의합니다. 두 이미지의 스타일이 같다라는 말은 "두 이미지에 존재하는 특징들의 상관관계 정도가 유사하다." 라고 말할 수 있겠습니다.
- 상관관계를 수치적으로 표현하기 위해서 Gram Matrix를 사용합니다.

- 스타일 손실(Style loss)은 두 이미지의 특징 상관관계를 유사하게 만들어줍니다.
- 일반적으로 3~4개 정도의 레이어에서 Gram Matrix를 구해 유사해지도록 진행이 됩니다.
- 각 레이어 손실값에 가중치를 줄 수 있는 하이퍼 파라미터가 존재합니다.

<p align="center">
    <img src="images/13.PNG">
</p>

- 최종적으로 이러한 gram matrix의 값 자체를 그 이미지의 style이라고 볼 수 있습니다.
- style loss라는 것은 이러한 gram matrix를 사용하는 것이고 두 이미지의 gram matrix의 값이 같도록 만들어서 두 이미지의 style 값이 유사할 수 있도록 만드는 방식으로 동작합니다.
- style loss를 구할 때 어떤 layer를 사용할지 미리 결정해놓은 그 값에 따라서 각각의 layer에 대해서 전부 다 El 값을 구한 뒤에 전부 다 손실값을 줄일 수 있는 형태로 update를 진행한다고 볼 수 있습니다. Wl의 경우는 어떤 레이어에 더 많은 가중치를 둘지 설정하기 위해서 넣어주는 hyperparameter입니다.

<p align="center">
    <img src="images/14.PNG">
</p>
<p align="center">
    <img src="images/15.PNG">
</p>
<p align="center">
    <img src="images/16.PNG">
</p>
<p align="center">
    <img src="images/17.PNG">
</p>
