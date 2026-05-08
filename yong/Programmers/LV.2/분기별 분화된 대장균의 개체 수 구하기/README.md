# SQL 문법 정리

## 사용한 SQL

```sql
SELECT
    CONCAT(QUARTER(DIFFERENTIATION_DATE), 'Q') AS QUARTER,
    COUNT(*) AS ECOLE_COUNT
FROM ECOLI_DATA
GROUP BY QUARTER(DIFFERENTIATION_DATE)
ORDER BY QUARTER(DIFFERENTIATION_DATE)
```

## 핵심 문법

### 1. QUARTER 함수

```sql
QUARTER(DIFFERENTIATION_DATE)
```

`QUARTER()`는 날짜 값이 몇 분기에 해당하는지 반환하는 함수다.

반환 값은 `1`, `2`, `3`, `4` 중 하나이며, 이 문제에서는 대장균의 분화 날짜를 기준으로 분기를 구하는 데 사용했다.

### 2. CONCAT 함수

```sql
CONCAT(QUARTER(DIFFERENTIATION_DATE), 'Q') AS QUARTER
```

`CONCAT()`은 여러 값을 하나의 문자열로 이어 붙이는 함수다.

`QUARTER(DIFFERENTIATION_DATE)`의 결과에 `'Q'`를 붙여 `1Q`, `2Q`, `3Q`, `4Q` 형태로 출력한다.

### 3. COUNT 집계 함수

```sql
COUNT(*) AS ECOLE_COUNT
```

`COUNT(*)`는 그룹 안에 포함된 전체 행의 개수를 센다.

이 문제에서는 각 분기별로 분화된 대장균 개체 수를 구한다.

### 4. GROUP BY

```sql
GROUP BY QUARTER(DIFFERENTIATION_DATE)
```

`GROUP BY`는 같은 값을 가진 행들을 하나의 그룹으로 묶는다.

여기서는 분화 날짜에서 추출한 분기 기준으로 데이터를 묶어서, 분기별 개체 수를 계산한다.

### 5. ORDER BY

```sql
ORDER BY QUARTER(DIFFERENTIATION_DATE)
```

결과를 분기 기준 오름차순으로 정렬한다.

따라서 `1Q`, `2Q`, `3Q`, `4Q` 순서로 출력된다.
