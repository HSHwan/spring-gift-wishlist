# spring-gift-wishlist

- [1단계 - 유효성 검사 및 예외 처리](#1단계---유효성-검사-및-예외-처리)
  - [기능 요구 사항 정리](#구현-기능-목록)
  - [구현 기능 목록](#구현-기능-목록)


- [2단계 - 인증](#2단계---인증)
  - [기능 요구 사항 정리](#구현-기능-목록-1)
  - [구현 기능 목록](#기능-요구-사항-정리-1)

---

# 1단계 - 유효성 검사 및 예외 처리

## 기능 요구 사항 정리

- 상품을 추가하거나 수정하는 경우, 클라이언트로부터 잘못된 값이 전달될 수 있다. 잘못된 값이 전달되면 클라이언트가 어떤 부분이 왜 잘못되었는지 인지할 수 있도록 응답을 제공한다.

    - 상품 이름은 공백을 포함하여 최대 15자까지 입력할 수 있다.
    - 특수 문자 
      - 가능: ( ), [ ], +, -, &, /, _
      - 그 외 특수 문자 사용 불가
    - "카카오"가 포함된 문구는 담당 MD와 협의한 경우에만 사용할 수 있다.


## 구현 기능 목록

- 상품 이름 유효성 검사
  - 상품 이름의 길이가 15자를 초과하는지 확인
  - 상품 이름에 사용 가능한 특수 문자를 제외한 특수 문자가 있는지 확인
  - "카카오"가 포함되어 있을 경우 담당 MD와 협의한 경우에만 사용할 수 있다는 메시지 출력


- 상품 추가 및 수정에서 잘못된 요청에 대한 응답 제공
  - 상품 이름의 유효성 검사에서 잘못된 부분을 응답 내용에 반영

---

# 2단계 - 인증

## 기능 요구 사항 정리

- 사용자가 로그인하고 사용자별 기능을 사용할 수 있도록 구현한다.

### 예시

- Request

```
POST /login/token HTTP/1.1
content-type: application/json
host: localhost:8080

{
    "password": "password",
    "email": "admin@email.com"
}
```

- Response

```
HTTP/1.1 200 
Content-Type: application/json

{
    "accessToken": ""
}
```

## 구현 기능 목록

- 사용자 로그인 기능
  - 사용자 테이블 구축
  - 로그인 폼 생성
  - 로그인 성공 시 토큰 생성 후 사용자에게 전달
  - 로그인 성공/실패 메시지 출력
---

# 3단계 - 위시 리스트

## 기능 요구 사항 정리

- 이전 단계에서 로그인 후 받은 토큰을 사용하여 사용자별 위시 리스트 기능을 구현한다.
  - 위시 리스트에 등록된 상품 목록을 조회할 수 있다.
  - 위시 리스트에 상품을 추가할 수 있다.
  - 위시 리스트에 담긴 상품을 삭제할 수 있다.

### 실행 결과
사용자 정보는 요청 헤더의 Authorization 필드를 사용한다.
- Authorization: <유형> <자격증명>
```
Authorization: Bearer token
```

## 구현 기능 목록

- 사용자별 위시 리스트 기능
  - 상품 위시 리스트 폼 추가 
  - 위시 리스트의 상품 조회/추가/삭제 기능
  - 위시 리스트에 등록할 수 있는 상품 리스트 조회 기능
  - 로그인을 통해 받은 토큰으로 사용자 인증