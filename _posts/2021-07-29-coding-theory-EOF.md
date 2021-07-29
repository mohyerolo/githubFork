---
title: "[Java] EOF"
layout: post
categories: coding
tags: theory
---
백준 10951문제에서 EOF를 검사하는 문제를 풀어보고 내가 EOF에 대해 자세히는 모르고 있다는 걸 알았다.    
파일의 끝이라는 것만 알고있어 좀 더 자세히 알아봐야되겠다는 생각이 들었다.   

EOF란 __파일의 끝__ 으로 (End Of File) 데이터 소스로부터 더 이상 읽을 수 있는 데이터가 없음을 나타내는 것이다.    
EOF의 실제 값은 시스템에 따라 다르며 파일뿐만 아니라 키보드를 통한 입력 시에도 입력의 끝을 알려주는 방법이 필요하다.
윈도우 명령창에서는 해당 라인의 어디에서든 Ctrl+Z를 누르고 나서 Enter를 누르면 발생시킬 수 있다.    

Java에서는 입력 클래스가 Scanner와 BufferedReader 두 가지로 구성되고 각각의 EOF 처리 방법이 다르다.

### Scanner
```java
public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);

    while (true) {
        int s = sc.nextInt();
        System.out.println(s);
    }
}
```
![image](https://user-images.githubusercontent.com/68698007/127435807-4c6d9151-d21f-4718-879d-16cfa3e53160.png)

Scanner에서는 EOF가 발생하면 NoSuchElementException이라는 예외가 발생한다.    
이런 예외는 try-catch문으로 종료 처리를 해주거나 Scanner의 hasNext(), hasNextInt()등과 같은 메소드를 통해 처리해주면 된다.    

### BufferedReader
```java
public static void main(String[] args) {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    while (br.readLine() != null) {
        ...
    }
}
```
BufferedReader는 EOF인 경우 null을 반환한다. 버퍼를 통해 이용하는 것이므로 버퍼가 비어있으면 null을 반환하는 것이다.    
