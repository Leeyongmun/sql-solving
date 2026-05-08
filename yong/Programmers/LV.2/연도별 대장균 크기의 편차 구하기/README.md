# SQL 문법 정리

## 사용한 SQL

```sql
SELECT
    YEAR(e.DIFFERENTIATION_DATE) AS YEAR,
    m.MAX_SIZE - e.SIZE_OF_COLONY AS YEAR_DEV,
    e.ID
FROM ECOLI_DATA e
JOIN(
    SELECT
        YEAR(DIFFERENTIATION_DATE) AS YEAR,
        MAX(SIZE_OF_COLONY) AS MAX_SIZE
    FROM ECOLI_DATA
    GROUP BY YEAR(DIFFERENTIATION_DATE)
) m
ON YEAR(e.DIFFERENTIATION_DATE) = m.YEAR
ORDER BY YEAR, YEAR_DEV
```

## 핵심 문법

### 1. YEAR 함수

```sql
YEAR(e.DIFFERENTIATION_DATE) AS YEAR
```

`YEAR()`는 날짜 값에서 연도만 추출하는 함수다.

이 문제에서는 `DIFFERENTIATION_DATE`에서 연도를 뽑아 연도별로 데이터를 묶거나 출력하는 데 사용했다.

### 2. 서브쿼리

```sql
JOIN(
    SELECT
        YEAR(DIFFERENTIATION_DATE) AS YEAR,
        MAX(SIZE_OF_COLONY) AS MAX_SIZE
    FROM ECOLI_DATA
    GROUP BY YEAR(DIFFERENTIATION_DATE)
) m
```

`FROM` 절에서 사용하는 서브쿼리다.

먼저 연도별 가장 큰 대장균 크기를 구하고, 그 결과를 `m`이라는 임시 테이블처럼 사용한다.

### 3. GROUP BY

```sql
GROUP BY YEAR(DIFFERENTIATION_DATE)
```

`GROUP BY`는 같은 값을 가진 행들을 하나의 그룹으로 묶는다.

여기서는 분화 날짜의 연도 기준으로 데이터를 묶어서, 각 연도마다 최대 크기를 구할 수 있게 한다.

### 4. MAX 집계 함수

```sql
MAX(SIZE_OF_COLONY) AS MAX_SIZE
```

`MAX()`는 그룹 안에서 가장 큰 값을 반환하는 집계 함수다.

이 문제에서는 각 연도별 가장 큰 대장균 크기를 `MAX_SIZE`로 구한다.

### 5. JOIN

```sql
ON YEAR(e.DIFFERENTIATION_DATE) = m.YEAR
```

원본 테이블 `ECOLI_DATA`와 연도별 최대 크기를 구한 서브쿼리 `m`을 조인한다.

같은 연도끼리 연결해야 하므로 원본 데이터의 연도와 서브쿼리의 `YEAR` 값을 비교한다.

### 6. 산술 연산

```sql
m.MAX_SIZE - e.SIZE_OF_COLONY AS YEAR_DEV
```

각 연도의 최대 대장균 크기에서 현재 행의 대장균 크기를 뺀다.

이 값이 문제에서 요구하는 연도별 크기 편차이며, `YEAR_DEV`라는 컬럼명으로 출력한다.

### 7. ORDER BY

```sql
ORDER BY YEAR, YEAR_DEV
```

결과를 먼저 `YEAR` 기준 오름차순으로 정렬하고, 같은 연도 안에서는 `YEAR_DEV` 기준 오름차순으로 정렬한다.
