## Advanced

---

### apollo-server Structure

- 각종 타입을 정의한 schema들을 typeDefs에 모아줌
- 호출에 대한 물리적 처리를 하는 부분을 resolver로 만듦
- typeDefs와 resolver는 makeExecutableSchema로 합친 후 apolloServer가 선언되는 곳에 배치
- server.start()를 이용해 apollo 서버 작동
- 미들웨어 설정

### MongoDB Basic

[Studio 3T 설치](https://studio3t.com/)

1. 실행 후 url 입력이 아닌 아래 체크 선택
2. Port를 3001로 변경

- Schema less  
  구조를 정의하는 Schema가 없고, 백지에 텍스트를 입력하는 구조  
  => 일반적인 DB와 달리 중복을 권장하기도 함

- No SQL

Tree, Table, JSON 형식으로 데이터 확인이 가능

- 조회 : find()  
  db.getCollection("컬렉션명").find().skip(제외할 필드의 개수).limit(불러올 필드의 개수)

```
// 혈액형이 A인 사람만 조회
db.getCollection("ex_1_human").find({"blood":"A"})

// 혈액형이 A이고 성별이 남성인 사람만 조회
db.getCollection("ex_1_human").find({"blood":"A", "gender":"male"})

// 혈액형이 A거나 B인 사람만 조회
db.getCollection("ex_1_human").find({"blood":{$in: ["A", "B"]}})

// 상단 5개만 조회
db.getCollection("ex_1_human").find({}).limit(5)

// 페이지네이션, skip(n)을 변경하면서 데이터 조회
db.getCollection("ex_1_human").find({}).limit(5).skip(0)
```

- 삽입 : insert()  
  db.getCollection("컬렉션명").insert({  
  　"필드명": "필드값",  
  　"필드명": "필드값",  
  })

```
// 데이터 추가
db.getCollection("ex_1_human").insert({
    humanName: "sun",
    blood: "A",
    gender: "male",
    age: 12
})

// 추가한 데이터 조회
db.getCollection("ex_1_human").find({"humanName":"sun"})
```

- 수정 : update()  
  *id는 ObjectId()로 감싸줘야 함, *인 경우와 id인 경우 모두 고려  
   db.getCollection("컬렉션명").update(  
   　{\_id:ObjectId("id값")},  
   　{$set: {  
   　　필드이름: 변경할 값,  
   　　필드이름: 변경할 값,  
   　　필드이름: 변경할 값,  
   　}  
   　}  
   )

```
// 데이터 수정
db.getCollection("ex_1_human").update(
    {_id: ObjectId("62e34c9e585673fe70cf7502")},
    {
        $set: {
            blood: "B",
            age: "20"
        }
    }
)

// 수정한 데이터 조회
db.getCollection("ex_1_human").find({"humanName":"sun"})
```

- 삭제 : remove()  
  db.getCollection("컬렉션명").remove({\_id: ObjectId값})  
  db.getCollection("컬렉션명").remove(ObjectId값)

```
// 데이터 삭제
db.getCollection("ex_1_human").remove(ObjectId("62e34c9e585673fe70cf7502"))

// 삭제한 데이터 조회
db.getCollection("ex_1_human").find({"humanName":"sun"})
```
