# 📖Weekly Paper - Week 6

# 🔍Q1.
- 🇶1. 예시의 코드를 실행할 때, 콘솔에 출력될 값과 그 이유를 설명해 주세요.
```js
// 1번
let num = 1;

// 2번
setTimeout(() => {
  num = 2;
}, 0);

// 3번
num = 3;

// 4번
console.log(num);
```
결과: 3
과정: 
1번에서 변수 num에 1이 저장
2번에서 setTimeout을 호출하여 콜백 함수인 num = 2;가 비동기적으로 실행되어 이벤트 루프에 의해 Macrotask 큐로 이동
3번에서 num의 값이 3으로 변경
4번에서 현재 num의 값인 3이 출력
이후에 콜 스택 값이 비었으므로 num의 값이 2로 변경

### 2. 이벤트 루프
- **비동기** 코드가 실행되는 방식 관리
- 콜 스택이 **비었을 때**만 비동기 코드 실행 O
- Task 큐와 Microtask 큐 관리

📌 **이벤트 루프** 실행 순서
1️⃣ 콜 스택 실행 (동기 코드) 
2️⃣ Microtask 큐 (주로 `Promise`)
3️⃣ Macrotask 큐 (주로 `setTimeout`, `setInterval`)
→ `setTimeout`의 지연 시간은 최소 시간만 보장

# 🔍Q2.
- 🇶2. AJAX에 대해 설명해 주세요.
