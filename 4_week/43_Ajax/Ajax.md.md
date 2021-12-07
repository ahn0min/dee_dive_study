## 1.Ajax(Asynchronous JavaScript and XML)

### 1-1 Ajax란 무엇인가요?
__Ajax란__ 자바스크립트를 사용하여 __브라우저__ 가 __서버__ 에게 비동기 방식으로 __데이터를 요쳥__ 하고, 서버가 응답한 데이터를 수신하여 __웹페이지를 동적으로 갱신하는 프로그래밍 방식__ 입니다.

Ajax 등장 이전에는 서버로부터 html 태그로 시작하여 html 태그로 끝나는 완성된 형태의 HTML을 전송받아 전체를 렌더링하는 방식을 사용했다. 그러나 이런 방식은 여러 문제점들이 존재했다.

1. 불필요한 통신이 존재함(HTML 전체를 다시 서버로부터 수신하기 때문에)
2. 불필요한 화면의 깜박임 발생(전체를 다시 렌더링하기 때문에)
3. 클라이언트와 서버의 통신은 동기방식임으로 서버로부터 응답이 오기전까지의 다음처리는 블로킹됨

이런 전통적인 방식의 문제점은 __Ajax__ 의 등장과 함께 모두 해결되었습니다.
- 필요한 부분만 통신가능 (필요한 통신만 주고받음)
- 한정적인 부분만 다시 렌더링 가능 (화면 깜박임 소멸)
- 블로킹이 발생하지 않음 (비동기 방식으로 동작)

<br>

### 1-2 JSON(JavaScript Object Notation)
__JSON__ 이란 클라이언트와 서버간의 HTTP(Hyper Text Transfer Protocol)통신을 위한 텍스트 데이터 포맷입니다. 자바스크립트에 종속되지 않는 독립적인 데이터 포맷으로 대부분의 프로그래밍 언어에서 사용이 가능합니다.
#### JSON 표기방식
```js
{
  "key": "value"
}
``` 
자바스크립트의 객체리터럴과 유사하게 `key`와 `value`로 구성되어져 있으나 __반드시  `key`를 큰따음표(""__)__로 묶어서 사용해야 한다는 차이점이 존재합니다.

<br>

### 1-3 JSON.parse, JSON.stringify
JSON객체는 자바스크립트에 빌드인된 객체로써 `parse`, `stringify` 를 메서드로 가지고 있습니다.
- stringify: 자바스크립트 객체 -> JSON 형식의 문자열로 변환
- parse: JSON 형식의 문자열 -> 자바스크립트 객체로 변환

```js
const o = { name: 'ahn', age: 20 }
const a = ['1', 0, true];

// JSON.stringify: JavaScript 객체 -> JSON 문자열
const strObject = JSON.stringify(o); 
const strArray = JSON.stringify(a); 

console.log(typeof strObject, strObject) // string {"name":"ahn","age":20}
console.log(typeof strArray, strArray) // string ["1",0,true]

// JSON.parse: JSON 문자열 -> JavaScript 객체
const obj = JSON.parse(strObject);
const arr = JSON.parse(strArray)

console.log(typeof obj, obj) // object { name: 'ahn', age: 20 }
console.log(typeof arr, arr) // object [ '1', 0, true ]
```

<br>

## 2 XMLHttpRequest
- 브라우저는 주소창이나 HTML의 form 태그, a 태그를 통해 HTTP 요청 전송기능을 기본 제공합니다. 
- 자바스크립트를 통해서 HTTP 요청을 전송하려면 __XMLHttpRequest__ 객체를 사용해야 합니다. 
- __XMLHttpRequest__ 는 Web API임으로 HTTP 요청 전송, HTTP 응답 수신을 위한 다양한 메서드, 프로퍼티를 제공합니다.

<br>

### 2-1 XMLHttpRequest 사용하기
```js
// XMLHttpRequest 객체 생성
const xhr = new XMLHTTPRequest()

// HTTP 요청 초기화
xhr.open('GET', 'https://jsonplaceholder.typicode.com/todos/1');

// 클라이언트 -> 서버 전송시 데이터의 MIME 타입 지정: json
xhr.XMLHTTPRequest('content-type', 'application/json');

// HTTP 요청 전송
xhr.send()

// 요청전송이 완려되면 실행
xhr.onload = () => {
    // 상태코드의 값에 따라 다른 동작을 수행하게 해준다.
    // xhr.response는 서버의 응답결과가 담겨있습니다.
    // 200 (정상적으로 응답한 상태)
    if (xhr.status === 200) console.log(JSON.parse(xhr.response));
    // 에러가 발생한 상태
    else console.error('Error', xhr.status, xhr.statusText);
}
```

> - 참고로 이야기 했듯이 XMLHTTPRequest는 브라우저에서 제공하는 Web API임으로 일반적인 Node.js에서는 지원하지 않습니다.
> - Node.js에서는 좀더 사용하기 편리한 타사 라이브러리(Axios, node-fetch)를 지원하고 있습니다.

<br>

### 2-2 Axios 사용예제
```js
const axios = require('axios');

axios.get('https://www.juso.go.kr/addrlink/addrLinkUrl.do')
.then((response) => console.log(response.data))
.catch((err) => console.log(err))
```





