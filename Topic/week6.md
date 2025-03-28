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
- AJAX: 웹 애플리케이션에서 페이지를 새로 고침하지 않고 서버와 비동기적으로 데이터를 주고받을 수 있는 기술
- 장점: 웹 애플리케이션이 훨씬 반응성이 좋아지고, 더 나은 사용자 경험 제공

## AJAX의 핵심 특징:
1. 비동기: 서버 요청을 보내고 응답을 기다리는 동안 다른 작업을 할 수 있습니다.
2. 서버와의 데이터 전송: 페이지를 새로 고침하지 않고 서버와 데이터를 주고받을 수 있습니다.
3. DOM 업데이트: 서버에서 받은 데이터를 바탕으로 웹 페이지를 동적으로 변경할 수 있습니다.

## 예시
### Javascript의 XMLHttpRequest 사용
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AJAX 예시</title>
</head>
<body>
  <h1>AJAX 예시</h1>
  <button onclick="fetchData()">데이터 가져오기</button>
  <div id="result"></div>

  <script>
    function fetchData() {
      var xhr = new XMLHttpRequest();  // XMLHttpRequest 객체 생성
      xhr.open("GET", "https://jsonplaceholder.typicode.com/posts/1", true);  // 서버 요청 준비 (GET 방식)
      
      // 요청이 완료되었을 때 처리할 콜백 함수 설정
      xhr.onload = function() {
        if (xhr.status >= 200 && xhr.status < 300) {  // 요청이 성공적으로 완료된 경우
          var response = JSON.parse(xhr.responseText);  // 서버에서 받은 JSON 데이터 파싱
          document.getElementById("result").innerHTML = 
            `<h2>${response.title}</h2><p>${response.body}</p>`;  // 받은 데이터를 HTML로 표시
        } else {
          console.error("Error fetching data:", xhr.statusText);  // 오류 처리
        }
      };
      
      // 요청 실패 시 오류 처리
      xhr.onerror = function() {
        console.error("Request failed:", xhr.statusText);
      };

      xhr.send();  // 요청 보내기
    }
  </script>
</body>
</html>
```
1. var xhr = new XMLHttpRequest();로 XMLHttpRequest 객체를 생성
2. GET 요청 설정: xhr.open("GET", url, true);로 서버에 GET 요청을 보낼 URL을 설정
3. 응답 처리: xhr.onload 함수에서 서버로부터 응답이 오면 xhr.responseText로 응답 데이터를 가져옴. 이 데이터는 보통 JSON 형식이므로 JSON.parse로 객체로 변환
4. HTML에 표시: document.getElementById("result").innerHTML을 사용하여 서버에서 받은 데이터를 페이지에 동적으로 추가
5. 에러 처리: 요청이 실패 시 xhr.onerror에서 에러 처리 -> 콘솔에 에러 출력

### jQuery를 사용한 Ajax 요청
- jQuery: $.ajax() 메서드로 AJAX 요청의 간단한 처리 O
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AJAX 예시 (jQuery)</title>
  <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>
  <h1>AJAX 예시 (jQuery)</h1>
  <button id="fetchButton">데이터 가져오기</button>
  <div id="result"></div>

  <script>
    $(document).ready(function() {
      $('#fetchButton').click(function() {
        $.ajax({
          url: "https://jsonplaceholder.typicode.com/posts/1",  // 요청할 URL
          type: "GET",  // HTTP 요청 방식
          success: function(response) {
            $('#result').html(`<h2>${response.title}</h2><p>${response.body}</p>`);  // 성공적으로 데이터를 받으면 HTML에 표시
          },
          error: function(xhr, status, error) {
            console.error("Error:", error);  // 오류 처리
          }
        });
      });
    });
  </script>
</body>
</html>
```
1. jQuery로 AJAX 요청 보내기: $.ajax() 메서드를 사용하여 AJAX 요청을 보냄
2. 요청 성공 시 처리: success 콜백 함수에서 서버 응답을 받아서 HTML을 동적으로 업데이트
3. 에러 처리: error 콜백 함수에서 에러 처리

### AJAX와 Fetch API
- Fetch API: 객체를 직접 다루지 X, 간단하고 모던한 방식으로 AJAX 요청 O
- Promise 기반으로 async/await과 함께 사용
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AJAX 예시 (Fetch)</title>
</head>
<body>
  <h1>AJAX 예시 (Fetch)</h1>
  <button onclick="fetchData()">데이터 가져오기</button>
  <div id="result"></div>

  <script>
    async function fetchData() {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts/1');  // 서버 요청
        if (!response.ok) throw new Error('Network response was not ok');  // 오류 처리

        const data = await response.json();  // JSON 형식의 응답을 파싱
        document.getElementById("result").innerHTML = 
          `<h2>${data.title}</h2><p>${data.body}</p>`;  // HTML에 데이터 표시
      } catch (error) {
        console.error('There was a problem with the fetch operation:', error);  // 에러 처리
      }
    }
  </script>
</body>
</html>
```
1. fetch 사용: fetch() 메서드를 사용하여 서버에 요청을 보냄
2. async/await 사용: 비동기 요청을 기다리기 위해 async/await를 사용하여 코드의 가독성을 높임
3. JSON 파싱: 응답 데이터를 .json() 메서드를 사용하여 JavaScript 객체로 변환

## 정리
- AJAX는 웹 페이지에서 서버와의 상호작용을 비동기적으로 처리하게 해줌
-> 페이지 새로고침없이 서버와 데이터 주고받고 화면의 동적 업데이트 가능
- XMLHttpRequest 객체를 사용 방법 외에, jQuery와 Fetch API 사용 시 더 간단하고 직관적 구현 O 