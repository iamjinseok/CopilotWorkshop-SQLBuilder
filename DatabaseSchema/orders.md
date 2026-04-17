# 테이블명: orders

설명: 사용자 주문 이력을 저장하는 테이블

## 컬럼 정의

| 컬럼명 | 자료형 | PK 여부 | NULL 허용 여부 | 비고 |
|---|---|---|---|---|
| order_id | BIGINT | Y | N | 주문 고유 ID |
| user_id | BIGINT | N | N | users.user_id 참조 |
| product_id | BIGINT | N | N | products.product_id 참조 |
| quantity | INT | N | N | 주문 수량 |
| ordered_at | DATETIME | N | N | 주문 일시 |
