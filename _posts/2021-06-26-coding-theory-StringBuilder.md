---
title: "[Java] StringBuilder, StringBuffer"
layout: post
categories: coding
tags: theory
---

백준을 통해 프로그래밍을 하다보면 출력을 할 때 StringBuilder를 많이 사용하게 된다. StringBuilder는 책에서 잠깐 본 기억만 나고 학교에서는 별로 사용하지 않았었다.    
BufferedWriter같이 System.out.print보다 출력 시간을 매우 단축시킬 수 있다.    

### String과의 차이
StringBuilder란 __가변성__ 을 가진 객체이다. 이는 매우 중요한 것으로 이와 반대로 String객체는 immutable, 즉 불면성을 가진 객체이다.    
따라서 String 객체의 값을 변경하면(+연산자나 concat을 통해) 내부적으로 Autoboxing, Unboxing과정을 통해 concat 메소드를 참조해 기존의 메모리에서 값이 바뀌는 것이 아닌, 그 값을 버리고 새로운 값을 재할당 하는 것이다.   

```java
public class Step3_11021_1 {
    public static void main(String[] args) {
        String temp = "";
        System.out.println(System.identityHashCode(temp));
        temp += "hello ";
        System.out.println(System.identityHashCode(temp));
        temp += "world\n";
        System.out.println(System.identityHashCode(temp));
        
        System.out.println(temp);


        StringBuilder sb = new StringBuilder();
        sb.append("hello ");
        System.out.println(System.identityHashCode(sb));
        sb.append("world\n");
        System.out.println(System.identityHashCode(sb));
        
        System.out.println(sb);

        
        StringBuffer bf = new StringBuffer();
        bf.append("hello ");
        System.out.println(System.identityHashCode(bf));
        bf.append("world\n");
        System.out.println(System.identityHashCode(bf));

        System.out.println(bf);
    }
}
```    

<img src="https://user-images.githubusercontent.com/68698007/123508882-04042980-d6ad-11eb-8223-a6b41ff11072.png" width="10%" height="10%">

보다시피 String으로 이어붙일때마다 객체가 생성돼 주소값이 변경되는 것을 알 수 있다.
<br>
이런 변경을 1000번 이상 하게 되면 힙 메모리에 많은 garbage가 생기고 힙 메모리 부족으로 이어져 성능에 영향을 미치게 된다.    

<br>
이를 해결하기 위한 방법이 <mark style='background-color: #fff5b1'>StringBuilder와 StringBuffer</mark>이다.    
이 둘은 가변성을 가지기 때문에 내용에 변경이 생기면 __새로운 객체를 생성하는 게 아닌 가변성이 있는
sequence를 수정__ 하는 것이라 훨씬 빠르게 작동할 수 있다. (내부적으로 boxing 과정을 거치지 않음)
<br><br>

### StringBuilder와 StringBuffer의 차이
| StringBuilder | StringBuffer |
|-------|-------|
| 동기화 지원 X<br> -> 멀티 쓰레드 환경 적합 X, 단일 쓰레드 환경 | 동기화 지원 O<br> -> 멀티 쓰레드 환경 적합 O |    


그러나 쓰레드 환경이 아닌 이상은 StringBuilder가 성능이 뛰어나 StringBuilder를 사용하면 된다.    
StringBuffer 자료형은 String 자료형보다 무거운 편에 속한다. new로 객체를 생성하는 것은 일반 String을 사용하는 것보다
메모리 사용량도 많고 속도도 느리다. 
