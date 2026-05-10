# SQL 풀이 설명

## 풀이 SQL

```sql
SELECT f.FLAVOR
FROM FIRST_HALF f
    JOIN (
        SELECT FLAVOR, SUM(TOTAL_ORDER) AS JULY_ORDER
        FROM JULY
        GROUP BY
            FLAVOR
    ) j ON f.flavor = j.flavor
ORDER BY f.TOTAL_ORDER + j.JULY_ORDER DESC
LIMIT 3
```

## 코드 설명

### 1. 7월 주문량을 맛별로 합산

```sql
SELECT FLAVOR, SUM(TOTAL_ORDER) AS JULY_ORDER
FROM JULY
GROUP BY
    FLAVOR
```

`JULY` 테이블에는 7월 아이스크림 주문 정보가 들어 있습니다.

같은 맛의 아이스크림이 여러 출하 번호로 나뉘어 있을 수 있으므로 `FLAVOR`를 기준으로 그룹화한 뒤 `SUM(TOTAL_ORDER)`로 7월 총 주문량을 구합니다.

계산한 7월 주문량은 `JULY_ORDER`라는 이름으로 사용합니다.

### 2. 상반기 주문 정보와 7월 주문 정보 연결

```sql
FROM FIRST_HALF f
    JOIN (
        ...
    ) j ON f.flavor = j.flavor
```

`FIRST_HALF` 테이블은 상반기 주문 정보를 담고 있고, 서브쿼리 `j`는 7월 주문량을 맛별로 합산한 결과입니다.

상반기 주문량과 7월 주문량을 같은 아이스크림 맛 기준으로 더해야 하므로 `FLAVOR`를 기준으로 `JOIN`합니다.

### 3. 조회할 컬럼 선택

```sql
SELECT f.FLAVOR
```

문제에서 총 주문량이 많은 아이스크림 맛을 조회하라고 했으므로 `FLAVOR`만 출력합니다.

### 4. 총 주문량 기준 정렬

```sql
ORDER BY f.TOTAL_ORDER + j.JULY_ORDER DESC
```

총 주문량은 상반기 주문량인 `f.TOTAL_ORDER`와 7월 주문량인 `j.JULY_ORDER`를 더해서 계산합니다.

주문량이 많은 아이스크림부터 조회해야 하므로 계산한 총 주문량을 기준으로 내림차순 정렬합니다.

### 5. 상위 3개만 조회

```sql
LIMIT 3
```

문제에서 총 주문량이 큰 순서대로 상위 3개의 맛을 조회하라고 했으므로 `LIMIT 3`을 사용합니다.
