# SQL 풀이 설명

## 풀이 SQL

```sql
SELECT i.INGREDIENT_TYPE, SUM(f.TOTAL_ORDER) AS TOTAL_ORDER
FROM FIRST_HALF f
    JOIN ICECREAM_INFO i ON f.FLAVOR = i.FLAVOR
GROUP BY
    i.INGREDIENT_TYPE
ORDER BY TOTAL_ORDER ASC;
```

## 코드 설명

### 1. 상반기 주문 정보와 아이스크림 성분 정보 연결

```sql
FROM FIRST_HALF f
    JOIN ICECREAM_INFO i ON f.FLAVOR = i.FLAVOR
```

`FIRST_HALF` 테이블에는 아이스크림 맛별 상반기 주문량 정보가 들어 있고, `ICECREAM_INFO` 테이블에는 아이스크림 맛별 성분 타입 정보가 들어 있습니다.

성분별 총 주문량을 구하려면 각 맛의 주문량과 성분 정보를 함께 봐야 하므로 `FLAVOR`를 기준으로 두 테이블을 `JOIN`합니다.

### 2. 성분 타입 조회

```sql
SELECT i.INGREDIENT_TYPE
```

문제에서 성분 타입별 총 주문량을 조회하라고 했으므로 `INGREDIENT_TYPE`을 출력합니다.

### 3. 성분 타입별 총 주문량 계산

```sql
SUM(f.TOTAL_ORDER) AS TOTAL_ORDER
```

같은 성분 타입에 여러 아이스크림 맛이 포함될 수 있습니다.

따라서 `SUM()`을 사용해 같은 성분 타입에 속한 아이스크림들의 상반기 주문량을 모두 더합니다.

계산한 총 주문량 컬럼 이름은 문제 요구사항에 맞게 `TOTAL_ORDER`로 지정합니다.

### 4. 성분 타입별 그룹화

```sql
GROUP BY
    i.INGREDIENT_TYPE
```

성분 타입별 총 주문량을 구해야 하므로 `INGREDIENT_TYPE`을 기준으로 그룹화합니다.

### 5. 총 주문량 기준 정렬

```sql
ORDER BY TOTAL_ORDER ASC;
```

문제에서 총 주문량이 작은 순서대로 조회하라고 했으므로 `TOTAL_ORDER`를 기준으로 오름차순 정렬합니다.
