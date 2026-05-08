# SQL 문법 정리

## 사용한 SQL

```sql
SELECT e1.ID, e1.GENOTYPE, e1.GENOTYPE & e2.GENOTYPE AS PARENT_GENOTYPE
FROM ECOLI_DATA e1
JOIN ECOLI_DATA e2 
    ON e1.PARENT_ID = e2.ID
WHERE e1.GENOTYPE & e2.GENOTYPE = e2.GENOTYPE
ORDER BY ID
```

## 핵심 문법

### 1. 테이블 별칭

```sql
FROM ECOLI_DATA e1
JOIN ECOLI_DATA e2
```

같은 테이블을 두 번 사용하기 위해 `e1`, `e2`라는 별칭을 붙였다.

- `e1`: 자식 대장균
- `e2`: 부모 대장균

### 2. SELF JOIN

```sql
JOIN ECOLI_DATA e2
    ON e1.PARENT_ID = e2.ID
```

하나의 테이블을 자기 자신과 조인하는 방식이다.

`e1.PARENT_ID = e2.ID` 조건으로 자식 개체와 부모 개체를 연결한다.

### 3. 비트 AND 연산자

```sql
e1.GENOTYPE & e2.GENOTYPE
```

`&`는 두 숫자를 2진수로 비교해서 둘 다 `1`인 비트만 남기는 연산자다.

이 문제에서는 자식의 형질과 부모의 형질을 비교하는 데 사용했다.

### 4. WHERE 조건

```sql
WHERE e1.GENOTYPE & e2.GENOTYPE = e2.GENOTYPE
```

부모가 가진 모든 형질을 자식도 가지고 있는지 확인하는 조건이다.

부모 형질과 자식 형질을 비트 AND 했을 때 결과가 부모 형질과 같으면, 부모의 형질이 모두 자식에게 포함되어 있다는 뜻이다.

### 5. ORDER BY

```sql
ORDER BY ID
```

결과를 `ID` 기준 오름차순으로 정렬한다.
