---
title: WHy Spring?
layout: post
categories: coding
tags: spring
---

## 프레임워크 
'복잡한 문제를 해결하거나 서술하는데 사용되는 기본 개념 구조'  [위키백과]    
'소프트웨어의 구체적인 부분에 해당하는 설계와 구현을 재사용이 가능하게끔 일련의 협업화된 형태로 클래스들을 제공하는 것'    
'특정 프로그램을 개발하기 위한 여러 요소들과 메뉴얼인 룰을 제공하는 프로그램'    
<br>
__스프링은 자바 프레임워크이다 그렇다면 왜 굳이 프레임워크를 사용해야 되는가?__    

프레임워크는 구조화된 스크립트를 통해 개발자의 스크립트 패턴을 정형화 할 수 있도록 해주며 개발자가 반복적으로 해야 하는 공통부분을 최소화 할 수 있도록 설계되어있다.    
✔ 체계적인 코드관리로 유지보수가 용이하다    
✔ 기본설계 및 기능 라이브러리를 제공하여 개발 생산성이 높다    
✔ 코드에 대한 재사용성이 높다    
✔ 추상화된 코드 제공을 통해 확장성이 좋다    

<br>
아직까지의 위의 설명으로 충분하지 않지만 공부하다보면 이해할 수 있을 것 같다!
<br><br><br>

## Spring Framework
<div><center>“Spring makes programming Java quicker, easier, and safer for everybody. Spring’s focus on speed, simplicity, and productivity has made it the world's most popular Java framework.”</center></div>    
<br>
Spring Framework는 Dependency Injection(DI)를 지원하는 컨테이너이다. 이를 통해 다형성, OCP(개방-폐쇄 원칙), DIP (의존관계 역전 원칙)를 가능하게 지원한다.    


<br>✔ POJO(Plane Old Java Object)를 이용한 쉬운 개발: 단순 오브젝트는 의존성이 없고 추후 테스트 및 유지보수가 편리한 유연성의 장점을 갖는다.    
✔ Loose Coupling: Dependency Injection과 Interface를 활용한 객체들 간의 느슨한 결합    
✔ AOP (Aspect Oriented Programming): 관점 지향 프로그래밍. 핵심 기능과 공통 기능을 분리시켜 핵심 로직에 영향을 끼치지 않게 공통 기능을 끼워 넣는 개발 형태로 효율적인 유지보수 및 재활용성 극대화    


### Spring 공부
1. [Spring Web MVC framework]()
2. [Spring Bean]()
3. [Dependency Injection]()
