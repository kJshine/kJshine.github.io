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
<br/>
<br/>
<br/>
또한 화살표함수로 setTimeout 을 선언하면 그 당시 this가 함수호출 패턴에 의해 결정되는 것을 막을 수 있습니다.

예시
```javascript
function arrow(){
    setTimeout(()=>{
        console.log(this); // arrow {}
    }, 1000)
}

function not_arrow(){
    setTimeout(function(){
        console.log(this); // Node.js에서는 Timeout || 브라우저에서는 Window
    }, 1000)
}

const p1 = new not_arrow();
const p2 = new arrow();
```

위처럼 화살표 함수로 setTimeout함수를 정의한다면 화살표 함수에서의 this가 그 위의 생성자함수를 가리킬 수 있습니다.

## forEach, map, reduce, filter

```javascript
const arr = new Array();
arr.push(1, 2, 3, 4, 5);

const func1 = (e, index) => {
    console.log(`${index}번째 요소는 ${e}입니다.`);
}

const func2 = (e, index) => e * 2;
const func3 = (prev, curr, index) => prev + curr;
const func4 = e => e % 2;
const a = arr.forEach(func1);
/*
0번째 요소는 1입니다.
1번째 요소는 2입니다.
2번째 요소는 3입니다.
3번째 요소는 4입니다.
4번째 요소는 5입니다.
*/
console.log(a); // undefined
const b = arr.map(func2);
console.log(b); // [2, 4, 6, 8, 10]
const c = arr.reduce(func3);
console.log(c); // 15
const d = arr.filter(func4);
console.log(d); // [1, 3, 5]
```

1. forEach: 배열에서 그 안에 있는 요소를 이용하여 기능을 구현할 때 사용. 반환값이 없다.
2. map: 배열을 이용해서 **새로운** 배열을 만들 때 사용. 새로운 배열을 반환
3. filter: 배열을 이용해 **조건**에 맞는 원소로 배열을 만들 때 사용. 추출만 가능하고 원소를 변화시킬 순 없음
4. reduce: 배열을 통해 **하나의 계산된 값**을 추출해낼 때 사용. 반환값이 존재

**[Reference]** 실시간 모니터링 시스템을 만들며 정복하는 MEVN
{: .notice--info}