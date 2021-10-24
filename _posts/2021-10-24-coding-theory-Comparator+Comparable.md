---
title: "[Java] Comparator, Comparable"
layout: post
categories: coding
tags: theory
---
Comparator와 Comparable은 정렬을 할 경우에 주로 쓰이게 된다. 어떻게 쓰이는지는 밑에서 설명하겠지만 비교를 통해 값을 반환하고 그 값을 이용하는 것이다.    

비교를 하려면 부등호가 있는 데 굳이 Interface를 사용해서 해야되나 싶지만 이 둘은 Primitive type을 정렬하는 것이 아닌 객체의 정렬을 위해 사용되는 경우가 많다.    
<br>

```java
public class Sorting {
    public static void main(String[] args) {
        Student a = new Student(170, 58);
        Student b = new Student(163, 59);
    /**
     * 매번 if문으로 클래스의 각 값을 비교하며 쓸 수는 없음 
     */

    }
}
class Student {
    int height;
    int weight;

    Student(int height, int weight) {
        this.height = height;
        this.weight = weight;
    }
}
```

객체의 정렬이란 Student가 자신의 정보로 신장, 체중을 가지고 있을 경우 우리는 어떤 정보로 정렬을 할 지 생각할 수 있다. 그러나 기준이 정해져있는 것은 아니고 각자 기준이 다르니 이렇게 여러 개의 정보를 가지고 있을 경우 기존의 비교 방법으로는 해결 할 수 없는 것이 있다.    
<br>

이를 위해 <mark style='background-color: #fff5b1'>Comparable과 Comparator </mark>가 존재한다.    


## Interface Comparable
java.lang package에 있어 따로 import해 줄 필요가 없다.    

```java
public interface Comparable<T> {
    /**
     * @param   o the object to be compared.
     * @return  a negative integer, zero, or a positive integer as this object
     *          is less than, equal to, or greater than the specified object.
     *
     * @throws NullPointerException if the specified object is null
     * @throws ClassCastException if the specified object's type prevents it
     *         from being compared to this object.
     */
    public int compareTo(T o);
}
```    
Comparable은 보다시피 \<T\> 로 선언되어 객체가 들어갈 수 있다.    
compareTo(T o) 단 하나만을 가지고 있으며 따라서 Comparable을 implements할 때는 compareTo를 구현해주면 된다. 이 compareTo(T o) 메소드가 객체를 비교할 기준을 정의하는 부분이 되는 것이다.    

매개변수가 한 개이므로 Comparable은 __자기 자신과 매개변수로 들어온 객체를 비교__ 하는 것임을 알 수 있다.

그러면 위에서 본 Student를 아래와 같이 수정할 수 있다.

```java
class Student implements Comparable<Student> {
    int height;
    int weight;

    Student(int height, int weight) {
        this.height = height;
        this.weight = weight;
    }

    @Override
    public int compareTo(Student o) {
        // height를 기준으로 비교

        // 자기자신의 height가 매개변수로 들어온 o객체의 height보다 크다면 양수
        if (this.height > o.height) {
            return 1;
        }
        // 같다면 0
        else if (this.height == o.height) {
            return 0;
        }
        // 작다면 음수
        else {
            return -1;
        }
    }
}
```

결국 __양수, 0, 음수중 어떤 것이 반환되는지에 따라 어느 객체가 더 우선순위인지를 알 수 있게 된다__.     
위의 if-else문을 좀 더 간편하게 바꾼다면 아래와 같이 수정할 수 있다.

```java
class Student implements Comparable<Student> {
    int height;
    int weight;

    Student(int height, int weight) {
        this.height = height;
        this.weight = weight;
    }

    @Override
    public int compareTo(Student o) {
        /**
         * 만약 자기 자신의 height가 매개변수 객체보다 작다면 음수,
         * 같다면 0
         * 크다면 양수가 반환될 것
         */ 
        return this.height - o.height;
    }
}
```
<br>

Comparable은
- Arrays.sort(array)
- Collections.sort(list)    

에서 사용할 수 있다.    

<br>

예시

```java
public class Test {
    public static void main(String[] args) {
        List<Student> sList = new ArrayList<>();

        sList.add(new Student(170, 58));
        sList.add(new Student(163, 59));

        Collections.sort(sList);

        for(Student s : sList) {
			    System.out.println(s);
		    }
    }
}

class Student implements Comparable<Student> {
    int height;
    int weight;

    Student(int height, int weight) {
        this.height = height;
        this.weight = weight;
    }

    @Override
	  public String toString() {
		  return "Student [" + height + ", " + weight + "]";
	  }

    @Override
    public int compareTo(Student o) {
        return this.height - o.height;
    }
}
```

결과    
Student [163, 59]<br>
Student [170, 58]    

<br>

## Interface Comparator
java.util에 속해있어 import가 필요하다.    

```java
public interface Comparator<T> {
    /**
     * @param o1 the first object to be compared.
     * @param o2 the second object to be compared.
     * @return a negative integer, zero, or a positive integer as the
     *         first argument is less than, equal to, or greater than the
     *         second.
     * @throws NullPointerException if an argument is null and this
     *         comparator does not permit null arguments
     * @throws ClassCastException if the arguments' types prevent them from
     *         being compared by this comparator.
     */
    int compare(T o1, T o2);
}
```     

Comparator는 Comparable과 달리 많은 것을 가지고 있지만 필수로 구현해야 되는 것은 compare(T o1, T o2)다.    

Comparable과 달리 Comparator의 비교 함수는 매개변수가 두 개인 것을 볼 수 있다. 즉, Comparator는 __두 매개변수 객체를 비교__ 하는 것이다.

```java
class Student implements Comparator<Student> {
    int height;
    int weight;

    Student(int height, int weight) {
        this.height = height;
        this.weight = weight;
    }

    @Override
	  public String toString() {
		  return "Student [" + height + ", " + weight + "]";
	  }

    @Override
    public int compare(Student o1, Student o2) {
        if (o1.height > o2.height) {
            return 1;
        }
        // 같다면 0
        else if (o1.height == o2.height) {
            return 0;
        }
        // 작다면 음수
        else {
            return -1;
        }
    }
}
```
compare로 들어오는 두 개의 매개변수를 비교해 양수, 0, 음수를 반환한다. 위의 것은 Comparable에서 했던 것처럼 좀 더 간단하게 수정할 수 있다.    

```java
class Student implements Comparator<Student> {
    int height;
    int weight;

    Student(int height, int weight) {
        this.height = height;
        this.weight = weight;
    }

    @Override
	  public String toString() {
		  return "Student [" + height + ", " + weight + "]";
	  }

    @Override
    public int compare(Student o1, Student o2) {
        return o1.height - o2.height;
    }
}
```    

Comparator는    
- Arrays.sort()    
- Collections.sort()   

에 사용될 수 있다.    

그런데 이렇게 정렬하고자 할 때 Student라는 클래스에 compare가 들어가게 되면 비교를 위해서는 항상 비교를 위한 Student객체가 필요한 것이다. 그러나 비교는 일회성이고 Student 객체를 하나 꼭 두는 것이 아닌 Comparator를 구현하는 익명객체를 하나 생성하는 것이 훨씬 간단하다.    

Arrays.sort와 Collections.sort는 둘 다 두 번째 매개변수에 Comparator가 들어갈 수 있도록 만들어진 메소드가 있으다.    

sort()에는 정렬하고자 하는 array 또는 list가 첫 번째 매개변수로 들어가고, 두 번째 매개변수는 __익명 객체 구현으로 Comparator Interface__ 가 들어가면 된다.    

```java
public class Test {
    public static void main(String[] args) {
        Comparator<Student> comp = new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                // TODO Auto-generated method stub
                return o1.height - o2.height;
            }
        };
        
        List<Student> sList = new ArrayList<>();

        sList.add(new Student(170, 58));
        sList.add(new Student(163, 59));

        Collections.sort(sList, comp);

        for(Student s : sList) {
			    System.out.println(s);
		    }
    }
}
class Student {
    int height;
    int weight;

    Student(int height, int weight) {
        this.height = height;
        this.weight = weight;
    }
}
```    

이런 익명 객체 구현은 여러 정보로 비교하고싶을때 유용하다. 신장이 아닌 몸무게로 비교하고 싶을 때는 하나의 익명 객체를 더 생성해서 o1.weight - o2.weight를 반환하도록 작성하기만 하면 된다.    

<br>

이렇게 Comparable과 Comparator를 알아봤고 Java는 기본적으로 오름차순 정렬이다. 만약 내림차순으로 정렬하고싶다면 Comparator의 compare에서 o1- o2 를 o2 - o1로 바꿔주면 된다.    

왜냐하면 오름차순이란 작은 수가 앞에 위치하는 것이므로 o1 - o2의 값이 음수가 나와야 바뀌지 않는 것이고 양수가 나오면 바뀌는 것이다. 따라서 내림차순으로 정렬하고싶으면 두 개를 바꿔주면 되는 것이다.   

