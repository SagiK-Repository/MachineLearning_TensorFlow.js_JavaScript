문서정보 : 2023.01.25. 작성, 작성자 [@SAgiKPJH](https://github.com/SAgiKPJH)

<br>

# MachineLearning_TensorFlow.js_JavaScript

<img src="https://user-images.githubusercontent.com/66783849/214444371-c07b93e6-69b8-47d3-b084-37f24da52dab.png" width="250">

### 목적
- 책 [머신러닝 TensorFlow.js JavaScript]를 읽고 요약한다.

### 목표

- [ ] 1부 TensorFlow.js
  - [x] [1. 개요](https://github.com/SagiK-Repository/MachineLearning_TensorFlow.js_JavaScript/blob/main/README.md#1-%EA%B0%9C%EC%9A%94)
  - [x] 2. Tensor 생성
  - [x] 3. 함수, 식, 행렬
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

- 벡터
  ```js
  const tsOne = tf.tensor1d([10, 13, 16]);
  const tsTwo = tf.tensor1d([1, 3, 5]);
  
  tsOne.add(tsTwo); // [11, 16, 21]
  tsOne.sub(tsTwo); // [9, 10, 11]
  
  const tsScl = tf.scalar(7);  
  tsScl.add(tsTwo); // [8, 10, 12]
  
  // 내적
  tsOne.dot(tsTwo); // 32
  
  // 외적
  tf.outerProduct(tsOne, tsTwo); // [[4, 5, 6], [8, 10, 12], [12, 15, 18]]
  ```
- 행렬
  ```js
  const tsOne = tf.tensor2d([1, 2 ,3 ,4], [2, 2]);
  const tsTwo = tf.tensor2d([5, 6, 7, 8], [2, 2]);
  
  tsOne.add(tsTwo); // [[6, 8], [10, 12]]
  
  const tsThr = tf.tensor1d([1, 2]);
  tsOne.add(tsThr); // [[2, 4], [4, 6]]
  
  // 행렬곱
  tsTwo = tf.tensor2d([[5], [6]]);
  tsOne.matMul(tsTwo); // [[17], [39]]
  
  // 엘리먼트-와이즈 곱
  tsOne.mul(tsTwo); // [[5, 10], [18, 24]]
  ```

<br><br>

## 4. Tensor 연산

- tensor 산술연산
  - add() : 더하기
  - addN() : 더하기, 파라미터에 배열로 다수의 tf.Tensor 작성
  - sub() : 빼기
  - mul() : 곱하기
  - div() : 나누기
  - floorDiv() : 나눈 몫
  - tf.mod() : 나눈 나머지, 몫은 버림
  - tf.maximum() : 가장 큰 값 (엘리먼트 비교)
  - tf.minimum() : 가장 작은 값 (엘리먼트 비교)
  - tf.pow() : 거듭제곱
  - tf.squaredDifference() : 차이 제곱
  - tf.cumsum() : 누적
- tensor 논리연산
  - tf.equal()
  - tf.notEqual()
  - tf.greater() : >
  - tf.greaterEqual() : >=
  - tf.less()
  - tf.lessEqual()
  - tf.logicalAnd() : &&
  - tf.logicalOr()
  - tf.logicalNot()
  - tf.logicalXor()
  - tf.where() : a||b, 상태에 따라 값 변환
  - tf.whereAsync() : 값이 true일 때 값의 인덱스 반환, Promise 처리
- tensor 수열
  ```js
  // 등차수열
  const tsOne = tf.linspace(0, 10, 5); // [0, 2.5, 5, 7.5, 10]
  tf.range(0, 8, 2); // [0, 2, 4, 6]
  tf.range(0, 3); // [0, 1, 2]
  tf.range(7, 0, -2); // [7, 5, 3, 1]
  
  // 시그마
  tf.range(0, 10, 2).sum(); // 20
  tf.zeros(); // 모두 0
  tf.zerosLike(); // shape가 같은 tf.Tensor 생성 + 0
  tf.ones(); tf.onesLike();
  tf.fill(); // 모든 엘리먼트 값을 스칼라로 대체
  tf.clone();
  ```
- 수학식
  ```js
  tf.abs(); // 절댓값
  tf.ceil(); // 최소 정수
  tf.floor(); // 최대 정수
  tf.round(); // 반올림
  // ...
  ```
- 특수 기능
  ```js
  // 최대 최소
  const tsOne = tf.tensor1d([1, 2, -3, 4]);
  tsOne.clipByValue(-2, 3); // [1, 2, -2, 3]
  tf.clipByValue(tsOne, -2, 3); // 동일
  ```

<br><br>

## 5. Tensor Class

- 함수 목록
  ```js
  // shape 변환
  const tsOne = tf.tensor2d([[1, 2], [3, 4]]).flatten(); // [1, 2, 3, 4]
  const tsTwo = tf.tensor2d([1, 2, 3, 4], [2, 2]).reshapeAs(tsOne); // [1, 2, 3, 4]

  // 스칼라 변환
  tf.tensor1d([124]).asScalar(); // 124

  // 랭크 변환
  tf.tensor3d([[[1], [2], [3], [4]]]).as2D(); // [[1, 2], [3, 4]]
  tf.tensor3d([[[1], [2], [3], [4]]]).as1D(); // [1, 2, 3, 4]

  // 값 타입 변환
  tf.tendor1d([1.0, 2.1, 3.1]).asType('int32'); // [1, 2, 3]

  // 동기 방법 텐서 추출
  const tsOne = tf.tensor2d([[1, 2], [3, 4]]);
  const typedData = tsOne.dataSync(); // tsOne을 TypedArray 오브젝트로 변환
  web.getArray(typedData); // [1, 2, 3, 4]
  getArray(values){
    if (values.shape) { values = values.dataSync(); }
    return Array.from(values).map((value) => {return value});
  }

  // 비동기 방법 텐서 추출
  const tsOne = tf.tensor2d([[1], [3]]);
  const typedData = await tsTwo.data(); // 0: 1  1: 3
  ```

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
