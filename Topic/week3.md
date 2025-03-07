# 🔍Q1.
- Q1. 자바스크립트에서 ==와 ===가 어떻게 다른지 설명해 주세요.

## 차이
- '==' 연산자는 서로 다른 유형의 두 변수의 [값] 비교
- '===' 연산자는 엄격한 비교(값과 나입 모두 일치해야 true 반환)

```javascript
0 == false // true
0 === false // false
```
- 위와 같이 0의 자료형은 number이고, false의 자료형은 boolean이기에 서로 다름

1) null과 undefined의 비교 값은?
```javascript
null == undefined // true
null === undefined // false
```
- null의 자료형은 object, undefined의 자료형은 undefined로 서로 다름

2) !=과 !==도 다를까?
```javascript
0 != false // false
0 !== false // true
```
- ==과 ===의 비교 값과 정반대의 값을 도출

3) NaN을 비교하면?
- Not a number은 어떤 것과도 같지 않음.

## 결론
- 변수 비교 시 '===' 연산자 사용 권장
- 가능한 '==' 연산자를 사용 X 
- 직접 자료형을 변환하여 코드 가독성 향상

<hr>

# 🔍Q2.
- Q2. 자바스크립트에서 얕은 복사(Shallow Copy)와 깊은 복사(Deep Copy)에 대해 설명해 주세요.

## JS의 데이터 타입
- 원시값: 기본 자료형
    - Number
    - String
    - Boolean
    - Null
    - Undefined
- 참조값
    - Object
    - Symbol

## 얕은 복사 
- 객체의 참조값(주소)을 복사
- 객체를 복사할 때 기존 값과 복사된 값이 같은 참조를 가리키고 있는 것
- 객체 안에 객체가 있을 경우 한 개의 객체라도 기존 변수의 객체를 참조하는 것

```javascript
let x = { name: '전유진' }
let y = x; 
y.birth = 2017; // x === y
```
- 얕은 복사: 참조값 복사 시 변수가 객체 참조를 가리켜 복사된 변수 또한 메모리 공간의 참조를 가리킴. -> 복사 후 객체 수정 시 동일한 참조를 가리켜 기존 변수에 영향 O

### 얕은 복사 방법
1. Array.prototype.slice()
- 대표적 예로, 기존 배열에서 추출하여 새 배열 리턴하는 메소드
- start와 end 미설정 시 기존 배열 전체 얕은 복사

예시1
```javascript
const example = [1, '이', "3"];
const copy = example.slice();

console.log(JSON.stringify(example) === JSON.stringify(copy)); // true
copy.push(4);
console.log(JSON.stringify(example) === JSON.stringify(copy)); // false

console.log(example); // [1, '이', "3"]
console.log(copy); // [1, '이', "3", 4] 
```
- 기본 배열에 영향을 끼치지 않아 깊은 복사로 보이지만, 원시값을 저장한 1차원 배열일 뿐 배열은 Object 타입으로 배열 내부 요소들이 객체일 경우 같은 메모리 주소 가리킴.

예시2
```javascript
const example2 = [
    {
        a: 1,
        b: 2,
    },
    true,
];
const copy = example2.slice();

console.log(JSON.stringify(example2) === JSON.stringify(copy)); // true

copy[0].a = 100;
copy[1] = false;

console.log(example2); // [ { a: 100, b: 2 }, true ] 
console.log(copy);  // [ { a: 100, b: 2 }, false ]
```
- 배열 내부 요소들이 객체(obj)이기 때문에 동일한 메모리 주소를 가리켜 복사한 변수 값 변경 시 원본에도 영향 O
- 두번째 값인 boolean형은 원시값이기 때문에 원본에 영향 X

2. Object.assign()
- 사용: Object.assing({}, obj1);
- 메소드의 첫 인자로 빈 객체 넣어주고 두 번째 인자로 복사할 객체 넣기

```javascript
const obj1 = {
    a: 'a',
    number: {
        one: 1,
        two: 2,
    },
};
const copy = Object.assign({}, obj1);

copy.number.one = 3;

console.log(obj1 === copy); // false
console.log(obj1.number.one === copy.number.one); // true
```
- 두 객체의 내용은 같지만 서로 다른 객체이므로 copy.a = 'b';를 하면 obj1.a = 'a';로 그대로
- 객체 안의 객체는 동일한 주소를 가리키므로 원본과 복사본이 동일하게 변경됨.

3. Spread 연산자(전개 연산자)
- Spread 연산자 (...): 배열, 객체 등의 요소를 개별적으로 풀어서(전개해서) 복사하거나 전달할 때 사용하는 문법
```javascript
const arr = [1, 2, 3];
console.log(...arr); // 1 2 3 
```

```javascript
const obj2 = {
    a: 'a',
    number: {
        one: 1,
        two: 2,
    },
};
const copy = {...obj2};
copy.number.one = 3;

console.log(obj2 === copy); // false
console.log(obj2.number.one === copy.number.one); // true
```
- 마찬가지로 얕은 복사이다~

## 깊은 복사 
- 객체의 실제 값 복사
- 깊은 복사: 객체 안에 객체가 있는 경우에도 원본과의 참조가 완전히 끊어진 객체를 뜻함

```javascript
let x = 3;
let y = x;
y=5;
// x = 3, y = 5
```
- 깊은 복사: 원시 값을 복사할 때 독립적 메모리 공간에 할당하기 때문에, 복사 후 값 수정하여도 기존 변수 영향 X 

### 깊은 복사 방법
1. JSON.parse && JSON.stringify
- JSON.stringify()는 객체를 json 문자열로 변환하는데, 이 과정에서 원본 객체와의 참조가 모두 끊어짐
- 문자열 변환 후 JSON.parse()로 다시 원래 객체로 되돌려줌
- 간단하고 쉽지만 느린 편 / 객체가 function인 경우 undefined로 처리

```js
const obj = {
    a: 'a',
    number: {
        one: 1,
        two: 2,
    },
    arr: [1, 2, [3, 4]],
};
const copy = JSON.parse(JSON.stringify(obj));

copy.number.one = 3;
copy.arr[2].push(5);

console.log(obj === copy); // false
console.log(obj.number.one === copy.number.one); // false
console.log(obj.arr === copy.arr); // false

console.log(obj); // { a: 'a', number: { one: 1, two: 2, }, arr: [1, 2, [3, 4]] }
console.log(copy); // { a: 'a', number: { one: 3, two: 2, }, arr: [1, 2, [3, 4, 5]] }
```

2. 재귀 함수를 구현한 복사
- 복잡함

```js
const object = {  
    a: "a",  
    number: {    
        one: 1,    
        two: 2,  
    },  
    arr: [1, 2, [3, 4]],
}; 
function deepCopy(object) {  
    if (object === null || typeof object !== "object") { // 깊은 복사가 필요없는 대상
        return object;  
    } 
    const copy = Array.isArray(object) ? [] : {};  // 객체인지 배열인지 판단 후 복사본 생성

    for (let key of Object.keys(object)) { // 재귀 호출로 객체 내부 요소까지 깊은 복사
    copy[key] = deepCopy(object[key]);  
    }       
    return copy;
} 
const copy = deepCopy(object); 

copy.number.one = 3;
copy.arr[2].push(5); 

console.log(object === copy); // false
console.log(object.number.one === copy.number.one); // false 
console.log(object.arr === copy.arr); // false 
console.log(object); // { a: 'a', number: { one: 1, two: 2 }, arr: [ 1, 2, [ 3, 4 ] ] }
console.log(copy); // { a: 'a', number: { one: 3, two: 2 }, arr: [ 1, 2, [ 3, 4, 5 ] ] }
```

3. Lodash 라이브러리 사용
- 라이브러리 사용 시 더 쉽고 안전하게 깊은 복사 가능
- 일반적인 개발에는 효율적이지만 코테에는 사용 X
- 라이브러리를 설치해야한다는 단점

```js
const deepCopy = require("lodash.clonedeep");

const obj = {
    a: 'a',
    number: {
        one: 1,
        two: 2,
    },
    arr: [1, 2, [3, 4]],
};
const copy = deepCopy(obj);

copy.number.one = 3;
copy.arr[2].push(5);

console.log(obj === copy); // false
console.log(obj.number.one === copy.number.one); // false
console.log(obj.arr === copy.arr); // false
console.log(obj); // { a: 'a', number: { one: 1, two: 2 }, arr: [ 1, 2, [ 3, 4 ] ] }
console.log(copy); // { a: 'a', number: { one: 3, two: 2 }, arr: [ 1, 2, [ 3, 4, 5 ] ] }
```

### 결론
- 복사본을 변경하는 경우에 원본이 변경된다면 코드의 흐름을 방해할 수 있기 때문에 깊은 복사를 습관화하고 얕은 복사를 방지하기 위해 의식해야 함!
- 코딩테스트나 라이브러리 설치가 어려운 경우가 아닌 이상 깊은 복사를 할 때에는 lodash를 사용하는 것이 쉬움.

### 참고 자료
- https://velog.io/@filoscoder/-%EC%99%80-%EC%9D%98-%EC%B0%A8%EC%9D%B4-oak1091tes
- https://bbangson.tistory.com/78