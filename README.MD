# 4.5 Recap

type Query가 없다면 이 서버는 실행되지 않을 수도 있다.
type Query는 가장 기본 type이다.
모든 graphql 서버에서 required인 type이다.
그래서 type Query가 필요하고 type Query에 무엇을 넣던지
그게 user가 request 할 수 있는 것들이 된다.

allTweets field를 Query type 안에 넣는다면,
user가 우리의 graphql API에 allTweets request를 보낼 수 있다.

가끔은 Boolean, ID, String, Int type 만으로는 충분하지 않다.
왜냐하면 data는 더 복잡하기 때문이다.
그래서 우리가 배운건 우리만의 type을 만드는 것이었다.
우리의 경우 우리만의 Tweet type을 만들었다.

graphql한테 어떤 field가 무언가의 list를 준다는 것을 알려주고 싶다면, 대괄호([]) 안에 type의 이름을 넣어주면 된다.

이건 우리가 ID, String, Int, Boolean type 만 썼을 때보다 더 많은 걸 할 수 있게 해준다.

우리가 만든 type을 또 다른 tpye이랑 연결해 줄 수 있다.
그게 우리가 Tweet type에서 한 것이다.

# Tweet type

Tweet type은 id와 string인 text를 가지고 있지만
author도 가지고 있다.
그렇다는건 Tweet이 User를 가진다는 것이다.
우리는 User라는 type을 만들었다.
원하는 type을 만들고 type에 연결 할 수 있다는 것을 배웠다.

# Mutation

Mutation은 API와 소통할 수 있게 해준다.
Mutation에 있는 동작들은 database에 영향을 미치기도 하고,
우리 server의 state를 mutate 할 거다.
Mutation은 POST나 DELETE request,
혹은 resource를 업데이트 하기 위한 PUT request가 될 수 있다.
POST, PUT, DELETE request 같은 것들은
모두 Mutation type에 있어야 한다.

Mutation에 있어야 할 것들을 Query에 넣어도 실행은 되지만,
graphql의 포인트는 무엇은 도대체 무엇이며, 그 의도가 뭔지를 명확히 하는 것이다.

type Query에 있는 field는 database에서 data를 얻고자 하는 것이고,
type Mutation의 field는 database에서 data를 수정하고 하는 것들이다.

# !

느낌표를 쓰지 않는다면 기본적으로 nullable field가 된다.
느낌표는 graphql한테 null이 되면 안된다고 알려주는 것이다.
느낌표를 type 뒤에도 쓰지만 argument에도 쓸 수 있다.

# allTweets: [Tweet!]!

[]! 이건 allTweets가 항상 list를 준 다는 것을 의미한다.
항상 null이어서는 안 되고 list여야 한다.
[Tweet!]! 이건 항상 list가 되어야 한다는 것이고, list는 항상 Tweet이란 거다. null이어서는 안 된다.
database에 Tweet이 비어있더라도 에러가 뜨지는 않는다.
비어있다는 것은 null이 아니고 그냥 비어있는 것이다.
핵심은 allTweets field가 항상 Tweet들을 가지고 있어야 한다는 게 아니다.
서버를 방금 시작했을 수도 있고, database에 Tweet이 없을 수도 있다.

# tweet(id: ID!): Tweet

하나의 tweet을 보고싶다면 id를 보내야하지만,
tweet이 삭제되어 원하는 tweet을 찾지 못할 수도 있다.
그래서 이 경우에는 Tweet이다. (nullable이다.)
