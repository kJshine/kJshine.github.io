---
layout: single
title:  "쓰면서 공부하는 자바스크립트"
categories: javascript
tag: [Javascript, ES6]
author_profile: false
---

이 포스터는 제가 자바스크립트를 사용하면서 제대로 알지 못하고 사용했던 것들과 새로 배운 지식, 또 잊지 않기 위해 여러번 보려고 만들었습니다!   
작성하고 싶은게 있거나 좋은 정보가 있다면 계속 업데이트해 공유할 예정입니다

# Javascript

## 화살표 함수
화살표 함수는 다른 함수와 여러가지가 다른점이 있습니다. 생성자함수로 사용할 수 없고, arguments를 지원하지 않는다는 특징이 있습니다. (arguments 가 무엇인지 추후 업데이트)

```javascript
function ES5(){
    return 1;
}

const ES6 = () => 1

console.log(ES5());
console.log(ES6());
/*
1
1
*/
```

두 함수는 같은 역할을 합니다. 하지만 화살표함수는 function과 return이 사라지고 화살표만 남게된다는 차이가 있습니다. 한 줄짜리 함수의 작성에서 좀더 간결하게 표현이 가능한 장점이 있습니다.

```javascript
const ES6 = () => {
    // 추가 로직
    return 1;
}
```

한 줄이상인 코드의 경우는 중괄호 안에 로직을 구현하고 반환할 값을 return 해주시면 됩니다. 이렇게 함수의 끝에 return [값]으로 하는 것이 좋다고 합니다. 추후 디버깅, 메서드체이닝이나 함수합성을 할 때 편리하다는 장점이 있습니다.

