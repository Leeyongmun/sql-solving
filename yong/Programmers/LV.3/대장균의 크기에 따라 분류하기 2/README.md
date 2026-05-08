# SQL 문법 정리

## 사용한 SQL

```sql
SELECT 
    ID, 
    CASE NTILE(4) OVER (ORDER BY SIZE_OF_COLONY DESC)
        WHEN 1 THEN 'CRITICAL'
        WHEN 2 THEN 'HIGH'
        WHEN 3 THEN 'MEDIUM'
        ELSE 'LOW'
    END AS COLONY_NAME
FROM ECOLI_DATA
ORDER BY ID
```

## 핵심 문법

### 1. 윈도우 함수

```sql
NTILE(4) OVER (ORDER BY SIZE_OF_COLONY DESC)
```

윈도우 함수는 행들을 특정 기준으로 정렬하거나 그룹화한 뒤, 각 행에 대한 계산 결과를 반환한다.

이 쿼리에서는 `NTILE(4)`를 사용해서 전체 데이터를 4개 구간으로 나눈다.

### 2. NTILE

```sql
NTILE(4)
```

`NTILE(n)`은 정렬된 결과를 `n`개의 그룹으로 최대한 균등하게 나누고, 각 행에 그룹 번호를 부여한다.

이 문제에서는 `4`개의 그룹으로 나누므로 결과는 `1`, `2`, `3`, `4` 중 하나가 된다.

### 3. OVER와 ORDER BY

```sql
OVER (ORDER BY SIZE_OF_COLONY DESC)
```

`OVER`는 윈도우 함수가 어떤 기준으로 동작할지 정한다.

`SIZE_OF_COLONY DESC`는 대장균 크기가 큰 순서대로 정렬한다는 뜻이다.

따라서 가장 큰 그룹이 `NTILE` 결과 `1`번 그룹이 된다.

### 4. CASE 표현식

```sql
CASE NTILE(4) OVER (ORDER BY SIZE_OF_COLONY DESC)
    WHEN 1 THEN 'CRITICAL'
    WHEN 2 THEN 'HIGH'
    WHEN 3 THEN 'MEDIUM'
    ELSE 'LOW'
END AS COLONY_NAME
```

`CASE`는 조건에 따라 다른 값을 반환하는 표현식이다.

이 쿼리에서는 `NTILE(4)`의 결과에 따라 그룹명을 붙인다.

- `1`: `CRITICAL`
- `2`: `HIGH`
- `3`: `MEDIUM`
- `4`: `LOW`

### 5. 컬럼 별칭

```sql
END AS COLONY_NAME
```

`AS`를 사용해서 계산 결과 컬럼의 이름을 `COLONY_NAME`으로 지정한다.

### 6. ORDER BY

```sql
ORDER BY ID
```

최종 결과를 `ID` 기준 오름차순으로 정렬한다.
