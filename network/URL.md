## URL (Uniform Resource Locator)

URL은 웹에 게시된 어떤 자원을 찾기 위해 브러우저에서 사용되는 메커니즘으로, 인터넷상에서 HTML이나 이미지 등 리소스의 위치를 특정하기 위한 서식으로 사용되기 위해 등장했다.

웹에는 수 많은 파일이 연결되어 있는데, 웹에 존재하는 파일을 다른 파일과 구별하기 위한 식별자로 사용되는 것이 URL이다. 인터넷 브라우저의 주소창에 입력한 URL은 서버가 제공되는 환경에 존재하는 파일의 위치를 나타낸다.

예를 들어 구글(https://[google.com](http://google.com):443)에 접속하면 google.com 주소가 가리키는 서버의 기본 폴더를 뜻한다. CLI나 GUI 환경에서 폴더와 파일의 위치를 찾아 이동하듯이 슬래시(/)를 이용해 서버의 폴더에 진입하거나 파일을 요청할 수 있다.

그러나, 기본적인 보안의 일환으로 외부에서 직접 접근이 가능한 경우는 거의 없다.

또한, 특정 브라우저에서 PC의 폴더와 파일을 탐색할 수 있는 파일 탐색기로도 사용할 수도 있다.

크롬에서 OS 환경에 맞게 파일 경로를 입력하면, PC의 해당 위치에 있는 폴더와 파일을 나타낸다.

윈도우 : file://localhost/C:\Users/username\Desktop\

리눅스 : file://127.0.0.1/home/username/Desktop

맥OS : file://127.0.0.1/Users/username/Desktop/

## URL의 구조

![URL.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/251b1ee1-6b39-4889-a2af-23e5db0b0d5a/URL.png)

URL의 구조는 scheme, hosts, url-path로 구분할 수 있다.

**scheme** : ****스킴은 프로토콜이라고도 하며, 통신 방식(프로토콜)을 결정한다. 일반적으로 웹 브라우저에서는 http(s)를 사용한다.

**hosts** : 호스트는 웹 서버의 이름이나 도메인, IP를 사용하며 주소를 나타낸다.

**url-path** : url-path는 웹 서버에서 지정한 루트 디렉토리부터 시작하여 웹 페이지, 이미지, 동영상 등이 위치한 경로와 파일명을 나타낸다.

**URI (Uniform Resource Identifier)**

URI는 URL의 기본 요소인 scheme, hosts, url-path에서 query와 bookmark를 포함한 것을 뜻한다.

**query** : 쿼리는 웹 서버에 보내는 추가적인 질문이다. 위 이미지에서 search는 검색창을 뜻하며, ?q=JavaScript 부분이 쿼리이다. 해당 URI를 입력하면, 구글에 JavaScript를 검색한 결과가 나타난다.

브라우저의 검색 창을 클릭하면 나타나는 주소가 URI이다. URI는 URL을 포함하는 상위 개념으로 ‘URL은 URI이다’는 맞지만, ‘URI는 URL이다’는 틀린 개념이다.