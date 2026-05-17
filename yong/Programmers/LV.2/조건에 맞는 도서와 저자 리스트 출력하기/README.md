# SQL 풀이 설명

## 풀이 SQL

```sql
SELECT b.BOOK_ID, a.AUTHOR_NAME, b.PUBLISHED_DATE
FROM BOOK AS b
    JOIN AUTHOR AS a ON b.AUTHOR_ID = a.AUTHOR_ID
WHERE
    b.CATEGORY = '경제'
ORDER BY PUBLISHED_DATE
```

## 코드 설명

### 1. 도서 테이블과 저자 테이블 연결

```sql
FROM BOOK AS b
    JOIN AUTHOR AS a ON b.AUTHOR_ID = a.AUTHOR_ID
```

`BOOK` 테이블에는 도서 정보와 저자 ID가 있고, `AUTHOR` 테이블에는 저자 ID와 저자 이름이 있습니다.

도서의 저자 이름을 함께 출력해야 하므로 두 테이블을 `AUTHOR_ID` 기준으로 조인합니다.

### 2. 필요한 컬럼 조회

```sql
SELECT b.BOOK_ID, a.AUTHOR_NAME, b.PUBLISHED_DATE
```

문제에서 요구하는 도서 ID, 저자명, 출판일을 조회합니다.

`BOOK_ID`와 `PUBLISHED_DATE`는 `BOOK` 테이블에서 가져오고, `AUTHOR_NAME`은 `AUTHOR` 테이블에서 가져옵니다.

### 3. 경제 카테고리만 필터링

```sql
WHERE
    b.CATEGORY = '경제'
```

조건에 맞는 도서만 출력해야 하므로 `CATEGORY`가 `경제`인 행만 조회합니다.

### 4. 출판일 기준 정렬

```sql
ORDER BY PUBLISHED_DATE
```

결과를 출판일 기준으로 오름차순 정렬합니다.

`ORDER BY`의 기본 정렬 방향은 오름차순이므로 `ASC`를 생략할 수 있습니다.
