# 조인

## 관련 질문
<details>
  <summary>
    DB에서 두 테이블을 조인하는 4가지 방법에 대해 설명해주세요
  </summary>
  <blockquote>
    두 테이블을 조인하는 방법으로는 내부 조인, 왼쪽 조인, 오른쪽 조인, 합집합 조인이 있습니다.<br/>
    내부 조인은 두 테이블의 교집합을 레코드로 생성하는 것이며, 왼쪽 조인은 교집합과 왼쪽 테이블의 레코드를 모두 생성하는 것입니다. 이때 오른쪽 테이블에 해당 값이 없을 경우 null로 표시됩니다.<br/>
    마찬가지로 오른쪽 조인은 교집합과 오른쪽 테이블의 레코드를 생성하는 것이며, 합집합 조인은 두 테이블의 모든 값을 레코드로 생성하는 것입니다. 왼쪽 조인과 마찬가지로 해당 값이 없는 경우 null로 표시가 됩니다.
  </blockquote>
</details>
<br/>

<hr/>

## 조인이란?

- 하나의 테이블이 아닌 두 개 이상의 테이블을 묶어서 하나의 결과물을 만드는 것
- MySQL에서는 JOIN이라는 쿼리 사용, MongoDB에서는 lookup이라는 쿼리 사용
- lookup 보다는 관계형 데이터베이스의 JOIN 연산이 성능이 우수함

## 조인의 종류

1. 내부 조인(inner join)
2. 왼쪽 조인(left outer join)
3. 오른쪽 조인(right outer join)
4. 합집합 조인(full outer join)

[SQL JOIN 시각화 사이트](https://sql-joins.leopard.in.ua/)

### 내부 조인

- 두 테이블 간에 교집합

```sql
SELECT * FROM TableA A
INNER JOIN TableB B ON
A.key = B.key
```

### 왼쪽 조인

- 테이블 B의 일치하는 부분의 레코드와 함께 테이블 A를 기준으로 완전한 레코드 집합을 생성
- 테이블 B에 일치하는 항목이 없으면 null로 표시

```sql
SELECT * FROM TableA A
LEFT JOIN TableB B ON
A.key = B.key
```

### 오른쪽 조인

- 테이블 A에서 일치하는 부분의 레코드와 함께 테이블 B를 기준으로 완전한 레코드 집합을 생성
- 테이블 A에 일치하는 항목이 없으면 null로 표시

```sql
SELECT * FROM TableA A
RIGHT JOIN TableB B ON
A.key = B.key
```

### 합집합 조인

- 양쪽 테이블에서 일치하는 레코드와 함께 테이블 A와 테이블 B의 모든 레코드 집합을 생성
- 일치하는 항목이 없으면 누락된 쪽에 null로 표시

```sql
SELECT * FROM TableA A
FULL OUTER JOIN TableB B ON
A.key = B.key
```

[예시와 함께 조인 결과를 보고싶다면 클릭!](https://leejinseop.tistory.com/19)

## 조인의 원리

### 중첩 루프 조인

- Nested Loop Join(NLJ)
- 중첩 for 문과 같은 원리로 조건에 맞는 조인을 하는 방법
- 랜덤 접근에 대한 비용이 많이 증가하여 대용량의 테이블에서는 적절치 않음
- 중첩 루프 조인에서 발전시킨 블록 중첩 루프 조인이 존재

**예시 코드**
```
for each row in t1 matching reference key {
    for each row in t2 matching reference key {
        if row satisfies join conditions, send to client
    }
}
```

### 정렬 병합 조인

- 각각의 테이블을 조인할 필드 기준으로 정렬하고 정렬이 끝난 이후에 조인 작업을 수행하는 조인 방법
- 적절한 인덱스가 없고 대용량의 테이블들을 조인해야 할 때 필요
- 또한, 조인 조건으로 <, > 등 범위 비교 연산자가 있을 때 필요

### 해시 조인

- 해시 테이블을 기반으로 조인하는 방법
- 하나의 테이블이 메모리에 온전히 들어간다면 중첩 루프 조인보다 효율이 좋음
- 동등(=) 조인에서만 사용 가능

[해시 조인의 과정 및 원리](https://goodbyeanma.tistory.com/64)
