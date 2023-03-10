# 모두의 딥러닝
## 2023-02-07(화)
### 전이 학습
- [VGG16](https://medium.com/@msmapark2/vgg16-%EB%85%BC%EB%AC%B8-%EB%A6%AC%EB%B7%B0-very-deep-convolutional-networks-for-large-scale-image-recognition-6f748235242a)

### 설명 가능한 딥러닝 모델 만들기
- 그래디언트 CAM
- 오클루전

## 2023-02-03(금)
### 컨볼루션 신경망(CNN)
- [DNN CNN 개념 차이](https://ebbnflow.tistory.com/119)
- stride = 1, 1칸씩 움직인다는 뜻
- padding: 0(zero padding)을 cnn 시 연산에 넣는다 (padding=same) -> 이미지가 계속 줄어드는 것을 방지
- max pooling: cnn output의 max 값을 넘긴다
- input -> convolution -> max-pooling -> convolution -> max-pooling ..... -> flatten
- [drop out](https://hyewonleess.github.io/cnn/CNN_options/)

### 적대적 신경망(GAN)
- [적대적 신경망](https://www.spri.kr/posts/view/21883?code=industry_trend)
- [배치정규화](https://gaussian37.github.io/dl-concept-batchnorm/)

## 2023-02-02(목)
### K-fold 교차 검증
[K-fold 교차 검증](https://nonmeyet.tistory.com/entry/KFold-Cross-Validation%EA%B5%90%EC%B0%A8%EA%B2%80%EC%A6%9D-%EC%A0%95%EC%9D%98-%EB%B0%8F-%EC%84%A4%EB%AA%85)

### 딥러닝 모델
```
## 1. 모델 생성
model = keras.Sequential(name='sonar')
model.add(keras.layers.Dense(24, input_shape=(60, ), activation='relu'))
model.add(keras.layers.Dense(10, activation='relu'))
model.add(keras.layers.Dense(1, activation='sigmoid'))
model.summary()

## 2. 모델 컴파일 (loss, optimizer, metrics)
model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])

## 3. 모델 학습(fit)
model.fit(X,y, epochs=100, batch_size=20)

## 4. 모델 평가
print(f'loss:{model.evaluate(X, y)[0]}, accuracy:{model.evaluate(X, y)[1]}')

## 5. 모델 저장
model.save('sonar_model.hdf5')

## 6. 모델 로딩
model_imported = keras.models.load_model('./sonar_model.hdf5')

## 7. 로딩한 모델 사용방법
model_imported.evaluate(X_test, y_test)
```
### 모델 성능 검증
- 딥러닝의 경우 샘플 수가 많을수록 성능이 좋아짐
- 데이터에 따라서는 딥러닝이 아닌 랜덤 포레스트, XGBoost, SVM 등 다른 알고리즘이 더 좋은 성과를 보일 때도 있음(머신러닝)

### 모델 성능 향상
- 학습의 자동 중단
```
modelpath = './model/best_model.hdf5'

checkpoint = keras.callbacks.ModelCheckpoint(filepath=modelpath, monitor='val_loss', save_best_only=True, verbose=1)

earlystop = keras.callbacks.EarlyStopping(monitor='val_loss', patience=10) # 10정도 좋아지지 않으면 stop

history = model.fit(X,y,validation_split=0.3, epochs=2000, batch_size=500, callbacks=[checkpoint, earlystop])
```

## 2023-02-01(수)
### 다층 퍼셉트론
- XOR 문제의 해결

### 오차 역전파 계산
- [back propagation](https://evan-moon.github.io/2018/07/19/deep-learning-backpropagation/)
- [기울기 소실 문제(vanishing gradient)](https://heytech.tistory.com/388)
- 학습: 오차를 최소화하는 가중치를 찾는 과정.
- 확률적 경사 하강법: 랜덤하게 추출한 일부 데이터만 사용. 빠르고 더 자주 업데이트 할 수 있는 장점.
- 모멘텀: 오차를 수정하기 전 바로 앞 수정값과 방향을 참고해 같은 방향으로 일정한 비율만 수정되게 하는 방법.
- 옵티마이저(optimizers): 오차를 최소화하는 경사 하강법.

### 대표적인 오차 함수
- [예측 모델 평가를 위한 지표 정리](https://aliencoder.tistory.com/43)
- 선형회귀: 평균제곱오차(MSE), 평균절대오차(MAE), 평균절대백분율오차(MAPE), 평균제곱로그오차(MSLE)
- 다항분류: 범주형교차엔트로피(CC), 이항교차엔트로피(BC)

### 다중 분류 문제 해결

## 2023-01-31(화)
### Gradient descent(GD, 경사하강법)
- 반복적으로 기울기 a를 변화시켜서 m 값을 찾아내는 방법
- 학습률(learning rate)
- 오차의 변화에 따라 이차 함수 그래프를 만들고 적절한 학습률을 설정해 미분 값이 0인 지점 구하는 것

### 로지스틱 회귀 모델: 참 거짓 판단
- 시그모이드 함수: S자 형태로 그래프가 그려진 함수
- a 값은 기울기 , b 값은 위치를 결정함

### examples
- 최소제곱, 평균제곱오차(MSE), 선형 회귀, 다중 선형 회귀, 텐서플로, 로지스틱회귀

## 2023-01-27(금)
### 딥러닝 기초
[confusion matrix](https://diseny.tistory.com/entry/%ED%98%BC%EB%8F%99%ED%96%89%EB%A0%ACconfusion-matrix?category=906035)
- 딥러닝을 설계한다는 것은 결국 몇 개의 층을 어떻게 쌓을지, Dense 외에 어떤 층을 사용할지, 내부의 변수들을 어떻게 정해야 하는지 등에 대해 고민하는 것

### 딥러닝을 위한 기초 수학
1. 일차함수
- 기울기: x 값이 증가할 때 y 값이 어느 정도 증가하는지에 따라 그래프의 기울기 a가 정해짐
- 절편: 그래프가 축과 만나는 지점을 의미(b)

2. 이차함수
- 이차함수의 맨 아래에 위치한 지점이 최소값(minimum). 하나만 존재함.

3. 순간변화율과 미분함수
- 순간변화율: x의 증가량(Δx)이 0에 가까울 만큼 아주 작을 때의 순간적인 기울기를 의미
- 함수 f(x)를 x로 미분하라는 것은 x의 변화량이 0에 가까울 만큼 작을 때 y의 변화량을 x의 변화량으로 나누어 순간 기울기를 구하라는 뜻
- 도함수: f(x) = xn -> f'(x) = nx n-1 -> 미분한다는 소리임.
- f(x) = kx n k(상수), f'(x) = k nx n-1
- 곱의 미분, 나누기의 미분 알아두기
- 연쇄 미분(chain rule): backpropagation 관련 알아두기

4. 편미분: 변수가 두개일 때 하나를 상수 취급.
5. 지수와 지수함수
6. 로그 함수

### 가장 훌륭한 예측선
1. 최소제곱추정량: 제곱으로 구하는 이유? 미분하기 편해서
2. 최소제곱법
- 분자: x와 y의 편차를 곱해서 합한 값
- 분모: x의 편차(각 값과 평균과의 차이)를 제곱해서 합한 값
- 기울기가 나온다는 의미
3. [손실함수](https://heytech.tistory.com/361)
4. 평균 제곱 오차(MSE)

## 2023-01-26(목)
### 오리엔테이션
- 1, 2, 3 scalar
- [1,2] vetor
- [1,2
   3, 4] matrix

[행렬의 계산](https://j1w2k3.tistory.com/575)

- 오류역전파: 미분, 연쇄미분
[오류역전파 알고리즘](https://goofcode.github.io/back-propagation)