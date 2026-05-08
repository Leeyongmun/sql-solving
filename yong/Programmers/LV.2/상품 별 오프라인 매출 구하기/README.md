# SQL 풀이 설명

## 풀이 SQL

```sql
SELECT p.PRODUCT_CODE, sum(p.PRICE * o.SALES_AMOUNT) AS SALES
FROM PRODUCT p
    JOIN OFFLINE_SALE o ON p.PRODUCT_ID = o.PRODUCT_ID
GROUP BY
    p.PRODUCT_CODE
ORDER BY SALES DESC, p.PRODUCT_CODE ASC;
```

## 코드 설명

### 1. 상품 테이블과 오프라인 판매 테이블 연결

```sql
FROM PRODUCT p
    JOIN OFFLINE_SALE o ON p.PRODUCT_ID = o.PRODUCT_ID
```

`PRODUCT` 테이블에는 상품 코드와 가격 정보가 있고, `OFFLINE_SALE` 테이블에는 상품별 판매량 정보가 있습니다.

두 테이블은 `PRODUCT_ID`를 기준으로 연결합니다.

### 2. 상품 코드 조회

```sql
SELECT p.PRODUCT_CODE
```

문제에서 상품 코드별 매출액을 구해야 하므로 `PRODUCT_CODE`를 조회합니다.

### 3. 상품별 매출액 계산

```sql
sum(p.PRICE * o.SALES_AMOUNT) AS SALES
```

각 판매 내역의 매출액은 `상품 가격 * 판매량`으로 계산합니다.

같은 상품 코드에 여러 판매 내역이 있을 수 있으므로 `SUM()`을 사용해서 상품별 전체 매출액을 구합니다.

계산한 매출액 컬럼 이름은 문제 요구사항에 맞게 `SALES`로 지정합니다.

### 4. 상품 코드별 그룹화

```sql
GROUP BY
    p.PRODUCT_CODE
```

상품 코드별 총 매출액을 구해야 하므로 `PRODUCT_CODE`를 기준으로 그룹화합니다.

### 5. 정렬

```sql
ORDER BY SALES DESC, p.PRODUCT_CODE ASC;
```

먼저 매출액 `SALES`를 기준으로 내림차순 정렬합니다.

매출액이 같은 경우에는 상품 코드 `PRODUCT_CODE`를 기준으로 오름차순 정렬합니다.
