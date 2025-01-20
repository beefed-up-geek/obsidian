# Lecture 2: Image Classification Pipeline
* 수강 일자: 2025-01-20
* [강의 영상](https://www.youtube.com/watch?v=OoUX-nOEjG0&list=PL3FW7Lu3i5JvHM8ljYj-zLfQRF3EO8sYv&index=2) 
* [강의 노트](http://cs231n.stanford.edu/slides/2017/cs231n_2017_lecture1.pdf)
* 면접 질문
> 1. 두 데이터의 차이를 잴 때 <U>Manhattan Distance</U>와 <U>Euclidian Distance</U> 어떨 때 사용해야할까?
> 2. KNN의 시간복잡도는? 
> 3. KNN의 두 가지 한계가 무엇일까?
> 4. Linear Classification의 한계가 무엇일까?

---
CS231n 강의의 전반부는 Image Classification을 주로 다룬다. 이는 특정 이미지가 주어지면, 이미지를 특정 레이블로 분류하는 작업이다. (강의에서는 예제로 [CIFAR10](https://www.cs.toronto.edu/~kriz/cifar.html) 데이터셋을 사용한다. )
![[Screenshot 2025-01-20 at 3.38.53 PM.png|300]]
이미지를 분류하기 위한 가장 naïve한 방식으로는 KNN이 있다. 

KNN(K-Nearest Neighbors)알고리즘은 라벨링된 데이터와 분류하고자하는 데이터의 차이(distance)를 모두 계산해서, 가장 가까운 K개의 라벨링된 데이터 중 다수를 차지하는 라벨로 새로운 데이터를 분류한다. 
![[Screenshot 2025-01-20 at 3.53.53 PM.png]]
KNN 모델의 학습을 위해서는 단순히 데이터셋의 모든 데이터를 변수로 할장하면 되므로 O(1)이 필요하고, KNN을 통해 새로운 데이터를 분류하기 위해서는 새로운 데아터와 데이터셋 안의 모든 데이터 사이의 거리를 계산해야하므로 O(N)이 소요된다.
> KNN 시간복잡도
> 학습: O(1) / 예측: O(N)

KNN 알고리즘은 두가지 hyperparameter를 갖는다. K값과 Distance측정 방식이다. K값을 정하는 방법은 단순히 다양한 K값에 따른 검증 데이터에서의 성능을 측정해서 정한다. 아래의 데이터에서는 K=7일때 성능이 가장 우수하다.
![[Screenshot 2025-01-20 at 4.05.12 PM.png | 300]]

두 번째로 Distance 측정 방식은 사실 매우 다양하지만 이번 강의에서는 Manhattan Distance(L1)과 Euclidian Distance(L2)를 다룬다. 
![[Screenshot 2025-01-20 at 4.08.24 PM.png|300]]
이때 거의 대부분의 상황에서는 L2를 사용하는 것이 훨씬 직관적이지만, 아래와 같은 표에서 각 차원에 있는 데이터가 서로 다른 의미를 갖는 경우 L1을 사용해 서로다른 데이터 사이의 거리를 측정하는 것이 더 직관적이다. 

| 이름  | 직급  | 부서  | 연봉  |
| --- | --- | --- | --- |
| 사원1 | 인턴  | 개발  | 2천  |
| 사원2 | 부장  | 운영  | 3천  |
> 두 데이터의 차이를 잴 때 <U>Manhattan Distance</U>와 <U>Euclidian Distance</U> 어떨 때 사용해야할까?
> 	표 데이터에서와 같이 각 차원이 의미하는 바가 서로 다르다면 L1을 쓰는 것이 더 직관적이다. 

