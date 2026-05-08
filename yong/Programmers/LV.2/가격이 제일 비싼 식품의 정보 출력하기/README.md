# SQL 문제 풀이

## 사용한 SQL

```sql
SELECT *
FROM FOOD_PRODUCT
WHERE (
    SELECT MAX(PRICE)
    FROM FOOD_PRODUCT f
) = PRICE
```

## 코드 설명

### 1. 전체 식품 테이블 조회

```sql
FROM FOOD_PRODUCT
```

`FOOD_PRODUCT` 테이블에서 식품 정보를 조회합니다.

이 문제는 가장 비싼 식품의 정보를 출력해야 하므로, 기본 대상 테이블은 `FOOD_PRODUCT`입니다.

### 2. 최고 가격 구하기

```sql
SELECT MAX(PRICE)
FROM FOOD_PRODUCT f
```

서브쿼리로 `FOOD_PRODUCT` 테이블의 `PRICE` 중 가장 큰 값을 구합니다.

`MAX()` 함수는 컬럼의 최댓값을 반환하므로, 가장 비싼 식품의 가격을 찾는 데 사용합니다.

### 3. 최고 가격과 같은 행만 선택

```sql
WHERE (
    SELECT MAX(PRICE)
    FROM FOOD_PRODUCT f
) = PRICE
```

서브쿼리에서 구한 최고 가격과 현재 행의 `PRICE`가 같은 데이터만 남깁니다.

즉, 가장 비싼 가격을 가진 식품의 정보만 결과로 출력됩니다.

같은 최고 가격을 가진 식품이 여러 개라면, 해당 식품들이 모두 조회됩니다.
