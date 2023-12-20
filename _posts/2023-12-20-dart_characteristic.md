---
layout: single
title:  "Dart) 특징과 변수형"
categories: dart
tag: [dart, flutter]
author_profile: false
---



**[참고영상]** [노마드코더) Dart 시작하기](https://nomadcoders.co/)
{: .notice--info}

## **특징**

객체 지향 언어이다.

자바스크립트와의 차이점

1. 정적 타입 시스템
2. 클래스 기반 상속
3. 비동기 프로그래밍
4. 가비지 컬렉션
5. 라이브러리 생태계

1. 다트는  크로스 플랫폼 앱을 만드는데에 사용된다.
- 크로스 플랫폼 앱은 여러 플랫폼(운영 체제)에서 동작하는 애플리케이션을 의미합니다. 일반적으로 모바일 앱 개발에서 사용되며, 특정 플랫폼에 종속되지 않고 여러 플랫폼에서 실행될 수 있도록 설계되는 앱을 말합니다.
- 전통적으로 모바일 앱 개발은 안드로이드와 IOS 두 가지 주요 플랫폼을 대상으로 개발되었습니다. 그러나 안드로이드와 IOS는 서로 다른 운영체제이며, 각각의 플랫폼에는 고유한 개발 환경과 언어가 있습니다. 따라서 각 플랫폼에 맞게 개발된 앱은 해당 플랫폼에서만  실행됩니다.
- 크로스 플랫폼 앱은 이러한 플랫폼 간의 차이를 극복하기 위해 설계되었습니다. 하나의 코드베이스를 사용하여 여러 플랫폼에서 실행될 수 있도록 개발되며, 플랫폼별로 필요한 코드의 일부를 조정하여 각 플랫폼에 맞게 컴파일 또는 변환됩니다. 이를 통해 앱 개발자는 개발 비용과 시간을 줄이고, 여러 플랫폼에 대한 일관된 경험을 제공할 수 있습니다.
- 크로스 플랫폼 앱 개발 도구와 프레임워크에는 React Native, Flutter, Xamarin, Ionic 등이 있습니다. 이러한 도구를 사용하면 개발자는 하나의 코드베이스로 안드로이드와 IOS앱을 개발할 수 있으며, 필요한 경우 특정 플랫폼에 맞는 기능을 추가할 수 있습니다.

1. 다트는 2개의 컴파일러를 가진다.
- dart web: dart → javascript // dart native : dart → 기계어

1. JIT and AOT
- Just in time 과 Ahead of Time
- just-in-time 컴파일러는 dart VM을 사용하는데, 코드의 결과를 바로 화면에 보여준다. 하지만 오래걸리므로, FLUTTER로 개발하는 중일 때 사용한다.
- ahead-of-time은 개발이 끝난 후 앱을 배포할 때 사용한다. 다른 CPU 아키텍처에 맞추어서 빠른 기계어, 컴파일된 바이너리를 만들 수 있다.

⇒ 개발할 때는 빠른 피드백을 받을 수 있고, 배포할 때는 기계어로 컴파일이 가능하므로 두가지 다 가능 한게 장점이다.

## 변수형

### hello world

- 코드는 main 함수 안에 들어가야 한다.
- 자바스크립트와 다르게 세미콜론을 꼭 달아주어야 한다.

```dart
void main(){
    print("hello world");
}
```

### The Var Keyword

- 타입을 정한 변수는, 다른 타입으로 바꿀 수 없다.
- 선언할 때 `var name = “재환”` 혹은 `String name = “재환”` 처럼 선언할 때 타입을 지정할 수 있다.
- 하지만 함수 안에서 지역변수를 선언하거나, 메소드 안에서 지역변수를 선언하는 상황이라면 var를 사용하는게 dart 스타일의 권장 방식이다.

### Dynamic Type

- 여러가지 타입을 가질 수 있는 변수에 쓰이는 키워드이다.
- 필요한 이유는 변수가 어떤 타입일지 알기 어려운 경우에 사용한다.
- 하지만 보통은 권장되지 않는 타입이다.

### Nullable Variables

- null safety란 개발자가 null값을 참조할 수 없도록 한다.

```dart
String jaehwan = '재환'
if (jaehwan != null) {

}
```

이라는 if조건문이 있는데 기본적으로 모든 변수는 non-nullable이기 때문에 null이 될 수 없다. null이 될 수 없는데 null로 조건을 걸어주었기 때문에 오류가 생긴다.

- 따라서 타입 뒤에 ?를 붙여주면 변수가 null값이 될 수 있다는걸 암시해주므로

```dart
String? jaehwan = '재환'
if (jaehwan != null)  {
    jaehwan.isNotEmpty;
}
```

위 식을 바꿔서

jaehwan?,isNotEmpty 즉, jaehwan이 null이 아니라면 isNotEmpty속성을 요청한다.

### Final Variables

- var 대신 final을 쓰면 자바스크립트의 const처럼 수정할 수 없다.
- `var name = “재환”;` → `final name = “재환”;`
- `final String name = “재환”` 이렇게도 작성이 가능하지만 필수는 아니다.

### Late Variables

- late는 final이나 var앞에 붙여줄 수 있는 수식어이다.
- 초기 데이터 없이 변수를 선언할 때 사용한다.
- 장점은 실수를 막아준다는 점이다. 예를 들어 값을 넣기전까지는 print가 안된다. → 접근이 안됨

### Constant Variables

- 다트의 const라고 볼 수 있지만, 자바스크립트의 const와는 다르다.
- 다트의 const는 compile-time constant를 만든다.
- 처음 컴파일 되었을 때 값을 알 수 있는 상수라는 뜻으로, 이것은 API요청을 받아서 변수에 그 값을 집어넣는 작업이 불가능하다. API요청 전까지는 데이터의 값을 모르기때문이다.
- 즉 사용자가 화면에서 입력해야 하는 값은 final이나 var를 사용해야한다. 앱에서 사용할 상수가 있다면 const를 사용하면 된다. ex) `max_allowed_price = 120;`
- *const 변수들은 컴파일 때 평가된다.* = 앱에 답긴 코드를 앱스토어에 보내기 전

### Recap

- dart의 스타일 가이드에 따르면 var를 가능한 한 많이 사용하는게 권장된다.
- type을 사용하는 방식은 class의 property를 작성할 때 사용하는게 권장된다.
- dynamic은 보통 자주 사용하는건 좋지 않다.
