# Normalization-Standardization-Regularization-20190726-
Machine Learning에서의 Normalization(정규화), Standardization(표준화), Regularization(일반화)의 목적과 특징 공부.

# A. 목적
Normalization(정규화), Standardization(표준화), Regularization(일반화)의
공통점은 'Overfitting(과적합)'을 방지하기 위함이다.

# B. 차이점
목적은 같으나 각 개념에는 약간의 차이가 존재한다.

# B.1. Normalization(정규화), Standardization(표준화)
 Normalization과 Standardization은 데이터를 좀 더 compact하게 만들기 위해 사용한다.
즉, 값의 범위(scale)를 축소하는 re-scaling 과정을 의미한다. 왜 이렇게 해야할까?

 먼저, scale의 범위가 너무 크면 노이즈 데이터가 생성되거나 overfitting 가능성이 높아진다.
※ 제곱 손실 함수와 절댓값 손실 함수의 특성을 비교해보면 그 이유를 짐작할 수 있다.
제곱 손실 함수를 사용할 때에는 값이 비정상적으로 커져 노이즈 데이터가 많이 생성될 수 있다.
때문에 노이즈 데이터가 너무 많이 생성될 것 같으면 절댓값 손실 함수를 사용한다.
 또, 활성화 함수(activation function)를 거치는 의미가 사라진다.
값이 너무 커지게 되므로 활성화 함수를 거친다고 해도 한쪽으로 값이 쏠릴 가능성이 높아지기 때문이다.
 마지막으로, weight 초기화 방법으로 정규분포(N(0,1))로부터 값을 생성하는 방법을 자주 사용하는데,
정규분포의 값은 ±2.58내에 99%가 존재한다. 따라서, scale이 너무 커서 값의 분포 범위가 넓으면 값을 정하기 힘들어진다.
 여기서 Normalization과 Standardiztion의 scale 조절 방식에 차이가 존재한다.

※ Normalization의 scale 조절 방식
 다양한 방식이 존재하나, 한 예를 들자면 이미지의 픽셀 값 범위(0 - 255)를
255로 나눠 0 - 1의 범위로 축소시키는 방식이 있다

※ Standardization의 scale 조절 방식
 표준화 확률 변수를 구하는 방법. Z-Score 구하기 라고 할 수도 있다.

# B.2. Regularization(일반화)
 Regularization은 말 그대로 '제약'을 거는 작업이다.
여기서 제약을 건다는 것은 모델을 좀 더 complex 혹은 flexible하게 만든다는 것이다.
 Overfitting은 모델이 train data에 너무 딱 맞게 학습이 돼서 발생하는 문제인데,
여기서 특정 penalty 값만 더해주거나 빼주어서 특정 가중치가 너무 과도하게 커지지 않도록 
모델의 복잡도를 조정해주어도 train data에 딱 맞게 돼버리는 상황을 어느 정도 예방할 수 있다.
모델 복잡도에 대한 panalty로 overfitting을 예방하고 Generalization(일반화) 성능을
높이는데 도움을 준다.
 가중치 w가 작아지도록 학습한다는 것은 결국 Local noise에 영향을 덜 받도록 하겠다는 것이며,
이는 Outlier(이상치)의 영향을 더 적게 받도록 하겠다는 것이다.
 주로 Hyper Parameter를 수정하는 방식으로 Regularization을 수행한다.
Regularization 방법으로는 L1 Regularization, L2 Regularization, Dropout, Early stopping 등이 있다.

# B.2.1. L1 Regularization
 L1 Regularization은 cost function에 가중치의 절댓값을 더해주는 것으로
기존의 cost function에 가중치의 크기가 포함되면서 가중치가 너무 크지 않은 방향으로 학습되도록 한다.
이때 learning rate(학습률)이 0에 가까울 수록 정규화의 효과는 없어진다.

# B.2.2. L2 Regularization
 기존의 cost function에 가중치의 제곱을 포함하여 더함으로써 L1 Regularization과
마찬가지로 가중치가 너무 크지 않은 방향으로 학습되게 된다. 이를 Weight decay라고도 한다.

# 추가
● 배치 정규화(batch normalization)
 dataset을 사전에 정규화하는 것과는 달리 batch normalization은 각 미니 배치별로 학습 전에 정규화 처리를 하는 기법이다.
데이터의 전처리로서 dataset을 정규화하고 weight의 초기값을 정리함으로써 학습이 잘 진행되기는 하지만 학습시킬 때에는
신경망 모델 내부에서 분산이 편중되어 버리기 때문에 전처리를 한 효과가 한정적일 수 밖에 없다.
 batch normalization은 학습에 사용하는 각 미니 배치별로 정규화를 하기 때문에 학습 과정 전체에서 효과가 나타난다.
 미니 배치의 장점으로는 1. 학습률을 크게 설정해도 학습이 잘 진행된다. 2. dropout을 사용하지 않아도 일반화 성능이 높다.
