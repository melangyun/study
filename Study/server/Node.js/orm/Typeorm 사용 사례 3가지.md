# 1. 필요한 컬럼만 select 할때

- [c] 안좋은 케이스
```ts
async getUserNames(): Promise<{id: number, name: string }[]> {  
  return User.find({  
    select: ['id', 'name']  
  })  
}
```
- [p] 좋은 케이스
```ts
async getUserNames(): Promise<Pick<User, 'id' | 'name'>[]> {  
  return User.find({  
    select: ['id', 'name']  
  })  
}
```

## typeorm find param으로 동작

parameter를 사용하는것이 가능해졌다

> 단, `(0.3.x)`버전 이후

```ts
async getUserNames() {  
  return User.find({  
    select: {  
      id: true,  
      name: true,  
      office: {  
         id: true,  
         name: true  
       }  
     },  
     relations: ['office']  
  })  
}
```

이전 버전은 다음과 같이 표현이 가능하다

- [c] 안좋은 케이스
```ts
// 이 코드는 동작하지 않는다.
async getUserNames(): Promise<Pick<User, 'id' | 'name'>[]> {  
  return User.find({  
    select: ['id', 'name'],
    relations: ['office']
  })  
}
```
find의 select는 `Entity key`로 제한적이기 때문에 동작하지 않는다.

- [p] 좋은 경우  
```ts
async getUserNames(): Promise<(  
  Pick<User, 'id' | 'name'> & {  
  office: Pick<Office, 'id' | 'name'>  
})[]> {  
  return User.createQueryBuilder('user')  
    .select(['user.id', 'user.name'])  
    .addSelect(['office.id', 'office.name'])  
    .innerJoin('user.office', 'office')  
    .getMany()  
}
```

# SQL 주석 포함

(사용 의도를 위한 모니터링을 할수있음)
QueryBuilder는 `0.2.29` 부터, FindOptiuons에는 `0.2.42`버전부터 사용이 가능하다.

```ts
// FindOptions  
User.find({  
  comment: '### getUserNames ###', // 주석  
  select: ['id', 'name']  
})  
// QueryBuilder  
User.createQueryBuilder('user')  
  .comment('### getUserNames ###')  
  .select(['user.id', 'user.name'])  
  .getMany()
```

# Insert시 SQL의 실행 동작이 다르다.

## .save()
Entity를 응답해주기위해 매번 Insert이후 SELECT을 하게된다.
```typescript
// 입력할 데이터  
const rows = [  
User.create({ name: '김직방' }),  
User.create({ name: '박직방' })  
]  
// CODE  
await User.save(rows)  
// SQL  
START TRANSACTION  
INSERT INTO user(id, name) VALUES (DEFAULT, '김직방')  
SELECT User.id AS User_id, User.name AS User_name FROM user User WHERE User.id = 101  
INSERT INTO user(id, name) VALUES (DEFAULT, '박직방')  
SELECT User.id AS User_id, User.name AS User_name FROM user User WHERE User.id = 102  
COMMIT
```
아쉬운 부분
- 매번 INSERT를 반복함
- 갱신된 Entity를 생성하기 위해 다시  SELECT을 하게된다.



---
[typeorm 사용 사례 3가지](https://medium.com/zigbang/typeorm-%EC%82%AC%EC%9A%A9%EC%82%AC%EB%A1%80-3%EA%B0%80%EC%A7%80-6a3c2bcd6cff)