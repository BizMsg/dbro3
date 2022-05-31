---
description: Ufit 서비스 (dbro5)
---

# Agent 소개

### 개요

### Ufit DBro란?

DBro는 (주)다우기술의 UFIT G/W 서비스 사용자에게 제공되는 daemon 형태의 Agent입니다.\
고객의 시스템과 쉽게 연동할 수 있도록 도와주는 Agent로, 고객사의 시스템에 설치되어 daemon 형태로 동작합니다.



### 고객 시스템과 연동

DBro의 실행을 위해서는 Database가 반드시 필요하며, Database에 Record Insert하여 메시지 발송이 가능니다.



### 용어

**SMSGW**

SMS/MMS G/W 를 지칭합니다. 즉, 메시지를 보내면 메시지는 망사업자에게 전달한 뒤\
망사업자로부터 메시지 전송 결과를 받아 되돌려 주는 일을 하는 서버

**JDBC**

자바 프로그램 내에서 데이터베이스 질의를 위한 라이브러리

즉, SQL을 실행하기 위한 자바 API (application programming interface) 입니다.
