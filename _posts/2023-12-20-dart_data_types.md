---
layout: single
title:  "Dart) 자료형"
categories: dart
tag: [dart, flutter]
author_profile: false
---



**[참고영상]** [노마드코더) Dart 시작하기](https://nomadcoders.co/)
{: .notice--info}

## 자료형(Data types)

### Basic Data Types

- String - 정의할 때 큰 따옴표, 작은 따옴표 둘 다 사용가능하다.
- bool - true, false
- int - 숫자, num 클래스로부터 상속받는다.
- double - 숫자 끝에 소수점을 붙일 수 있다. num 클래스로부터 상속받는다
- num - 정수형, 소수점 둘 다 사용가능하다. 자주 사용하지는 않는다.

위 자료형 모두 object, class로 이루어져 있다. 때문에 자동완성 되는 메소드들을 보면서 사용할 수 있다.

### Lists

flutter에서 자주 사용된다. ex) List<int> : 정수형으로 이루어진 리스트

```dart
void main(){
  List<int> numbers = [1, 2, 3, 4];
  numbers.add(2);
  print(numbers);
}
```

→ [1, 2, 3, 4, 2]

하지만 var의 사용이 좀 더 권장되므로

```dart
void main(){
  var numbers = [1, 2, 3, 4];
  numbers.add(2);
  print(numbers);
}
```
가 좋다.

numbers.first; -> 리스트의 첫번째 요소   
numbers.last; -> 리스트의 마지막 요소 *리스트의 갯수가 몇개인지 모를 때 사용할 수있다*   
numbers.inEmpty -> 리스트가 비어있는지 알 수 있다.   
numbers.add() -> 리스트에 새로운 하나의 요소를 추가할 수 있다.   
numbers.addAll() -> 리스트에 한꺼번에 여러 요소를 추가할 수 있다.   
numbers.clear() -> 리스트의 요소를 전부 없앨 수 있다.   
numbers.contains() -> 리스트가 특정 요소를 가지고 있는지 알아낼 수 있다.   

등등 여러가지 메소드가 존재한다.

그리고 리스트를 작성할 때 var numbers = [1,2,3,4,]; 처럼 요소의 마지막에 쉼표를 넣고

포맷을 하면

```dart
void main() {
  var giveMeFive = true;
  var numbers = [
    1,
    2,
    3,
    4,
  ];
}
```
처럼 가독성이 좋게 포맷이 된다.

리스트의 장점: collection if와 collection for를 지원한다.

ex) 

```dart
void main() {
  var giveMeFive = true;
  var numbers = [
    1,
    2,
    3,
    4,
    if (giveMeFive) 5,
  ];
}
```
위 코드는 giveMeFive가 true면 5요소를 추가한다는 의미이다.

```dart
void main() {
  var giveMeFive = true;
  var numbers = [
    1,
    2,
    3,
    4,
  ];
  if(giveMeFive) {
    numbers.add(5);
  }
}
```

의 문장을 좀 더 간결하고 가독성 좋게 표현한 것이다.

### String Interpolation

- String Interpo;ation은 text에 변수를 추가하는 방법이다.

```dart
void main() {
  var name = '재환';
  var greeting = 'hello everyone, my name is $name';
  print(greeting);
}
```
→ hello everyone, my name is 재환

계산을 해서 추가하고 싶다면,

```dart
void main() {
  var name = '재환';
  var age = 29;
  var greeting = "hello everyone, my name is $name, and I'm ${age + 1}";
  print(greeting);
}
```

> hello everyone, my name is 재환, and I'm 30

위처럼 달러 뒤에 { }를 붙여서 계산해 주면 된다.

- 'hello everyone, my name is $name, and I\'m ${age + 2}';
여기서 I'm 부분의 소따옴표 때문에 문장이 끝나는데 이 부분은 따옴표 앞에
\기호를 붙여주면 해결할 수 있다.

### Colllection For

```dart
void main() {
  var oldFriends = [
    'nico',
    'lynn',
  ];
  var newFriends = [
    'lewis',
    'ralph',
    'darren',
    for(var friend in oldFriends) "💝 $friend",
  ];
  print(newFriends);
}
```

→ [lewis, ralph, darren, 💝 nico, 💝 lynn]

### Maps

- Map은 자바스크립트와 타입스크립트의 object, python의 dictionary의 개념과 같다.
- dart에서의 object는 typescript의 any와 같다.

List로 이루어진 Map

```dart
void main() {
  Map<List<int>, bool> player = {
    [1, 2, 3, 4]: false,
  };
}
```

Map으로 이루어진 List

```dart
void main() {
  List<Map<String, Object>> players = [
    {'name': 'nico', 'xp': 199993.999},
    {'name': 'nico', 'xp': 199993.999},
  ];
}
```

자바스크립트와 타입스크립트의 object, python의 dictionary를 만드는 방식으로 사용할 것이라면

Map은 많이 사용하지 않는 것이 좋다. key와 value로 이루어진 것을 정의할 때는 class를 사용하는 것이 좋다.

### Sets

- 리스트와 비슷하지만 다르다.

```dart
void main() {
  var numbers = {1, 2, 3, 4};
  numbers.add(5);
  numbers.add(5);
  numbers.add(5);
  numbers.add(5);
  print(numbers);
}
```

→ {1, 2, 3, 4, 5}

위 코드처럼 5를 아무리 추가해도, set에서는 유니크한 요소가 하나씩만 존재해야 하므로 5는 하나만 추가된다.

요소가 항상 하나씩만 있어야 되면 Set을 사용하고, unique할 필요가 없다면 List를 사용하면 된다.
