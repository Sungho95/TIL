## 웹(Web)이란?

월드 와이드 웹(World Wide Web)은 전 세계에 퍼져 있는 인터넷 정보들을 서로 거미줄 처럼 연결해준다. 즉, 인터넷에 연결된 사용자들이 서로의 정보를 주고받을 수 있는 공간을 의미한다.

이러한 월드 와이드 웹을 WWW으로 줄여 말하기도 하며, 간단히 웹 또는 W3라고도 한다.

웹 프로젝트는 1989년 유럽 핵 물리 공동 연구소(CERN)의 연구원이었던 팀 버너스 리에 의해서 처음 시작되었다. 연구소 내의 직원들이 수많은 정보를 주고 받는 상황에 다른 운영체제나 애플리케이션을 사용하고 있어서 발생하는 문제를 해결하기 위해 만든 개념이다.

따라서 일정한 형식의 기준인 HTML을 제안하게 되었고, HTML은 운영체제나 애플리케이션이 달라도 인터넷 브라우저만 있으면 모두가 동일한 정보를 볼 수 있게 되었다.

즉, 웹은 HTML로 대표되는 하이퍼텍스트 언어 문서와 인터넷이 융합되어 등장한 시스템이다.

웹은 인터넷의 모든 서비스를 통합하여 제공한다. 웹 서비스 이전에 사용되었던 인터넷 서비스에서는 제공할 수 없었던 서비스를 클라이언트와 서버 측면에서 제공하게 되었다.

## 클라이언트-서버 아키텍처

웹에서 제공되는 서비스는 주로 서비스를 이용하는 클라이언트와 서비스를 제공하는 서버로 나뉜다. 이러한 구조를 클라이언트-서버 아키텍처(또는 2티어 아키텍처)라고 한다.

클라이언트-서버 아키텍처는 리소스가 존재하는 곳과 리소스를 사용하는 앱으로 분리시켜 서로 요청과 응답을 주고 받는 구조로 되어 있다.

리소스를 사용하는 앱이 클라이언트, 리소스를 제공하는 곳이 서버이다.

클라이언트-서버 아키텍처에서는 클라이언트의 요청이 먼저 이러우지며, 그 후 서버로부터 응답을 받는 구조이다. 클라이언트가 요청을 하지도 않았는데 서버로부터 응답이 오는 경우는 없다.

**클라이언트**

클라이언트는 사용자가 직접 이용하는 것으로, 사용 편의성이나 휴대성 등을 고려해 개발이 이루어진다.

**서버**

서버는 유지보수를 할 시점을 제외하고는 24시간 일년 내내 작동하고 있어야 한다. 클라이언트가 언제 접속하여 서비스를 이용할지를 알 수 없기 때문이다. 하지만, 사용자와는 직접적인 접점이 없기 때문에 편의성 보다는 기능에 중점을 두고 개발이 이루어진다.

**3티어 아키텍처**

일반적으로 서버는 리소스를 전달해 주는 역할만 담당한다. 리소스를 저장하는 별도의 공간이 존재하며 이를 데이터베이스라고 한다.

데이터베이스는 클라이언트가 서버에게 요청을 했을 때, 요청에 대해 응답하기 위한 리소스를 데이터베이스로부터 찾아 클라이언트에게 응답을 하게 된다.

이처럼 기존 2티어 아키텍처에 데이터베이스가 추가된 형태를 3티어 아키텍처라고 한다.

**클라이언트와 서버의 종류**

클라이언트는 보통 플랫폼에 따라 구분된다.

브라우저를 통해 주로 이용하는 웹(Web) 플랫폼에서의 클라이언트는 웹 사이트 또는 웹 앱이라고 부른다.

iOS나 안드로이드, 윈도우와 같은 운영체제 플랫폼에서의 클라이언트는 애플리케이션 또는 프로그램이 클라이언트가 될 수 있다.

서버는 무엇을 하느냐에 따라 종류가 달라진다.

파일 서버는 파일을 제공하는 앱, 웹  서버는 웹 사이트나 웹 앱에서 필요로 하는 정보들을 제공하는 앱, 메일 서버는 메일을 주고받을 수 있도록 도와주는 앱이된다.