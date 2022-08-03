---
layout: single
title: "[Java] 자바 제네릭(Generic)"
categories: Java
---

## 제네릭(Generic)이란 무엇일까?

### 이 글을 쓰게 된 이유

자바 웹 개발 강의를 듣던 중
![1](https://user-images.githubusercontent.com/77107216/182593407-b5fea8c5-927f-4f77-a0b6-2e8a837939ef.png)
![2](https://user-images.githubusercontent.com/77107216/182593435-02146b43-72de-4549-8960-b5a4def1d648.png)
이와 같이 CrudController을 상속받을 때 제네릭클래스를 이용하여
소스코드를 간편하게 리팩토링을 하는 것을 보고 제네릭클래스에 대해 제대로 알고 싶어져 공부해보았다.

---

## 제네릭이란?

다양한 타입의 객체들을 다루는 메서드나 클래스에 컴파일 시의 타입 체크를 해주는 기능이다.

#### 제네릭을 왜 써야 할까?

컴파일 타임에 타입 검사를 해주기 때문에 객체의 타입 안전성을 높이고 캐스팅과 같은 타입 변환의 번거로움이 줄어든다.

#### 제네릭을 사용하는 법:

Class\<T>, interface\<T>와 같이 일반 클래스나 인터페이스에 \<T>를 붙여주면 제네릭 클래스가 되어 모든 타입을 받는 것이 가능하다.

여기서 **T**는 타입 매개변수라고 한다.

#### 다양한 타입 매개변수

T - Type
E - Element
K - Key
V - Value
N - Number
S, U , V - 2nd, 3rd, 4th types

타입 매개변수는 보통 이와 같이 표기하는 것이 관례이지만 자신이 원하는대로 표기하여 사용해도 문제가 되지 않는다.

#### 제네릭의 문제점

Class에 제한없는 타입을 받는 \<T>만 선언할 경우 제네릭은 모든 타입을 받을 수 있기 때문에 여러 문제점이 발생할 수 있다.

#### 문제점의 해결방법

그래서 모든 타입을 받지 않게 제한을 해줄 필요가 있는데 <T extends (제한할 타입)>와 같이 제한할 타입을 타입 매개변수에 extends 해주면 된다.

#### 제네릭을 메서드에서 사용할 경우:

```java
public <T> T pizza(List<T> list){}
```

|     구조      |     설명      |
| :-----------: | :-----------: |
|     \<T>      | 타입 매개변수 |
|       T       |   리턴 타입   |
|     pizza     |   메소드 명   |
| List\<T> list |   매개변수    |

#### 메서드에서 타입 매개변수의 범위를 제한 하고 싶다면?

```java
public <T extends food> T pizza(List<T> list){}
```

타입 매개변수에 원하는 타입을 extends를 통해 제한할 수 있다.

---

#### 배열과 제네릭의 차이로 알아보는 공변과 불공변

공변(covariant) : A가 B의 하위 타입일 때, T\<A> 가 T\<B>의 하위 타입이면 T는 공변
불공변(invariant) : A가 B의 하위 타입일 때, T\<A> 가 T\<B>의 하위 타입이 아니면 T는 불공변

배열에서는 Integer $ \rightarrow $ Object 가능 (배열은 공변)

```java
Object[] objectArray = new Integer[1];
```

제네릭에서는 Integer $ \rightarrow $ Object 불가능 Complie Error 발생!! (제네릭은 불공변)

```java
List<Object> objectList = new ArrayList<Integer>();
```

제네릭은 불공변이므로 이와 같은 경우 컴파일 에러가 발생한다.
이러한 제네릭의 불공변 때문에 **와일드카드 제네릭의 \<?>타입**이 등장하게 되었다.

#### 와일드카드

제네릭 타입을 사용하고 싶지만, 들어오는 타입 매개변수가 무엇인지 신경쓰고 싶지 않다면 와일드카드 \<?>를 사용한다.

##### 제네릭과 와일드카드의 차이

**제네릭** : 지금은 타입을 모르지만, 타입이 정해지면 그 타입의 특성에 맞게 사용한다.
**와일드카드** : 지금도 무슨 타입인지 모르고, 앞으로도 모를 것이다.

\<?> 모든 타입이 가능 \<? extends Objects>와 동일

\<? extends (제한할 타입)> 제한할 타입과 그것의 하위 타입만 가능

\<? super (제한할 타입)> 제한할 타입과 그것의 상위 타입만 가능

---

### 참조

https://www.youtube.com/watch?v=n28M8iryFPw
https://opentutorials.org/module/516/6237
https://vvshinevv.tistory.com/55?category=692309

잘못된 정보가 기재되어있을 경우 피드백해주시면 감사하겠습니다!
