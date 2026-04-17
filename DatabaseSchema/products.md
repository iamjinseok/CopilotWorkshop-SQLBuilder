# 테이블명: products

설명: 판매 상품 정보를 저장하는 테이블

## 컬럼 정의

| 컬럼명 | 자료형 | PK 여부 | NULL 허용 여부 | 비고 |
|---|---|---|---|---|
| product_id | BIGINT | Y | N | 상품 고유 ID |
| product_name | VARCHAR(200) | N | N | 상품명 |
| price | DECIMAL(10,2) | N | N | 상품 가격 |
| stock_quantity | INT | N | N | 재고 수량 |
| created_at | DATETIME | N | N | 등록 일시 |
