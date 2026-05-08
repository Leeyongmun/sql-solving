# SQL 문법 정리

## 사용한 SQL

```sql
SELECT
    o.ANIMAL_ID,
    o.NAME
FROM ANIMAL_OUTS o
LEFT JOIN ANIMAL_INS i
    ON i.ANIMAL_ID = o.ANIMAL_ID
WHERE i.ANIMAL_ID IS NULL;
```

## 코드 설명

### 1. 입양 기록 테이블 기준 조회

```sql
FROM ANIMAL_OUTS o
```

이 문제는 `입양은 되었지만, 보호 시작 기록이 없는 동물`을 찾는 문제입니다.

그래서 입양 정보를 담고 있는 `ANIMAL_OUTS` 테이블을 기준으로 조회합니다.

### 2. `LEFT JOIN`으로 보호 시작 기록 연결

```sql
LEFT JOIN ANIMAL_INS i
    ON i.ANIMAL_ID = o.ANIMAL_ID
```

`ANIMAL_OUTS`의 모든 데이터를 유지한 채, 같은 `ANIMAL_ID`를 가진 `ANIMAL_INS` 데이터를 연결합니다.

즉, 입양 기록은 있는데 보호 시작 기록이 없는 경우에도 결과에서 사라지지 않도록 `LEFT JOIN`을 사용합니다.

### 3. 보호 시작 기록이 없는 데이터만 필터링

```sql
WHERE i.ANIMAL_ID IS NULL
```

`LEFT JOIN` 결과에서 매칭되는 `ANIMAL_INS` 데이터가 없으면 `i` 테이블의 컬럼 값은 `NULL`이 됩니다.

따라서 `i.ANIMAL_ID IS NULL` 조건을 사용하면 보호 시작 기록이 없는 동물만 조회할 수 있습니다.

### 4. 조회 컬럼

```sql
SELECT
    o.ANIMAL_ID,
    o.NAME
```

문제에서 요구한 동물의 아이디와 이름만 출력합니다.
