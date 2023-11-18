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

## forEach, map, reduce, filter, every, some

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

```javascript
const numbers = [1, 3, 5, 4];
const isAllOdd = numbers.every(e => e % 2);
const isSomeOdd = numbers.some(e => e % 2);
console.log(isAllOdd, isSomeOdd); // false true
```
5. every는 모든 조건을 만족해야 true를 리턴합니다.
6. some은 하나의 조건만 만족하면 true를 리턴합니다

## find, findIndex, includes

```javascript
const condition = e => e.money >= 10000;
const persons = [
    {"name": "a", "money" : 1000},
    {"name": "b", "money" : 5000},
    {"name": "c", "money" : 10000},
    {"name": "d", "money" : 20000}
]
const rich = persons.find(condition);
console.log(rich); // {"name": "c", "money" : 10000}
const richIndex = persons.findIndex(condition);
console.log(richIndex); // 2
```
위 코드 결과처럼 find, findIndex 모두 배열에서 조건에 해당하는 요소를 발견한다면 요소를 반환하고 종료한다는 특징이 있습니다.

```javascript
const a = new Array();
a.push(1, 2, 3, 4, 5);
console.log(a.includes(3)); // true

const result = a.findIndex(e => e === 3);
console.log(result); // 2
```
includes는 ES7문법이며 **배열에 어떠한 요소가 있는지 확인**하는 함수이다. 베열에 어떤 요소가 있는지 없는지만을 확인한다면 includes를 사용하며 반환값은 true false 입니다. 

어떤 요소를 찾고 그 해당 인덱스를 반환해야 한다면 indexOf / findIndex를 사용합니다. findIndex가 indexOf보다 더 빠르다는 장점이 있으므로 findIndex의 사용을 권장합니다.

```javascript
const a = [1, 2, 3, 4, 5]
const result = a.findIndex(e => e === 3);
console.log(result) // 2
```

## 구문 생략, spread 연산자
### 구문 생략
```javascript
const name = "진양철";
const job = "회장";
const age = "58";
const data_used_ES6 = {name, job, age}
const data_not_used_ES6 = {"name": name, "job": job, "age": age}
console.log(data_used_ES6); // {name: '진양철', job: '회장', age: '58'}
console.log(data_not_used_ES6); // {name: '진양철', job: '회장', age: '58'}
```
위의 출력 결과는 동일하지만 구문 생략을 통해 쉽게 객체를 정의할 수 있습니다.

### spread 연산자
1. rest 매개변수

```javascript
const result_1 = (first, ...rest) => {
    console.log(...rest);
}
result_1(1, 2, 3); // 2 3

const value_1 = [1, 2, 3];
const result_2 = (a, b, c) => console.log(a, b, c);
result_2(...value_1); // 1 2 3

const value_2 = [1, 2, 3, 4, 5];
const [first, ...rest] = value_2;
console.log(first, rest); // 1, [2, 3, 4, 5]
```
1. result_1 **함수의 매개변수를 담는 용도**로 사용. first를 제외한 나머지를 배열로 담을 수 있습니다.
2. 배열 value_1을 분해해서 각각 a, b, c로 담을 수 있습니다.
3. **배열의 나머지 것들을 쉽게 처리할 때 사용**. rest에는 first를 제외한 나머지 변수들이 담겨있습니다.

2. 배열 통합

```javascript
const first = [1, 2, 3];
const second = [4, 5, 6];
const third = [...first, ...second];
console.log(third); // [1, 2, 3, 4, 5, 6]
```
두개 이상의 배열을 합치는 방법은 concat()메서드도 존재합니다. 하지만 spread 연산자를 통해 first와 second를 분해해서 배열에 순수 요소들로 들어가게 해서 배열을 합치는 방법도 존재합니다.

3. Max 함수 매개변수로 집어넣기

```javascript
const arr = [1, 2, 3, 4];
const result = Math.max(...arr);
console.log(result); // 4
```
spread 연산자를 응용하여 Math.max()에 사용할 수 있습니다. spread 연산자를 통해 순수 요소들로 분해하여 그 중 최댓값을 뽑아내는 것입니다. 이외에 Math.min()에도 응용 가능합니다.

4. 객체 복사

```javascript
const before = {"name": "진양철", "age": "58"};
const after = {...before, "job": "회장"};
console.log(after); // {name: '진양철', age: '58', job: '회장'}
```
객체 안에 있는 값들을 순수 key와 value로 분해하고 직접 복사를 통해 다시 새로운 객체에 할당할 수 있습니다. 하지만 객체의 깊이가 1단계인 경우에 한해서만 가능합니다.


**[Reference]** 실시간 모니터링 시스템을 만들며 정복하는 MEVN
{: .notice--info}