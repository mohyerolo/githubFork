---
title: "[Java] StringTokenizer와 split()"
layout: post
categories: coding
tags: theory
comments: true
---

Buffer를 사용하다보니 문자열을 구분하여 분리하는 기능이 필요하다. 그럴때는    
<mark style='background-color: #fff5b1'>StringTokenizer</mark>와 String 메소드 중 <mark style='background-color: #fff5b1'>split()</mark>을 사용할 수 있다.
    
### 1. StringTokenizer   
StringTokenizer 클래스는 문자열을 우리가 지정한 구분자로 쪼개주는 클래스이다. 쪼개어진 문자열을 token이라고 부른다.    

* 생성자
  * public StringTokenizer(String str): 전달된 매개변수 str을 디폴트 delimiter로 분리한다. 기본 delimiter는 공백 문자인 "\t\n\r\t"이다.
  * public StringTokenizer(String str, String delim): 매개변수로 전달된 delim으로 문자열을 분리한다.
  * public StringTokenizer(String str, String delim,boolean returnDelims): 특정 delim으로 분리시키는데 그 delim까지 token으로 포함할지는 결정. true일시 포함, false일땐 포함하지 않음.
   
* int countTokens(): 남아있는 token의 개수를 반환
* boolean hasMoreElements(), boolean hasMoreTokens(): 다음에 읽을 token이 있으면 true, 없으면 false 반환
* Object nextElement(), String nextToken(): 다음 token을 반환한다. 두 개는 같은 객체 반환이나 반환형이 다름

```java
public class StringTokenizerTest {
    public static void main(String[] args) {
        String str = "가\n나\t다\t라\r마 바 사      ";
        StringTokenizer st = new StringTokenizer(str);

        while(st.hasMoreTokens()) {
            System.out.println(st.nextToken());
        }
    }
}
```
결과값    
![image](https://user-images.githubusercontent.com/68698007/121765722-f4062900-cb87-11eb-9744-74b7ec1aaf78.png)
<br>
위와 같이 구분자를 지정해주지 않으면 디폴트 구분자로 무조건 나눠진다.
<br><br>

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

StringTokenizer st = new StringTokenizer(br.readLine(), " ");
int A = Integer.parseInt(st.nextToken());
int B = Integer.parseInt(st.nextToken());
```

백준 1330문제에서 사용했듯 사용자의 입력을 받아와 디폴트 구분자인 띄어쓰기이지만 표시를 해준 경우이다.
<br><br><br>
### 2. String[] split(String regex)
split 함수는 입력받은 정규표현식 또는 특정 문자를 기준으로 문자열을 분리해 배열에 저장하여 리턴한다.    
```java
String str = "가나\t다\t라마  바 사      ";
String[] tokens = str.split(" ");

for (int i = 0; i < tokens.length; i++) {
    System.out.println(tokens[i]);
}
```
결과값    
![image](https://user-images.githubusercontent.com/68698007/121767220-ece41880-cb91-11eb-8be1-4e1086244f2a.png)
<br>

StringTokenizer와 split은 일반적인 상황(데이터 사이에 구분자강 있는 경우)에서는 동일하게 동작하나 데이터 사이에 구분자가 두 번 있거나 중간이 비어있는 경우 split만 공백의 데이터를 반환한다.
