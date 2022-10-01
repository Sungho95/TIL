## AJAX(**Asynchronous JavaScript And XML*)***란?

AJAX는 JavaScript, DOM, Fetch, XML, HTML 등의 다양한 기술을 사용하는 웹 개발 기법이다.

AJAX의 가장 큰 특징은 웹 페이지에 필요한 부분에 필요한 데이터만 비동기적으로 받아 화면에 그려낼 수 있다는 것이다.

구글에 접속하면 다음과 같은 웹 페이지를 확인할 수 있다.

![AJAX2.PNG](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cad18aa1-c286-4d69-931e-71c7662dbb06/AJAX2.png)

이 웹 페이지는 html에 의해 유저에게 필요한 페이지가 렌더링 된다.

그러나 검색창에서는 html에 작성된 대로 유저가 사용하는 것이 아니라, 유저의 요구에 따라 반응하며 변화한다.

검색창에 한 글자를 입력할 때마다, 해당 글자로 시작하는 단어들을 서버로부터 받아와 추천 검색어로 보여주게 된다.

이러한 경우가 필요한 데이터만 비동기적으로 받아와 렌더링되는 것으로 AJAX가 사용된다.

뿐만 아니라, 스크롤이 긴 페이지의 경우 사용자가 맨 밑까지 스크롤 하여 스크롤바 하단에 도달하면, 새로운 목록이 생성되는 페이지를 자주 접할 수 있다.

이를 무한 스크롤 이벤트라고 하며, 무한 스크롤이 발생할 때마다 Fetch를 통해 데이터를 가져와 업데이트하고 서버로부터 렌더링한다.

이와같이 비동기적으로 데이터를 서버에서 받아와 브라우저에 렌더링 하는 것을 AJAX 기법이라 한다.

## AJAX의 핵심 기술

AJAX를 구성하는 핵심 기술은 JavaScript와 DOM, Fetch가 있다.

**Fetch**

전통적인 웹 애플리케이션에서는 <from> 태그를 이용하여 서버에 데이터를 전송해야 한다. 또한, 서버는 요청에 대한 응답으로 새로운 웹 페이지를 제공해 주어야 헀다. 즉, 클라이언트에서 요청을 보내면 매번 새로운 페이지로 이동해야 한다는 것이다.

그러나 Fetch를 사용하면 페이지를 이동하지 않아도 서버로부터 필요한 데이터를 받아올 수 있다. Fetch는 서버에 요청을 보내고 응답 받을 때까지 모든 동작을 멈추는 것이 아닌 계속해서 페이지를 사용할 수 있게 하는 비동기적인 방식을 사용한다.

**JavaScript와 DOM**

또한 JavaScript에서 DOM을 사용해 조작할 수 있기 때문에 Fetch를 통해 전체 페이지가 아닌 필요한 데이터만 가져와 DOM에 적용시켜 새로운 페이지로 이동하지 않고 기존 페이지에서 필요한 부분만 변경할 수 있다.

**XHR과 Fetch**

Fetch 이전에는 XHR(XMLHttpRequest)를 사용했다. Fetch는 XHR의 단점을 보완한 새로운 Web API로 XML보다 가볍고 JavaScript와 호환되는 JSON을 사용한다.

따라서 현재 XHR보다 Fetch를 많이 사용하고 있다.

**Fetch 사용 예제**

```jsx
// Fetch를 사용
fetch('http://52.78.213.9:3000/messages')
	.then (function(response) {
		return response.json();
	})
	.then(function (json) {
		...
});
```

**XMLHttpRequest 사용 예제**

```jsx
// XMLHttpRequest를 사용
var xhr = new XMLHttpRequest();
xhr.open('get', 'http://52.78.213.9:3000/messages');

xhr.onreadystatechange = function(){
	if(xhr.readyState !== 4) return;
	// readyState 4: 완료

	if(xhr.status === 200) {
        // status 200: 성공
		console.log(xhr.responseText); // 서버로부터 온 응답
	} else {
		console.log('에러: ' + xhr.status); // 요청 도중 에러 발생
	}
}

xhr.send(); // 요청 전송
```

Fetch의 등장 이전에는 표준화된 XHR을 사용했다. 하지만, XHR은 Cross-Site 이슈 등의 불편함이 있었다.

Fetch는 간편함과 promise 지원 등의 장점을 가지고 있어 대부분 Fetch를 사용하고 있다.

이 외에도 Axios와 같은 라이브러리도 존재하며, 경우에 따라 적절한 것을 선택하여 사용한다.

## AJAX의 장단점

**장점**

1. 서버에서 HTML을 완성하여 보내주지 않아도 웹페이지를 만들 수 있다.
2. 브라우저에 상관없이 AJAX를 사용할 수 있다.
3. 빠르고 더 많은 상호작용이 가능한 애플리케이션을 만들 수 있다.
4. 필요한 데이터를 JSON, XML 등 텍스트 형태로 보내기 때문에 데이터의 크기가 작다.

**단점**

1. 검색 엔진 최적화(SEO : Search Engine Optimization)에 불리하다.
2. AJAX는 이전 상태를 기억하지 않기 때문에 뒤로 가기 기능에 대해 의도한 대로 동작하지 않을 가능성이 높다. 이를 구현하기 위해 별도의 History API를 사용해야 한다.