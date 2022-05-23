# EMNIST_classify

you can download dataset here. (EMNIST handwrite dataset)
https://www.kaggle.com/datasets/crawford/emnist

And, you can download dataset (Next Word)
1. letters train
https://drive.google.com/file/d/1TvXANMn2LKcbI09MzWNgEhD7lv4IgvaS/view?usp=sharing
2. letters test
https://drive.google.com/file/d/17OlyrwbJBTfXf_yCK7DWUH7h9Y0-sxU8/view?usp=sharing
3. balanced train
https://drive.google.com/file/d/1xrq9av_rSsBOz3PGI6EH9cLORjytJfbk/view?usp=sharing
4. balanced test
https://drive.google.com/file/d/1PluDzPRd_OSPzu-SUfyxTJ3OqFK4VAjE/view?usp=sharing


- 데이터 분석
    - emnist-letters : A-Z 총 26개 class train 약 89,000 test 약 14,800
    - emnist-balnaced : 0-9, A-Z, 대문자와 비슷하지 않은 소문자 총 47개 class
    - encodedpdc : emnist-letters에 맞춰 LSTM으로 각 문자 class를 실제 output으로 가지는 예측 데이터를 만든 것
    - encodedbalancepdc : emnist-balanced에 맞춰 LSTM으로 각 문자 class를 실제 output으로 가지는 예측 데이터를 만든 것

- CNN

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4194e7d8-58d0-4e62-a648-142c363b7a3d/Untitled.png)

- VGG16

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/17ff25d9-5f82-4b29-9538-1d86f524c511/Untitled.png)

vgg16은 Imagenet challenge에서 탄생한 모델이라 input이미지 크기가 224x224x3이고 ouput class 수가 1000개로 고정 되어 있어서
emnist 데이터의 크기와 클래스 수에 맞게 끔 조정 해 주는 과정이 필요했습니다. 

(24*24를 48*48로 변환)

- RESNET

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/817874ef-5c48-474b-a6a8-61ca85e3f948/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5d9d4996-99df-4f79-b119-ae0a2ad126c9/Untitled.png)

- LSTM : dataset 만드는 데 사용

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/15c17329-4ec8-40ca-aeed-3933dffafef8/Untitled.png)

LSTM 학습 데이터로는 저작권이만료된 Gutenberg을 합쳐서 사용했고, accuracy는 57%로 낮게 나왔으나, 오답으로 측정된 데이터도 살펴봤을 때 정답 레이블을 포함한 여러 클래스의 확률이 높게 나와서 충분히 의미 있다고 판단했습니다.

- 이미지 처리 모델 + LSTM으로 예측한 데이터 처리

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/13a9fa5c-5c2b-4584-8ddb-4f8115f20e49/Untitled.png)

CNN, VGG16, RESNET 등의 이미지를 처리하는 모델의 출력과 사전에 LSTM으로 산출한 실제 레이블에 대한 score점수를 처리하는 모델의 출력을 연접한 후 softmax를 적용해서 classification했습니다. 중간에 activation함수는 relu를 사용했습니다.

- Letters에 대한 결과
- Balanced에 대한 결과

(추후 공개)
