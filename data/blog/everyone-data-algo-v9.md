---
title: 누구나 자료구조와 알고리즘) 09. 재귀를 사용한 재귀적 반복
date: '2022-11-09'
tags: ['자료구조', '알고리즘']
draft: false
summary: 9장 이후에 나올 알고리즘을 이해하기 위해서 재귀를 알아봅시다!
images: []
---

# 9. 재귀를 사용한 재귀적 반복

9장 이후에 나올 알고리즘을 이해하기 위해서 재귀를 알아봅시다!

자기 자신을 호출할 때 재귀라는 말을 사용한다.

![자기 자신을 호출하는 함수를 재귀 함수라고 함.](/static/images/data/data09/01.png)

자기 자신을 호출하는 함수를 재귀 함수라고 함.

## 9.1 루프 대신 재귀

아니 왜 …? 루프 돌려 그냥!

10부터 0까지 1초에 하나씩 표시해야 하는 프로그램을 만들어야 한다면?

```jsx
function countdown(number) {
	for(var i = number; i >= 0; i—-) {
		console.log(i)
	}
}
countdown(10);
```

이런식으로 루프를 돌릴 수 있지만 재귀를 사용한다면 ?

```jsx
function countdown(number) {
  console.log(number)
  countdown(number - 1)
}
countdown(10)
```

자신을 호출하는 재귀함수를 만들 수 있다.

**재귀를 쓸 수 있는 경우라고 해서 재귀를 무조건 사용하는 것이 좋은 예는 아니다.**

재귀는 명쾌한 코드 작성을 도와주는 하나의 도구일 뿐…

## 9.2 기저 조건(base case)

```jsx
function countdown(number) {
  console.log(number)
  countdown(number - 1)
}
countdown(10)
```

위 함수를 실행하다 보면
우리가 원하는 마지막 단계인 number에 0 값이 들어가는 경우 이후에도
-1, -2 … 등 음수가 들어가게 될 것이다.

우리는 이 문제를 해결하기 위해 number가 0 일 경우, 더 이상 재귀를 호출하지 않는 조건문을 추가해야 한다.

```jsx
function countdown(number) {
	console.log(number) ;
	if(number === 0) {
		return;
	} else {
		countdown(number — 1);
	}
}
countdown(10);
```

재귀에서 메소드가 반복되지 않는 경우(더 이상 재귀가 발생하지 않는 조건)를 기저 조건 혹은 중단 조건이라 한다.

즉, 위 함수에서 기저 조건은 0이다.

## 9.3 재귀 코드 읽기

계승을 계산하는 예제를 살펴보자.

3의 계승은 다음과 같다!

3 \* \*2 \*\* 1 = 6

계승 = 팩토리얼 = !

계승을 반환하는 함수를 재귀적으로 구현하는 루비 코드로 살펴보자… 왜 루비임?

```ruby
def factorial(number)
	if number == 1
		return 1
	else
		return number * factorial(number - 1)
	end
end
```

이렇게 보면 어렵지만, 재귀 코드를 읽는 법을 알면 쉽다고 하는데 어렵다..

1. 기저 조건이 무엇인지 찾는다
   → 여기에서 기저 조건은 number == 1 의 경우이다.
2. 기저 조건을 다룬다는 가정하에 함수를 살펴본다.
3. 기저 조건 바로 전 조건을 다룬다는 가정하에 함수를 살펴본다.
   → 기저 조건 바로 전 조건은 number == 2 의 경우이다.
4. 한 번에 한 조건씩 올라가면서 계속 분석한다.

만약 factorial(3) 이라는 함수가 있다면

1. 기저 조건인 1의 경우에서 먼저 보자.
2. 1의 경우 1을 return 하고 종료된다.
3. 기저 조건의 전 단계를 살펴보자.
4. 2의 경우 2 \* factorial(1) = 1 이기 때문에 2를 리턴한다.
5. 이를 한번 더 반복할 경우, factorial(3)은 3 _ factorial(2) 이기 때문에 2의 값인 3 _ 2. 즉, 6을 리턴한다.

## 9.4 컴퓨터의 눈으로 바로본 재귀

컴퓨터는 스택을 사용해 어떤 함수를 호출 중인지 기록한다.
우리는 이것을 **호출 스택**이라 한다.

factorial(3)의 경우를 호출 스택으로 바라보자!

1. factorial(3)을 호출하자
2. factorial(3)을 수행하기 위해 factorial(2)를 호출해야 한다.
3. factorial(3)이 아직 끝나지 않았기 때문에 호출 스택에 푸시한다.

   ![스크린샷 2022-11-08 오후 3.37.35.png](/static/images/data/data09/02.png)

4. factorial(2)를 실행한다.
5. factorial(2)를 실행하기 위해 factorial(1)을 호출한다.
6. factorial(2)를 호출 스택에 푸시한다.

   ![스크린샷 2022-11-08 오후 3.41.09.png](/static/images/data/data09/03.png)

7. factorial(1)가 실행되고 factorial(1)은 기저 조건이기 때문에 재귀가 종료된다.
8. factorial(2)가 factorial(1)의 값을 리턴 받고 2 \* 1을 리턴하고 호출스택에서 팝된다.

   ![스크린샷 2022-11-08 오후 3.41.21.png](/static/images/data/data09/04.png)

9. factorial(3)이 factorial(2)의 값을 리턴 받고 3 _ 2 _ 1을 리턴하고 호출스택에서 팝된다.

   ![스크린샷 2022-11-08 오후 3.41.29.png](/static/images/data/data09/05.png)

9.1의 예제와 같이 무한 재귀가 있을 때 메모리에 공간이 없을 때까지 같은 메소드를 호출 스택에 푸시하고 이로 인해 **스택 오버플로우**가 발생하곤 한다.

## 9.5 재귀 다뤄보기

파일 시스템을 순회하는 예제를 살펴보자!

어떤 디렉토리 내에 있는 모든 파일을 작업하고 디렉토리안에 다른 하위 디렉토리도 수행하는 스크립트가 있다고 가정하자

주어진 상황을 루비코드로 만들어보면

![도저히 루비 정리 못하겠습니다. (노오력하세요.)](/static/images/data/data09/06.png)

도저히 루비 정리 못하겠습니다. (노오력하세요.)

위에 예시도 잘 작동하겠지만 바로 아래에 있는 하위 디렉토리 명만 출력하게 될 것이다.

한 단계 더 깊이 탐색할 수 있도록 업데이트해보자

![하.. 진짜 코드 ](/static/images/data/data09/07.png)

하.. 진짜 코드

이 경우에도 한계가 있다. 두 단계 아래 밖에 찾을 수 없다.

이 때, 재귀를 사용하면 쉽게 해결할 수 있다.

![스크린샷 2022-11-08 오후 3.55.45.png](/static/images/data/data09/08.png)

빅 오 측면에서 재귀만으로 알고리즘 효율성이 꼭 나아지는 것은 아니다.

하지만 재귀가 알고리즘 속도에 영향을 주는 핵심 요소가 될 수 있다.2162143

---

##### 해당 스터디는 팀원들과 함께 진행한 스터디이기에 모든 장을 혼자서 발표한 것이 아닙니다.

##### 다른 장도 궁금하다면 [노션](https://amplified-neptune-cfd.notion.site/HBT-9081eb15c1a04c9a821bb72052631e00)을 방문해주세요 :)