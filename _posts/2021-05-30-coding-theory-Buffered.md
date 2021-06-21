---
title: "[Java] BufferedReader/BufferedWriter"
layout: post
categories: coding
tags: theory
comments: true
---
## BufferedReader/BufferedWriter
<hr>
버퍼를 이용해 읽고 쓰는 함수
Scanner보다 입출력의 효율이 훨씬 좋음
    
버퍼링 없이 키보드가 눌릴 때마다 문자가 전달되면 버퍼에 모았다가 전달하는 것보다 비효율적.    
BufferedReader와 BufferedWriter 클래스의 메소드들은 입출력에러가 발생할 경우 자체적으로 IOException을 던지도록 정의되어 있어 IOException 처리를 별도로 해줘야 한다. (throws IOException 또는 try~catch문)    

* 버퍼를 이용한 입력: BufferedReader
* 버퍼를 이용한 출력: BufferedWriter

#### BufferedReader
* Scanner: 띄어쓰기와 개행문자를 경계로 입력 값 인식 -> 따로 가공할 필요가 없음
* BufferedReader: 개행문자만 경계로 인식. 받은 데이터가 String으로 고정 -> 데이터 가공 필요. but Scanner에 비해 상대적으로 빠름
    
_입력 스트림에서 문자를 읽는 함수인데 문자나 배열, 라인들을 효율적으로 읽기 위해서 문자들을 버퍼에 저장하고 읽음. 버퍼 사이즈는 지정하거나 디폴트 사이즈를 사용.
-> 많은 데이터를 입력받아야 할 상황에서는 BufferedReader 사용_

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
StringBuilder sb = new StringBuilder();

int n = Integer.parseInt(br.readLine()); // 한 줄을 읽어서 String으로 반환

br.close(); // 입출력이 끝난 후 입력스트림을 닫고 사용하던 자원을 풀어줌
```
위와 같은 식으로 문자를 받아온다. 받은 문자를 나누기 위해서는 StringTokenizer의 nextToken함수를 이용하거나 String 클래스의 split함수를 이용하면 된다.    

만약 입력을    
5    
1 2     
3 4     
으로 받을 경우 br.readLine이 입력의 처음부터 끝까지, 즉 전체를 입력받는게 아니라 __개행문자를 기준__ 으로 읽어들여서 한 줄씩 읽게되는 것이다.    
br.read()를 사용할 경우에는 전체를 다 읽어오는 게 아닌 값을 읽어올 때, int 값으로 변형하여 읽어오는 것이다. (1 -> 1로 읽는 게 아닌 아스키 값 '1'을 읽어와 int값으로 49가 들어온다.    
즉
- br.readLine(): 개행문자를 기준으로 = 한 줄씩 읽음
- br.read(): ASCII 형식의 문자값의 int값을 반환    


#### BufferedWriter
* System.out.println(): 함수가 문자열 출력(write())과 개행(newLine())을 동시에 해줌. 시스템 리소스를 필요 이상으로 잡아먹는다는 한계가 존재. OS의 콘솔을 활성화 시키면서 CPU 리소스를 점유.
* BufferedWriter: 버퍼에 저장된 문자를 출력. System.out.println처럼 함수가 문자열 출력과 개행을 동시에 해주지 않기 때문에 개행을 하려면 write에 "\n"을 넣어주거나 newLine()함수 사용


```java
import java.io.BufferedWriter;
import java.io.OutputStreamWriter;
 
public class BufferedWriterTest {
    public static void main(String[] args) throws Exception {
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
 
        bw.write("Hello World!"); //BufferedWriter 객체를 이용해 출력
 
        // write한다고 해서 바로바로 출력되지 않음
        // 직접 출력 stream에 반영되는 것이 아니라 성능을 위해 buffer에 저장해두었다가
        // BufferedWriter가 flush되거나 close되었을 때 한번에 출력 stream에 반영하기 때문
        bw.flush();
 
        // close는 stream을 닫아버리기 때문에 계속 출력하고자 한다면 flush 사용
        // bw.close();

        bw.newLine();
        bw.close();
    }
}
```    
- BufferedWriter 객체는 반드시 flush() 또는 close()를 해서 스트림을 끝내야 한다.
