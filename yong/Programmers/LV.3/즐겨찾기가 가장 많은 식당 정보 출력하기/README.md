# 즐겨찾기가 가장 많은 식당 정보 출력하기

## 문제 요약

`REST_INFO` 테이블에서 음식 종류별로 즐겨찾기 수가 가장 많은 식당의 정보를 조회한다.

- 출력 컬럼은 `FOOD_TYPE`, `REST_ID`, `REST_NAME`, `FAVORITES`이다.
- 음식 종류별로 `FAVORITES`가 가장 큰 식당을 찾아야 한다.
- 결과는 `FOOD_TYPE`을 기준으로 내림차순 정렬한다.

## SQL

```sql
SELECT R.FOOD_TYPE, R.REST_ID, R.REST_NAME, R.FAVORITES
FROM REST_INFO R
    JOIN (
        SELECT FOOD_TYPE, MAX(FAVORITES) AS FAVORITES
        FROM REST_INFO
        GROUP BY
            FOOD_TYPE
    ) M ON R.FOOD_TYPE = M.FOOD_TYPE
    AND R.FAVORITES = M.FAVORITES
ORDER BY R.FOOD_TYPE DESC
```

## 풀이 설명

먼저 음식 종류별로 가장 큰 즐겨찾기 수를 구한다.

```sql
SELECT FOOD_TYPE, MAX(FAVORITES) AS FAVORITES
FROM REST_INFO
GROUP BY FOOD_TYPE
```

`GROUP BY FOOD_TYPE`으로 음식 종류별 그룹을 만들고, `MAX(FAVORITES)`를 사용해 각 음식 종류에서 가장 높은 즐겨찾기 수를 찾는다.

그다음 이 결과를 원본 `REST_INFO` 테이블과 조인한다.

```sql
JOIN (
    SELECT FOOD_TYPE, MAX(FAVORITES) AS FAVORITES
    FROM REST_INFO
    GROUP BY FOOD_TYPE
) M ON R.FOOD_TYPE = M.FOOD_TYPE
AND R.FAVORITES = M.FAVORITES
```

조인 조건은 두 가지이다.

- `R.FOOD_TYPE = M.FOOD_TYPE`: 같은 음식 종류끼리 비교한다.
- `R.FAVORITES = M.FAVORITES`: 해당 음식 종류의 최대 즐겨찾기 수와 같은 식당만 남긴다.

이렇게 하면 각 음식 종류에서 즐겨찾기 수가 가장 많은 식당의 `REST_ID`, `REST_NAME`까지 함께 조회할 수 있다.

마지막으로 문제 조건에 맞게 음식 종류를 기준으로 내림차순 정렬한다.

```sql
ORDER BY R.FOOD_TYPE DESC
```

## 핵심 포인트

음식 종류별 최대 즐겨찾기 수만 구하면 식당 이름이나 ID를 바로 알 수 없다. 따라서 먼저 `GROUP BY`와 `MAX()`로 종류별 최대값을 구한 뒤, 원본 테이블과 다시 조인해서 최대값을 가진 식당의 전체 정보를 가져오는 방식으로 해결한다.
