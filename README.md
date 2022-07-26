# GraphQL Full stack Study

[Inflearn 강의](https://www.inflearn.com/course/graphql-%EC%99%84%EC%A0%84%EC%A0%95%EB%B3%B5/dashboard)

[참고자료](https://freeseamew.gitbook.io/graphql/)

코드자료 =>
[실습 자료](https://github.com/freeseamew/graphql-study-apollo-v3)
[디자인 요소](https://github.com/freeseamew/smart-menu-design)
[Smart Menu](https://github.com/freeseamew/smart-menu-study)

## Intro

---

### GraphQL

페이스북에서 만듦

iOS, Android 등 다양한 기기에서 필요한 정보의 형태가 조금씩 다름  
=> REST로 구현하기 어려움

정보를 요청하는 쪽에서 원하는 형태로 정보를 가져오고 수정할 수 있는 API  
=> query language와 유사한 형태의 API 제작

- GraphQL = SQL + API, 단일 uri
- over-fetching : 필요한 데이터보다 많은 정보의 데이터를 호출하는 것
- under-fetching : 필요한 데이터를 만들기 위해 호출을 여러 번 하는 것

```js
query {
    movies {
        original_language
        poster_path
    }
}

// 이와 같은 형식으로 필요한 데이터만 가져옴
```

**장점**

1. 필요한 것을 구체적으로 요청 가능
2. 단일 요청으로 많은 데이터 호출 가능
3. 자동으로 API 명세서 생성

**단점**

- 개발 서버의 구조가 REST API 보다 복잡함
  => 기존 프레임워크가 부족하였으나 현재는 꽤나 보완
