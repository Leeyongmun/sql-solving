# SQL 문제 풀이

## 사용한 SQL

```sql
SELECT SUM(PRICE) AS TOTAL_PRICE
FROM ITEM_INFO
WHERE
    RARITY = 'LEGEND'
```

## 코드 설명

### 1. 아이템 정보 테이블 조회

```sql
FROM ITEM_INFO
```

`ITEM_INFO` 테이블에서 아이템의 가격과 희귀도 정보를 조회합니다.

문제에서는 조건에 맞는 아이템들의 가격 총합을 구해야 하므로, 아이템 정보가 저장된 `ITEM_INFO` 테이블을 사용합니다.

### 2. 희귀도가 LEGEND인 아이템만 선택

```sql
WHERE
    RARITY = 'LEGEND'
```

`WHERE` 절을 사용해 `RARITY` 값이 `'LEGEND'`인 아이템만 필터링합니다.

이 조건을 만족하는 행들만 가격 합산 대상이 됩니다.

### 3. 조건에 맞는 아이템 가격 합산

```sql
SELECT SUM(PRICE) AS TOTAL_PRICE
```

`SUM()` 함수는 선택된 행들의 `PRICE` 값을 모두 더해 반환합니다.

희귀도가 `LEGEND`인 아이템들의 가격 총합을 구한 뒤, 문제에서 요구하는 컬럼명에 맞게 `TOTAL_PRICE`라는 별칭을 지정합니다.
