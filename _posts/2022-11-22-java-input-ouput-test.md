---
layout: single
title: "[Java] 사용자 입출력이 포함된 메서드 테스트하기"
categories: Java
tag: [java, junit]
published: true
---

# Java에서 사용자 입출력이 포함된 메서드를 테스트하는 방법을 알아보자

보통 Java에서는

```java
Scanner scanner = new Scanner(System.in)
String example = scanner.next();
```

Scanner를 이용해서 콘솔에 **입력**을 받고

```java
System.out.println(example);
```

System.out을 이용해 콘솔에 **출력**을 받는다.

하지만 이와 같은 사용자 입출력을 테스트를 하는 경우에는 직접 입력하거나 출력을 확인할 수가 없기에 입력을 할 때는 미리 사용자 입력을 설정해두고 출력을 할 때는 출력될 값을 따로 담아두는 방법을 이용하여 테스트를 해보았다.

자바에서 모든 입출력은 **stream**을 통해 이루어진다.  
그래서 콘솔의 입출력값은 자바와 데이터를 주고 받을 때 stream을 통해 데이터를 주고 받는다. 자바의 스트림은 **바이트(Byte)단위**로 자료의 입출력이 이루어지기 때문에 입출력값은 바이트단위로 만들어 주어야 한다.

### 입력 테스트

```java
String input = "입력할 값";
InputStream in = new ByteArrayInputStream(input.getBytes());
System.set(in); //
```

입력할 값을 바이트 단위로 만든 후에 ByteArrayInputStream에 담아준다. 그리고 System.setIn을 이용해 입력값을 미리 설정해준다. 이와 같은 방법을 이용하면 테스트를 할 떄 사용자 입력이 필요한 경우 미리 System.setIn에 설정해둔 값이 입력된다.

입력 예시  
![1](https://user-images.githubusercontent.com/77107216/203104821-6a070e3d-39a7-4acd-b0ce-7d725e55f1e5.png)
![3](https://user-images.githubusercontent.com/77107216/203112478-20abda2d-6d59-4ba7-b5e1-a3ce558111ae.png)  
정상적으로 테스트 완료가 된다.

### 출력 테스트

```java
OutputStream out = new ByteArrayOutputStream();
System.setOut(new PrintStream(out));
```

System.out은 PrintStream의 인스턴스이기 때문에 System.out.println와 같은 출력이 발생하면 System.setOut을 이용해 출력 값을 out에 담아 줄 수 있다. out.toString()를 이용하면 버퍼에 저장된 바이트 값을 String으로 반환한다.

출력 예시  
![2](https://user-images.githubusercontent.com/77107216/203104824-824f7e75-f7e0-4b89-b40f-96db8b36be80.png)
![4](https://user-images.githubusercontent.com/77107216/203112482-7bad84b8-e632-44a3-a776-8fda28f70eb9.png)  
정상적으로 테스트 완료가 된다.

---

**잘못된 정보 또는 오타가 기재되어있을 경우 피드백해주시면 감사하겠습니다!**
