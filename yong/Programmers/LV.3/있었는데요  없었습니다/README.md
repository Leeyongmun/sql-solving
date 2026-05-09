# SQL 풀이 설명

## 풀이 SQL

```sql
SELECT i.ANIMAL_ID, i.NAME
FROM ANIMAL_INS i
    JOIN ANIMAL_OUTS o ON i.ANIMAL_ID = o.ANIMAL_ID
WHERE
    i.DATETIME > o.DATETIME
ORDER BY i.DATETIME
```

## 코드 설명

### 1. 보호소 입소 기록 조회

```sql
FROM ANIMAL_INS i
```

`ANIMAL_INS` 테이블은 동물이 보호소에 들어온 기록을 담고 있습니다.

문제에서 조회해야 하는 동물의 아이디와 이름은 입소 기록 기준으로 가져오므로 `ANIMAL_INS` 테이블을 기준으로 조회합니다.

### 2. 입양 기록 테이블 연결

```sql
JOIN ANIMAL_OUTS o ON i.ANIMAL_ID = o.ANIMAL_ID
```

`ANIMAL_OUTS` 테이블은 동물이 입양을 간 기록을 담고 있습니다.

입소 기록과 입양 기록을 같은 동물 기준으로 비교해야 하므로 `ANIMAL_ID`를 기준으로 두 테이블을 `JOIN`합니다.

### 3. 날짜가 잘못된 데이터 찾기

```sql
WHERE
    i.DATETIME > o.DATETIME
```

정상적인 데이터라면 보호 시작일인 `i.DATETIME`이 입양일인 `o.DATETIME`보다 빠르거나 같아야 합니다.

하지만 이 문제에서는 보호 시작일이 입양일보다 늦은 동물을 찾아야 하므로 `i.DATETIME > o.DATETIME` 조건을 사용합니다.

### 4. 조회할 컬럼 선택

```sql
SELECT i.ANIMAL_ID, i.NAME
```

문제에서 동물의 아이디와 이름을 출력하라고 했으므로 `ANIMAL_ID`와 `NAME`을 조회합니다.

### 5. 보호 시작일 기준 정렬

```sql
ORDER BY i.DATETIME
```

결과는 보호 시작일이 빠른 순서대로 정렬해야 하므로 `i.DATETIME`을 기준으로 오름차순 정렬합니다.
