## Basic

---

### 실습환경 구축

- [nodeJS 설치](https://nodejs.org/en/) - v16.13.2
- METEOR JS 설치 - `npm i -g meteor`
- 소스코드 포크 - https://github.com/freeseamew/graphql-study-apollo-v3.git

```cmd
meteor run
```

http://localhost:3000/graphql GraphQL Playground

### Query & Mutation

- 용어 정리  
  Query - 데이터 조회  
  Mutation - 데이터 추가, 수정, 삭제  
  Schema - 요소의 구조를 담당

- Query

```
query {
    humans {
        humanName
        gender
        blood
        age
        phone
        hobbies {
          hobbyName
        }
    }
}
```

- Mutation

```
mutation {
  addPerson(humanName: "HWT", blood: "0", age:25, gender: "male", phone: "01012345678") {
    _id
    humanName
    age
  }
}

```

- 정리

1. query란 서버의 데이터를 조회하는 타입
2. 조회에 필요한 조건을 만들어 서버에 요청 가능
3. mutation은 서버의 데이터를 가공하는데 사용하는 타입

### Schema Basic

- 종류

1.  scalar 정의 Type
2.  사용자 정의 Type
3.  Query, Mutation 등 기본 Type

- scalar  
  : 하나의 수치만으로 완전히 표시되는 양 (원시 타입)  
  int float string boolean ID

```
Scalar Date

type Post {
  title: String
  createAt: Data
}
```

- 사용자 정의

```
type Human {
  humanName: String! // !(느낌표) => 호출 시 무조건 사용돼야 함
  school: School
  hobbies: [Hobby] // [](대괄호) => 결과가 배열
}

type Hobby {
  hobbyName: String
}

type School {
  _id: ID
  name: String
}
```

- Query & Mutation 정의

```
type Query {
  humans: [Human]
  belongs: [BelongTo]
  people(humanName: String): Person
  school: [School]
  workers: [Worker]
}

type Mutation {
  addPerson(humanName: String, blood: String, age: Int, sex: String, phone: String): Person
}
```

- 정리

1. schema란 GraphQL의 구조 및 형태를 정의하는 것
2. int, float, string, boolean, id 로 이루어진 기본 scalar 타입
3. scalar 타입을 베이스로 사용자에 의한 커스텀 타입 구조화 가능
4. Query, Mutation 등도 Schema로 정의해야 호출 가능

### Schema Advanced

- interface  
  : 중복해서 사용해야 하는 필수 타입 정의

```
interface TypeCommon {
  _id: ID
  name: String
}

type Worker implements TypeCommon {
  _id: ID
  name: String
  humanType: String
}
```

- union  
  : A 또는 B 등과 같이 분기를 나눈 타입

```
union BelongTo = School | Worker

type Worker implements TypeCommon {
  _id: ID
  name: String
  humanType: String
}

type School implements TypeCommon {
  _id: ID
  name: String
  humanType: String
  location: String
}

type Query {
  belongs: [BelongTo]
}
```

```
query {
  belongs {
    ...on Worker {
      name
      humanType
    }
    ...on School {
      name
      humanType
      location
    }
  }
}
// 쿼리 사용 예제
```

- enum  
  : 타입에 들어갈 값을 미리 정의

```
enum Blood {
  A
  B
  O
  AB
}

type Human {
  humanName: String
  blood: Blood
}
```

- subscription  
  : 구독을 통한 실시간 데이터 처리  
  => 발행 시 구독 전체에게 변경을 알리는 것으로 채팅 알람 등에 유용

```
type Subscription {
  personAdded: Person
}
```

```
subscription {
  personAdded {
    _id
    humanName
    blood
  }
}

// Listen...
```

```
mutation {
  addPerson(humanName: "HWT", blood: "O")
}

// 위 코드에서 Listen이 끝나고 삽입한 결과가 나옴
```
