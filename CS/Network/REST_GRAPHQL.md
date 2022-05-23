> Q: REST API vs Graph QL : Which one is better?
> A: Well, it depends.

REST API와 Graph QL의 차이점은 뭐고, 어느 걸 사용하는 게 좋을까요? 오늘은 REST API를 중심으로 REST API와 Graph QL의 차이에 대해 다뤄보도록 하겠습니다.

인터넷의 발달로 기존에는 없었던 거대한 규모의 웹사이트들(e.g. 페이스북)이 등장했고, 이 커다란 공룡들을 관리하기 위해 웹 개발이 새로운 국면을 맞이했습니다. 백엔드와 프론트엔드로 각자의 전문성이 분리된 것입니다. 그 결과 현대의 웹사이트는 하나로 통합되어 있던 옛날과 달리 서버가 클라이언트 서버와 데이터베이스 서버로 분리되었습니다. 그래서 클라이언트단에서 데이터베이스에 있는 정보를 읽고 쓰기 위해선 컴퓨터들끼리 통신을 해야 합니다. 이때 컴퓨터들이 서로 통신하는 방식이 바로 **API**입니다.

통신을 하기 위해서는 모두가 이해할 수 있는 약속을 정해야 합니다. 오늘의 주제인 REST API가 바로 그 클라이언트와 서버가 서로 데이터를 잘 주고 받을 수 있도록 정해놓은 약속입니다. 더 정확히 말하자면, REST API는 'API는 이렇게 사용하면 좋습니다'라고 정리해둔 모범사례라고 할 수 있습니다. HTTP에서 필요한 자원에 접근할 때 웹의 장점을 최대한 활용하기 위한 아키텍처로 만들어졌죠. 앞서, REST API는 'API를 이렇게 사용하면 좋습니다'라는 모범사례라고 했습니다. 그럼 그 '이렇게'가 뭘까요?

> **REST API**

- 모든 Resource(자료, User, …)들을 하나의 Endpoint 에 연결해놓고, 각 Endpoint 는 그 Resource 와 관련된 내용만 관리하게 하자는 방법론이다.
- HTTP URI를 통해 자원을 명시하고 , HTTP Method(post,get,put,delete)를 통해 해당자원에 대한 CRUD Operation을 적용한다.
- 따라서 형식(주소) 만으로 대충 이게 무슨 요청인지 알 수 있어야 한다.

자, 그럼 REST API의 구성요소를 자세히 살펴보겠습니다.

#### 1. HTTP Method - 행위

GET: 데이터 조회
POST: 새로운 데이터 추가
PUT: 데이터 전체 수정
PATCH: 데이터 일부 수정
DELETE: 정보 삭제

#### 2. URL - 데이터 접근

#### 3. Representation of Resource - 자원의 표현

REST API의 장점은 다음과 같습니다.

> - HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구출할 필요가 없다.

- HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.

하지만 마법의 탄환은 없다는 말처럼, REST API에도 단점이 있습니다. 바로 Over Fetching과 Under Fetching입니다.

**Over Fetching**은 필요한 정보보다 더 많은 데이터를 전달 받는 것을 말합니다.

**Under Fetching**은 필요한 데이터를 만들기 위해 여러 번의 호출이 필요한 것을 뜻합니다. REST API의 경우, 두 가지 종류의 정보가 동시에 필요하다면 API 호출이 2번 필요하고, 세 가지라면 3번 호출해야 합니다. 추가적인 리소스 요청이 발생하는 셈이죠. 여러 요청을 통해 전달받은 정보를 조합하는 추가 작업도 발생합니다.

뿐만 아니라 REST API는 API마다 다른 URL이 존재합니다. 경우에 따라 수십, 수백 개의 URL이 필요할 수 있습니다. 게다가 API를 만들 때 이름도 일일이 지어줘야겠죠. API를 사용할 때도 API URL을 계속해서 확인해야 한다는 귀찮음이 따릅니다.

그래서 페이스북은 **정보를 요청하는 쪽에서 정보를 원하는 형태로 가져오고 수정**할 수 있는 Graph QL을 만들었습니다. Graph Query Language의 줄임말로, Query Language는 데이터베이스 또는 데이터 관리 시스템에 접근하기 위한 언어를 뜻합니다. Graph QL은 특히 서버 API로 정보를 주고받는 것이 특화된 언어입니다.

Graph QL의 장점이 몇 가지 있지만, 핵심은 **필요한 정보만 정확히 얻을 수 있다는 점**과 **항상 예측 가능한 결과를 반환한다는 점**입니다.

GraphQL API 는 주로 전체 API를 위해서 하나의 Endpoint를 사용합니다. REST API가 Resource 마다 하나의 Endpoint 를 가지는 것과 대조되는 부분입니다.

REST API에서 어떤 데이터를 조회하거나 추가하는 것과 같은 작업을 진행하고자 할 때, 제일 먼저 생각해야 하는 것은 어떤 엔드포인트로 요청을 보내야 하는지 입니다. 각 엔드포인트는 해당 리소스를 가리키며, 요청의 HTTP method에 따라 어떤 작업을 진행하는 지 달라집니다.

GraphQL에서는 URL을 Resource를 특정 짓는 것에 사용하지 않습니다. GraphQL Schema가 Resource를 특정 짓습니다. 또한, HTTP Method로 어떤 작업을 진행하게 되는지 구분하지 않고, Query, Mutation이라는 타입을 사용해 구분합니다.

어떻게 보면, 어떤 리소스와 필드를 가져오게 될 지 결정한다는 점에서 REST의 resource목록이 Query와 Mutation 타입에서 나열된 필드와 비슷합니다.

GraphQL은 한번의 요청으로 여러 resource에 대해 접근할 수 있습니다. 반면에 REST API에서 여러 리소스에 접근하고자 한다면 여러 번의 요청은 불가피합니다.

자, 그럼 다시 처음으로 되돌아가보겠습니다.

### Q: REST API vs Graph QL : Which one is better?

서로 다른 모양의 다양한 요청들에 대해 응답할 수 있어야 할 때, 대부분의 요청이 CRUD(Create-Read-Update-Delete) 에 해당할 때는 Graph QL을,

HTTP 와 HTTPs 에 의한 Caching 을 잘 사용하고 싶을 때, File 전송 등 단순한 Text 로 처리되지 않는 요청들이 있을 때, 요청의 구조가 정해져 있을 때는 REST API를 사용하면 좋습니다.

참조:

ArjanCodes **REST API vs Graph QL** https://www.youtube.com/watch?v=p3rr9_DvaWI
퉁퉁코딩 **Graph QL** https://www.youtube.com/watch?v=xiE9-S7s9rs
퉁퉁코딩 **REST API** https://www.youtube.com/watch?v=X4DezEXbc5o
**프론트엔드의 역사** https://velog.io/@teo/frontend
**REST API** https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html
**URL Routes vs GraphQL Schema** https://hwasurr.io/api/rest-graphql-differences/
