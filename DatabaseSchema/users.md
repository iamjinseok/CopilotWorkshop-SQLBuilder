# 테이블명: users

설명: 서비스 사용자 기본 정보를 저장하는 테이블

## 컬럼 정의

| 컬럼명 | 자료형 | PK 여부 | NULL 허용 여부 | 비고 |
|---|---|---|---|---|
| user_id | BIGINT | Y | N | 사용자 고유 ID |
| email | VARCHAR(255) | N | N | 로그인 이메일, 유니크 |
| name | VARCHAR(100) | N | N | 사용자 이름 |
| status | VARCHAR(20) | N | N | ACTIVE, INACTIVE |
| created_at | DATETIME | N | N | 가입 일시 |
