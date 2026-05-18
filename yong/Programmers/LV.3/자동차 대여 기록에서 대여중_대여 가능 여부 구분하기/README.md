# SQL 문법 정리

## 사용한 SQL

```sql
SELECT
    CAR_ID,
    CASE
        WHEN MAX(
            CASE
                WHEN '2022-10-16' BETWEEN START_DATE AND END_DATE  THEN 1
                ELSE 0
            END
        ) = 1 THEN '대여중'
        ELSE '대여 가능'
    END
FROM
    CAR_RENTAL_COMPANY_RENTAL_HISTORY
GROUP BY
    CAR_ID
ORDER BY CAR_ID DESC
```

## 핵심 문법

### 1. GROUP BY

```sql
GROUP BY
    CAR_ID
```

자동차별 대여 가능 여부를 구해야 하므로 `CAR_ID` 기준으로 데이터를 묶습니다.

같은 자동차에 여러 대여 기록이 있을 수 있기 때문에, 자동차 ID마다 하나의 결과만 나오도록 그룹화합니다.

### 2. BETWEEN

```sql
'2022-10-16' BETWEEN START_DATE AND END_DATE
```

`BETWEEN`은 특정 값이 시작값과 끝값 사이에 포함되는지 확인합니다.

이 문제에서는 기준 날짜인 `2022-10-16`이 대여 시작일과 대여 종료일 사이에 있으면 해당 자동차가 그 날짜에 대여중이라는 뜻입니다.

### 3. 내부 CASE 표현식

```sql
CASE
    WHEN '2022-10-16' BETWEEN START_DATE AND END_DATE  THEN 1
    ELSE 0
END
```

각 대여 기록이 기준 날짜에 대여중인지 판단합니다.

대여중인 기록이면 `1`, 아니면 `0`을 반환합니다.

### 4. MAX 집계 함수

```sql
MAX(
    CASE
        WHEN '2022-10-16' BETWEEN START_DATE AND END_DATE  THEN 1
        ELSE 0
    END
)
```

자동차별로 여러 대여 기록 중 하나라도 기준 날짜에 대여중이면 `1`이 존재합니다.

`MAX()`를 사용하면 그룹 안에 `1`이 하나라도 있을 때 결과가 `1`이 됩니다.

즉, 해당 자동차가 기준 날짜에 대여중인지 여부를 자동차별로 판단할 수 있습니다.

### 5. 외부 CASE 표현식

```sql
CASE
    WHEN MAX(...) = 1 THEN '대여중'
    ELSE '대여 가능'
END
```

자동차별 판단 결과가 `1`이면 `대여중`을 출력하고, 그렇지 않으면 `대여 가능`을 출력합니다.

### 6. 정렬

```sql
ORDER BY CAR_ID DESC
```

문제 조건에 맞게 자동차 ID를 기준으로 내림차순 정렬합니다.
