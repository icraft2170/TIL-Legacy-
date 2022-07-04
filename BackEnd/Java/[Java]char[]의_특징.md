---

title: char[]의 
date:2021-05-25
author: 손현호

---

# char[]

```java
		int[] intArray = { 3, 15, 5, 3,};
		double[] doubleArray = { 3.14,1.29,0.0 };
		char[] chArray = { 'H','E','L','L','O' };
		
		System.out.println(intArray);
		System.out.println(doubleArray);
		System.out.println(chArray);
```
>[I@5ca881b5  
>[D@24d46ca6  
>HELLO
 
<br/>

`Java`에서 배열을 선언한 변수를 출력하면 위와 같이  
`(자료형)@(해시코드)` 의 형태로 출력된다. 이유는 배열의 이름은 배열을 다루는데 필요한 참조변수이기 때문이다. 배열의 이름에는 배열이 위치하고 있는 메모리의 주소를 저장하고 있어 배열의 이름 출력시 주소 값이 나오는 것이다.

</br>

그런데, 값을 보면 `HELLO`만 주소 값이 아닌 배열이 순서대로 출력된 걸 볼 수 있다. 이는 char 배열의 특징이라 할 수 있는데, char[]은 변수 명을 적어도 그 안에 내용을 출력한다.  
아마도, String 클래스가 내부적으로 char[]로 이루어져있어 그럴 수 도 있고. C언어에서는 문자열을 char[]로 이용하기 때문일 수 도 있다. (추측...)  

<br/>

그래서 char[]은 다른 배열들과 다르게 배열의 주소를 출력하는 것이 아니라 배열의 내용을 출력한다. 다만, chArray(변수명)가 배열의 내용을 담고 있다는 얘기는 아니다. 아마, Character 클래스에서 toString을 배열의 내용을 리턴하도록 오버라이드 되어있기 때문일 것으로 생각된다.
