# CopilotWorkshop-SQLBuilder

Copilot Ask 모드와 Agent 모드를 활용해, 테이블 스키마 문서를 기반으로 SQL 쿼리를 생성하는 실습용 레포지토리입니다.

## 1. 레포지토리의 동작 설명

이 레포는 아래 흐름으로 동작합니다.

1. Template 폴더의 양식을 기준으로 테이블 문서를 작성합니다.
2. 작성한 테이블 문서를 DatabaseSchema 폴더에 누적합니다.
3. Ask 모드에서 질문할 때 Copilot이 DatabaseSchema 내용을 참고해 SQL을 생성합니다.
4. 생성된 SQL이 스키마와 일치하는지 검증합니다.

핵심은 자연어 질문만 던지는 것이 아니라, 문서화된 스키마를 근거로 쿼리를 유도하는 것입니다.

## 2. 쿼리를 Ask 모드에서 물어보는 예시

아래 문장은 그대로 복사해서 Ask 모드에 입력할 수 있습니다.

```text
DatabaseSchema를 참고해서 users 테이블의 최근 가입자 10명을 조회하는 SQL을 작성해줘. created_at 내림차순으로 정렬해줘.
```

예상 답변:

```sql
SELECT
	user_id,
	email,
	name,
	status,
	created_at
FROM users
ORDER BY created_at DESC
LIMIT 10;
```

```text
DatabaseSchema를 참고해서 products 테이블에서 재고가 0보다 큰 상품만 조회하는 SQL을 작성해줘. 가격 오름차순으로 정렬해줘.
```

예상 답변:

```sql
SELECT
	product_id,
	product_name,
	price,
	stock_quantity,
	created_at
FROM products
WHERE stock_quantity > 0
ORDER BY price ASC;
```

```text
DatabaseSchema를 참고해서 orders와 users를 조인해 사용자별 주문 건수를 조회하는 SQL을 작성해줘.
```

예상 답변:

```sql
SELECT
	u.user_id,
	u.name,
	COUNT(o.order_id) AS order_count
FROM users u
JOIN orders o
	ON u.user_id = o.user_id
GROUP BY
	u.user_id,
	u.name
ORDER BY order_count DESC;
```

```text
DatabaseSchema를 참고해서 orders와 products를 조인하고 상품별 총 판매수량을 집계하는 SQL을 작성해줘.
```

예상 답변:

```sql
SELECT
	p.product_id,
	p.product_name,
	SUM(o.quantity) AS total_sold_quantity
FROM products p
JOIN orders o
	ON p.product_id = o.product_id
GROUP BY
	p.product_id,
	p.product_name
ORDER BY total_sold_quantity DESC;
```

## 3. 테이블을 추가하는 Agent 모드 예시

아래 문장은 그대로 복사해서 Agent 모드에 입력할 수 있습니다.

```text
Template/table-template.md를 기준으로 DatabaseSchema/reviews.md 파일을 생성해줘.
문서 상단에 테이블명과 설명을 추가하고, 컬럼 표는 컬럼명, 자료형, PK 여부, NULL 허용 여부, 비고 순서로 작성해줘.
reviews 테이블 컬럼은 review_id, user_id, product_id, rating, comment, created_at으로 구성해줘.
user_id는 users.user_id, product_id는 products.product_id 참조 정보를 비고에 표시해줘.
```

## 4. 폴더 구조 설명

```text
.
├─ DatabaseSchema/
│  ├─ users.md
│  ├─ products.md
│  └─ orders.md
├─ Template/
│  └─ table-template.md
└─ README.md
```

- DatabaseSchema: 테이블 정의 문서를 저장하는 공간
- Template: 신규 테이블 문서 양식을 저장하는 공간
- README.md: 실습 방법, Ask/Agent 예시, 구조 설명 문서

파일 네이밍은 소문자 kebab-case를 권장합니다. 예: `order-items.md`
