---
layout: single
title:  "Dart) 함수형"
categories: dart
tag: [dart, flutter]
author_profile: false
---

**[참고영상]** [노마드코더) Dart 시작하기](https://nomadcoders.co/)
{: .notice--info}

## 함수형

### Defining a Function

sayHello에 넘겨주는 순서가 바뀌어도 named 파라미터를 넣게 되므로
파라미터의 순서는 이제 더이상 중요하지 않다.

- void function( ){ } : 함수명 앞에 붙은 void는 이 함수가 아무것도 return하지 않는다는 의미이다.

ex1) 
```dart
void sayHello(String name){
  print('hello $name nice to meet you!');
}
void main() {
  sayHello('재환');
}

→ hello 재환 nice to meet you!
```

ex2)
```dart
String sayHello(String name){
  return 'hello $name nice to meet you!';
}

void main() {
  print(sayHello('재환'));
}

→ hello 재환 nice to meet you!
```

위처럼 함수가 실행되고, 함수안의 코드가 한줄이면서 곧바로 return하는 경우 return과 중괄호를 생략할 수 있다.

→ String sayHello(String name) => 'hello $name nice to meet you!';

위처럼 작성된 문법을 fat arrow syntax라고 부르고 곧바로 return 하는 거랑 같은 의미이다.

ex) num plus(num a, num b) ⇒ a + b;

### Named Parameters

- flutter에서 자주 사용되는 개념이다.

```dart
String sayHello(String name, int age, String country) =>
  'Hello $name, you are age $age, and you come from $country';

void main() {
  print(sayHello('재환', 29, '인천'));
}

→ Hello 재환, you are age 29, and you come from 인천
```

*age의 type을 num대신 int로 사용한 이유는 num은 double도 받을 수 있기 때문이다*

이런 문법이 있다고 가정햇을 떄, Named Parameters를 사용해야 가독성이 더 좋다.

1) 첫번째 방법(default value 설정)
```dart
String sayHello({
  String name = 'anon',
  int age = 99,
  String country = 'Incheon',
  }) {
  return 'Hello $name, you are age $age, and you come from $country';
}

void main() {
  print(sayHello(
    age: 29,
    country: 'cuba',
    name: '재환',
  ));
}
→ Hello 재환, you are age 29, and you come from cuba
```
1) sayHello 함수에 들어가는 파라미터에 중괄호로 한번 묶어 주어야 한다.

2) sayHello에 넘겨주는 순서가 바뀌어도 named 파라미터를 넣게 되므로
파라미터의 순서는 이제 더이상 중요하지 않다.

3) sayHello 함수에 default value를 설정해주지 않으면, null safety가 성립되지
않기 때문에 오류가 발생한다. 따라서 default value를 설정해주면 사용자가 파라미터를
보내지 않더라도 실행이 된다.

```dart
String sayHello({
  String name = 'anon',
  int age = 99,
  String country = 'Incheon',
  }) {
  return 'Hello $name, you are age $age, and you come from $country';
}

void main() {
  print(sayHello());
}
-> Hello anon, you are age 99, and you come from Incheon
```
2) 두번째 방법 (default value 설정 X)

- 함수안에 들어가는 변수 앞에 required modifier를 붙여 주어 다트에게 필수 파라미터라는 것을 알려준다.

```dart
String sayHello({
  required String name,
  required int age,
  required String country,
  }) {
  return 'Hello $name, you are age $age, and you come from $country';
}

void main() {
  print(sayHello(
  name: '재환',
  country: '인천',
  age: 29,
  ));
}
```
### Recap

parameter의 종류는 2가지: 1. positional parameter 2. named parameter 가 있다.

1. positional parameter는 순서가 중요하다. (각각의 위치에 맞게 전달해야함)
2. named parameter는 파라미터를 중괄호로 감싸주면 된다. (위치에 상관없이 전달 가능)

그리고 공통적으로 null safety를 해결해줘야 한다. 방법은 2가지인데 첫번째는

1. 파라미터앞에 required modifier를 적용하는 것이다. 파라미터 앞에
required를 붙여주면 된다.
2. 파라미터에 default value를 설정해주는 것이다. 그러면 호출할 때
파라미터가 없어도 default value로 대체가능하기 때문이다.

### Optional Positional Parameters

required modifier 대신에 사용할 수 있는 방법이다.

```dart
String sayHello(
  String name,
  int age,
  [String? country = '인천']
) => 'Hello $name, you are $age years old from $country';

void main() {
  sayHello(
    '재환',
    29,
  );
}
```
위처럼 String 뒤에 ?를 붙여서 country 는 not required라고 알려주고,
defalut value를 부여해주는 것이다.

자주 사용하는 개념은 아니다.

### QQ Operator

여러 종류가 있지만,  ?? 와 ??= 를 알아보자.

1. ??
입력받은 이름을 대문자로 변환하는 함수를 호출한다고 가정한다.

```dart
String capitalizeName(String name) => name.toUpperCase();

void main(){
  print(capitalizeName('jaehwan'));
}
```
이런 단순한 코드에서 name이 null인 경우에도 작동시키고 싶다면
첫번째 방법으로는

```dart
String capitalizeName(String? name) {
  if(name != null){
    return name.toUpperCase();
  }
  return 'ANON';
}

void main(){
  print(capitalizeName(null));
}
```
이런 식으로 String 뒤에 ?를 붙이고 if문으로 각각의 경우를 return해줘야 한다.
여기서 fat arrow를 사용하면 좀더 간결하게 바꿔줄 수 있다.

```dart
String capitalizeName(String? name) => name != null ? name.toUpperCase() : 'ANON';

void main(){
  print(capitalizeName('jaehwan'));
}
```
이제 여기서 QQ operator를 사용한다면 한번더 줄일 수 있다.
```dart
String capitalizeName(String? name) => name?.toUpperCase() ?? 'ANON';

void main(){
  print(capitalizeName('jaehwan'));
}
```
여기서 ??는 좌항이 null이면 우항을 return하는 것이고, null이 아니라면 그대로 좌항을
return한다는 문장이다.

그리고 name?.toUpperCase() 에서 name뒤에 ?를 해준 이유는 name값이 null일 경우
toUpperCase()를 호출할 수 없기 때문에 name이 null이 아닐경우 호출한다는 문장이다.

1. ??=

??와 비슷한 역할을 하지만 차이점이 있다면
??=연산자는 변수 안에 값이 null일 때를 체크해서 값을 할당할 수 있다는 점이다.

```dart
void main() {
  String? name;
  name ??= 'nico';
  name ??= 'another';
  print(name);
}
```
### Typedef

typedef는 자료형에 alias(별명)을 붙일 수 있게 해준다.

```dart
List<int> reverseListOfNumbers(List<int> list) {
  var reversed = list.reversed;
  return reversed.toList();
}

void main() {}
```
이런 코드가 있다고 가정했을 때 integer List를 전달받아서 integer List를
return하는 코드가 있을 때
integer List의 alias를 만드는 방법은

ListOfInts라는 typedef를 선언해주면 된다.

```dart
typedef ListOfInts = List<int>;

ListOfInts reverseListOfNumbers(ListOfInts list) {
  var reversed = list.reversed;
  return reversed.toList();
}

void main() {
  print(reverseListOfNumbers([1,2,3,4,]));
}
```
또 두번째로는 Map같은 것도 typedef를 선언해줄 수 있다.

```dart
typedef UserInfo = Map<String, String>;

String sayHi(UserInfo userInfo) {
  return "Hi ${userInfo['name']}";
}

void main() {
  print(sayHi({'name': '재환'}));
}
```