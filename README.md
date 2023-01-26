문서정보 : 2023.01.25. 작성, 작성자 [@SAgiKPJH](https://github.com/SAgiKPJH)

<br>

# MachineLearning_TensorFlow.js_JavaScript

<img src="https://user-images.githubusercontent.com/66783849/214444371-c07b93e6-69b8-47d3-b084-37f24da52dab.png" width="250">

### 목적
- 책 [머신러닝 TensorFlow.js JavaScript]를 읽고 요약한다.

### 목표

- [ ] 1부 TensorFlow.js
  - [x] [1. 개요](https://github.com/SagiK-Repository/MachineLearning_TensorFlow.js_JavaScript/blob/main/README.md#1-%EA%B0%9C%EC%9A%94)
  - [ ] 2. Tensor 생성
  - [ ] 3. 함수, 식, 행렬
  - [ ] 4. Tensor 연산
  - [ ] 5. Tensor Class
  - [ ] 6. Tensor 추출, 변환
  - [ ] 7. 메모리 관리
  - [ ] 8. TensorFlow.js 모델링
- [ ] 2부 선형 회귀
  - [ ] 9. 선형 회귀
  - [ ] 10. 경사 하강법 Ⅰ
  - [ ] 11. 경사 하강법 Ⅱ
  - [ ] 12. 옵티마이저
  - [ ] 13. 다중·다항 회귀 모델
  - [ ] 14. 선형 회귀 정규화
- [ ] 3부 분류
  - [ ] 15.  로지스틱 회귀
  - [ ] 16. 활성화 함수
  - [ ] 17. 소프트맥스 회귀
- [ ] 4부 이미지 인식
  - [ ] 18.  이미지 인식
- [ ] 부록
  - [ ] 1. TensorFlow.js 설치
  - [ ] 2. 그래프 작성 방법
  - [ ] Index

### 제작자
[@SAgiKPJH](https://github.com/SAgiKPJH)

### 참조

- [머신러닝 TensorFlow.js JavaScript](http://www.yes24.com/Product/Goods/71863932)

<br><br>

---

# 1부 TensorFlow.js

## 1. 개요

- 머신러닝 목적 : 추론
- TensorFlow에서 Tensor는 수학에서 사용하는 언어, Flow는 Tensor의 흐름이다.
  - Tensor로 값을 구한 후에, 이어진 흐름상의 Tensor에 Tensor를 넘겨주면 다시 값을 구하는 흐름이다.
- Tensor와 자바스크립트 인스턴스의 차이는 플로우(Flow)가 있다는 점이다.
  ```js
  const one = tf.Scalar(1), two = tf.Scalar(2), five = tf.Scalar(5);

  tf.add(one, two).div(five);
  ```
- TensorFlow.js 파일을 설치해야 한다. <부록>
- TF.js는 머신러닝 모델 개발을 가히 위한 라이브러리이다.

<br><br>

## 2. Tensor 생성

- TF.js의 근본인 Tensor를 생성해본다.
  ```js
  tf.Tensor(10).print(); // 10
  tf.Tensor([1, 2, 3, 4]).print(); // [1, 2, 3, 4]
  tf.Tensor([[1, 2], [3, 4]]).print(); // [[1, 2], [3, 4]]
  tf.Tensor([[1, 2, 3, 4, 5, 6], [2, 3]]).print(); // [[1, 2, 3], [4, 5, 6]] (2행 3열)
  tf.Tensor([[1, 2, 3, 4, 5, 6], [2, 3, 1]).print(); // [[[1, 2, 3], [4, 5, 6]]] (1차원 2행 3열)

  const one = tf.Tensor([1, 2]);
  tf.print(one); // [1, 2]
  web.log(one);

  tf.Tensor([31, 32]).print(true);
  // dtype: float32
  // rank : 1
  // shape : [2]
  // value :
  // [31, 32]
  ```
- TypeArray 오브젝트를 생성할 수 있다.
  ```js
  const typed32 = new Int32Array(2);
  typed32[0] = 128;
  tf.Tensor(typed32).print(); // [128, 0]

  const buffer = new ArrayBuffer(12); // 12바이트
  const buffer32 = new Float32Array(buffer); // 4바이트 단위로 실수값을 View하기에, 3개의 엘리먼트
  buffer32[0] = 4.5, buffer32[2] = 9.1;
  tf.Tensor(buffer32).print(); // [4.5, 0, 9.1]
  
  const buffer8 = new Unit8Array(2); // 8비트 처리 (0~255), RGB 값 때 많이 사용
  buffer8[0] = 1;
  tf.Tensor(buffer8).print(); // [1, 0]
  
  tf.tensor1d([1, 2, 3]); // [1, 2, 3]
  tf.tensor1d([1,-3, 0], bool); // [1, 0, 0]
  tf.tensor2d([1, 2, 3, 4, 5, 6], [3, 2]);
  ```
- scalar Tensor
  ```js
  tf.scalar(123).print(true);
  // dtype : float 32
  // rank : 0
  // shape : []
  // values : 123

  tf.scalar(true).print(true);
  // dtype : bool
  // rank : 0
  // shape : []
  // values : 1
  ```


<br><br>

## 3. 함수, 식, 행렬

<br><br>

## 4. Tensor 연산

<br><br>

## 5. Tensor Class

<br><br>

## 6. Tensor 추출, 변환

<br><br>

## 7. 메모리 관리

<br><br>

## 8. TensorFlow.js 모델링

<br><br><br>

# 2부 선형 회귀

<br><br>

## 9. 선형 회귀

<br><br>

## 10. 경사 하강법 Ⅰ

<br><br>

## 11. 경사 하강법 Ⅱ

<br><br>

## 12. 옵티마이저

<br><br>

## 13. 다중·다항 회귀 모델

<br><br>

## 14. 선형 회귀 정규화

<br><br><br>

# 3부 분류

<br><br>

## 15.  로지스틱 회귀

<br><br>

## 16. 활성화 함수

<br><br>

## 17. 소프트맥스 회귀

<br><br><br>

# 4부 이미지 인식

<br><br>

## 18.  이미지 인식

<br><br><br>

# 부록

<br><br>

## 1. TensorFlow.js 설치

<br><br>

## 2. 그래프 작성 방법

<br><br>

## Index

<br><br>
