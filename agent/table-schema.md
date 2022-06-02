# Table Schema

DBro는 실행되면 바로 트랜잭션 테이블(em\_tran\_,\_ em\_tran\_mms)이 존재하는지 확인하며, 없을 경우 다음과 같은 스키마로 테이블을 생성합니다.

### em\_tran (발송 테이블)

|       필드 명       | 필수입력 여부 |                               내용                              |
| :--------------: | :-----: | :-----------------------------------------------------------: |
|   **tran\_pr**   |    필수   |             자동 증가하는 것으로 em\_tran의 primary key가 된다.            |
|   trna\_refkey   |         |              참조용으로 사용되는 것으로 메시지 전송 시에는 사용되지 않는다.              |
|     tran\_id     |         |              참조용으로 사용되는 것으로 메시지 전송 시에는 사용되지 않는다.              |
|  **tran\_phone** |    필수   |                            수신자 전화번호                           |
|  tran\_callback  |    필수   |         <p>송신자 전화번호<br>(발신번호 등록 처리된 번호만 사용 가능합니다)</p>         |
| **tran\_status** |         |                             메시지 상태                            |
|  **tran\_date**  |    필수   |                     메시지 접수시간 ( 전송 요청 시간 )                     |
|  tran\_rsltdate  |         |                  핸드폰에 전달된 시간 ( 통신사에서 전달한 시간 )                 |
| tran\_reportdate |         |                          전송 결과 수신 시간                          |
|    tran\_rslt    |         |                     전송 결과 코드 (결과코드 표 참조 )                     |
|     tran\_net    |         |                               -                               |
|   **tran\_msg**  |    필수   |              전송 메시지 (MMS 의 경우,MMS\_BODY 입력 값 발송 )             |
|    tran\_etc1    |         |    <p>사용자 임의로 사용할 수 있는 필드</p><p>SMS 전송 시에는 전혀 사용되지 않음.</p>    |
|    tran\_etc2    |         |    <p>사용자 임의로 사용할 수 있는 필드</p><p>SMS 전송 시에는 전혀 사용되지 않음.</p>    |
|    tran\_etc3    |         |    <p>사용자 임의로 사용할 수 있는 필드</p><p>SMS 전송 시에는 전혀 사용되지 않음.</p>    |
|    tran\_etc4    |         |    <p>사용자 임의로 사용할 수 있는 필드</p><p>SMS 전송 시에는 전혀 사용되지 않음.</p>    |
|  **tran\_type**  |    필수   | <p>메시지 발송 타입<br>(4: SMS 전송, 5: Callback-URL 전송, 6: MMS 전)</p> |

### em\_tran\_mms (MMS 컨텐츠 테이블)

|       필드 명      | 필수입력 여부 |                                             내용                                             |
| :-------------: | :-----: | :----------------------------------------------------------------------------------------: |
|     mms\_seq    |    필수   |                         자동 증가하는 것으로 em\_tran\_mms의 primary key가 된다.                        |
|    file\_cnt    |    필수   |                                    MMS전송 시 첨부파일 개수 (1이상)                                   |
|    build\_yn    |    -    | <p>dbro.jar 프로그램 내부에서 사용 된다. 입력 불가</p><p>(0:정상으로 빌드 되었으며 사용가능,<br>9:빌드 에러 발생 메시지 발송불가)</p> |
|    mms\_body    |    옵션   |                                        장문 전송 시 본문 내용                                       |
|   mms\_subject  |    필수   |                                           메시지 제목                                           |
|   file\_type1   |    옵션   |                            MMS파일타입. (IMG, TXT, ADO, MOV) , 생략가능                            |
|   file\_type2   |    옵션   |                                       MMS 파일타입 생략 가능                                       |
|   file\_type3   |    옵션   |                                       MMS 파일타입 생략 가능                                       |
|   file\_type4   |    옵션   |                                       MMS 파일타입 생략 가능                                       |
|   file\_type5   |    옵션   |                                       MMS 파일타입 생략 가능                                       |
|   file\_name1   |    옵션   |                                   MMS 파일경로를 포함한 파일명 생략가능                                   |
|   file\_name2   |    옵션   |                                   MMS 파일경로를 포함한 파일명 생략가능                                   |
|   file\_name3   |    옵션   |                                   MMS 파일경로를 포함한 파일명 생략가능                                   |
|   file\_name4   |    옵션   |                                   MMS 파일경로를 포함한 파일명 생략가능                                   |
|   file\_name5   |    옵션   |                                   MMS 파일경로를 포함한 파일명 생략가능                                   |
|  service\_dep1  |    옵션   |                                      MMS파일 서비스통신사 생략가능                                     |
|  service\_dep2  |    옵션   |                                      MMS파일 서비스통신사 생략가능                                     |
|  service\_dep3  |    옵션   |                                      MMS파일 서비스통신사 생략가능                                     |
|  service\_dep4  |    옵션   |                                      MMS파일 서비스통신사 생략가능                                     |
|  service\_dep5  |    옵션   |                                      MMS파일 서비스통신사 생략가능                                     |
| skn\_file\_name |    -    |                                dbro.jar 프로그램 내부에서 사용, 입력 불가                                |

### MSSQL

**em\_tran**

|       NAME       |  NULL 여부 |     TYPE     |
| :--------------: | :------: | :----------: |
|   **tran\_pr**   | NOT NULL |    INT(11)   |
|   trna\_refkey   |          |  VARCHAR(20) |
|     tran\_id     |          |  VARCHAR(20) |
|  **tran\_phone** | NOT NULL |  VARCHAR(15) |
|  tran\_callback  | NOT NULL |  VARCHAR(15) |
| **tran\_status** |          |    CHAR(1)   |
|  **tran\_date**  | NOT NULL |   DATETIME   |
|  tran\_rsltdate  |          |   DATETIME   |
| tran\_reportdate |          |   DATETIME   |
|    tran\_rslt    |          |    CHAR(1)   |
|     tran\_net    |          |    CHAR(3)   |
|   **tran\_msg**  |          | VARCHAR(255) |
|    tran\_etc1    |          |  VARCHAR(64) |
|    tran\_etc2    |          |  VARCHAR(16) |
|    tran\_etc3    |          |  VARCHAR(16) |
|    tran\_etc4    |          |    INT(10)   |
|  **tran\_type**  | NOT NULL |    INT(5)    |

***

**em\_tran\_mms**

|       NAME      |  NULL 여부 |      TYPE     |
| :-------------: | :------: | :-----------: |
|     mms\_seq    | NOT NULL |    INT(10)    |
|    file\_cnt    | NOT NULL |      INT      |
|    build\_yn    |          |    CHAR(1)    |
|    mms\_body    |          | VARCHAR(2000) |
|   mms\_subject  |          |  VARCHAR(40)  |
|   file\_type1   |          |   VARCHAR(3)  |
|   file\_type2   |          |   VARCHAR(3)  |
|   file\_type3   |          |   VARCHAR(3)  |
|   file\_type4   |          |   VARCHAR(3)  |
|   file\_type5   |          |   VARCHAR(3)  |
|   file\_name1   |          |  VARCHAR(100) |
|   file\_name2   |          |  VARCHAR(100) |
|   file\_name3   |          |  VARCHAR(100) |
|   file\_name4   |          |  VARCHAR(100) |
|   file\_name5   |          |  VARCHAR(100) |
|  service\_dep1  |          |   VARCHAR(3)  |
|  service\_dep2  |          |   VARCHAR(3)  |
|  service\_dep3  |          |   VARCHAR(3)  |
|  service\_dep4  |          |   VARCHAR(3)  |
|  service\_dep5  |          |   VARCHAR(3)  |
| skn\_file\_name |          |  VARCHAR(100) |

### Oracle

**em\_tran**

|       NAME       |  NULL 여부 |      TYPE     |
| :--------------: | :------: | :-----------: |
|   **tran\_pr**   | NOT NULL |   NUMBER(11)  |
|   trna\_refkey   |          |  VARCHAR2(20) |
|     tran\_id     |          |  VARCHAR2(20) |
|  **tran\_phone** | NOT NULL |  VARCHAR2(15) |
|  tran\_callback  | NOT NULL |  VARCHAR2(15) |
| **tran\_status** |          |    CHAR(1)    |
|  **tran\_date**  | NOT NULL |      DATE     |
|  tran\_rsltdate  |          |      DATE     |
| tran\_reportdate |          |      DATE     |
|    tran\_rslt    |          |    CHAR(1)    |
|     tran\_net    |          |    CHAR(3)    |
|   **tran\_msg**  |          | VARCHAR2(255) |
|    tran\_etc1    |          |  VARCHAR264)  |
|    tran\_etc2    |          |  VARCHAR2(16) |
|    tran\_etc3    |          |  VARCHAR2(16) |
|    tran\_etc4    |          |   NUMBER(10)  |
|  **tran\_type**  | NOT NULL |   NUMBER(5)   |

**em\_tran\_mms**

|       NAME      |  NULL 여부 |      TYPE     |
| :-------------: | :------: | :-----------: |
|     mms\_seq    | NOT NULL |   NUMBER(10)  |
|    file\_cnt    | NOT NULL |     NUMBER    |
|    build\_yn    |          |    CHAR(1)    |
|    mms\_body    |          | VARCHAR(2000) |
|   mms\_subject  |          |  VARCHAR2(40) |
|   file\_type1   |          |  VARCHAR2(3)  |
|   file\_type2   |          |  VARCHAR2(3)  |
|   file\_type3   |          |  VARCHAR2(3)  |
|   file\_type4   |          |  VARCHAR2(3)  |
|   file\_type5   |          |  VARCHAR2(3)  |
|   file\_name1   |          | VARCHAR2(100) |
|   file\_name2   |          | VARCHAR2(100) |
|   file\_name3   |          | VARCHAR2(100) |
|   file\_name4   |          | VARCHAR2(100) |
|   file\_name5   |          | VARCHAR2(100) |
|  service\_dep1  |          |  VARCHAR2(3)  |
|  service\_dep2  |          |  VARCHAR2(3)  |
|  service\_dep3  |          |  VARCHAR2(3)  |
|  service\_dep4  |          |  VARCHAR2(3)  |
|  service\_dep5  |          |  VARCHAR2(3)  |
| skn\_file\_name |          | VARCHAR2(100) |

### MYSQL

**em\_tran**

|       NAME       |  NULL 여부 |     TYPE     |
| :--------------: | :------: | :----------: |
|   **tran\_pr**   | NOT NULL |    INT(11)   |
|   trna\_refkey   |          |  VARCHAR(20) |
|     tran\_id     |          |  VARCHAR(20) |
|  **tran\_phone** | NOT NULL |  VARCHAR(15) |
|  tran\_callback  | NOT NULL |  VARCHAR(15) |
| **tran\_status** |          |    CHAR(1)   |
|  **tran\_date**  | NOT NULL |   DATETIME   |
|  tran\_rsltdate  |          |   DATETIME   |
| tran\_reportdate |          |   DATETIME   |
|    tran\_rslt    |          |    CHAR(1)   |
|     tran\_net    |          |    CHAR(3)   |
|   **tran\_msg**  |          | VARCHAR(255) |
|    tran\_etc1    |          |  VARCHAR(64) |
|    tran\_etc2    |          |  VARCHAR(16) |
|    tran\_etc3    |          |  VARCHAR(16) |
|    tran\_etc4    |          |    INT(10)   |
|  **tran\_type**  | NOT NULL |    INT(5)    |

**em\_tran\_mms**

***

|       NAME      |  NULL 여부 |      TYPE     |
| :-------------: | :------: | :-----------: |
|     mms\_seq    | NOT NULL |    INT(10)    |
|    file\_cnt    | NOT NULL |      INT      |
|    build\_yn    |          |    CHAR(1)    |
|    mms\_body    |          | VARCHAR(2000) |
|   mms\_subject  |          |  VARCHAR(40)  |
|   file\_type1   |          |   VARCHAR(3)  |
|   file\_type2   |          |   VARCHAR(3)  |
|   file\_type3   |          |   VARCHAR(3)  |
|   file\_type4   |          |   VARCHAR(3)  |
|   file\_type5   |          |   VARCHAR(3)  |
|   file\_name1   |          |  VARCHAR(100) |
|   file\_name2   |          |  VARCHAR(100) |
|   file\_name3   |          |  VARCHAR(100) |
|   file\_name4   |          |  VARCHAR(100) |
|   file\_name5   |          |  VARCHAR(100) |
|  service\_dep1  |          |   VARCHAR(3)  |
|  service\_dep2  |          |   VARCHAR(3)  |
|  service\_dep3  |          |   VARCHAR(3)  |
|  service\_dep4  |          |   VARCHAR(3)  |
|  service\_dep5  |          |   VARCHAR(3)  |
| skn\_file\_name |          |  VARCHAR(100) |

### SYBASE

**em\_tran**

|       NAME       |  NULL 여부 |     TYPE     |
| :--------------: | :------: | :----------: |
|   **tran\_pr**   | NOT NULL |  NUMERIC(11) |
|   trna\_refkey   |          |  VARCHAR(20) |
|     tran\_id     |          |  VARCHAR(20) |
|  **tran\_phone** | NOT NULL |  VARCHAR(15) |
|  tran\_callback  | NOT NULL |  VARCHAR(15) |
| **tran\_status** |          |    CHAR(1)   |
|  **tran\_date**  | NOT NULL |   DATETIME   |
|  tran\_rsltdate  |          |   DATETIME   |
| tran\_reportdate |          |   DATETIME   |
|    tran\_rslt    |          |    CHAR(1)   |
|     tran\_net    |          |    CHAR(3)   |
|   **tran\_msg**  |          | VARCHAR(255) |
|    tran\_etc1    |          |  VARCHAR(64) |
|    tran\_etc2    |          |  VARCHAR(16) |
|    tran\_etc3    |          |  VARCHAR(16) |
|    tran\_etc4    |          |  NUMERIC(10) |
|  **tran\_type**  | NOT NULL |  NUMERIC(5)  |

***

**em\_tran\_mms**

|       NAME      |  NULL 여부 |      TYPE     |
| :-------------: | :------: | :-----------: |
|     mms\_seq    | NOT NULL |  NUMERIC(10)  |
|    file\_cnt    | NOT NULL |    INTEGER    |
|    build\_yn    |          |    CHAR(1)    |
|    mms\_body    |          | VARCHAR(2000) |
|   mms\_subject  |          |  VARCHAR(40)  |
|   file\_type1   |          |   VARCHAR(3)  |
|   file\_type2   |          |   VARCHAR(3)  |
|   file\_type3   |          |   VARCHAR(3)  |
|   file\_type4   |          |   VARCHAR(3)  |
|   file\_type5   |          |   VARCHAR(3)  |
|   file\_name1   |          |  VARCHAR(100) |
|   file\_name2   |          |  VARCHAR(100) |
|   file\_name3   |          |  VARCHAR(100) |
|   file\_name4   |          |  VARCHAR(100) |
|   file\_name5   |          |  VARCHAR(100) |
|  service\_dep1  |          |   VARCHAR(3)  |
|  service\_dep2  |          |   VARCHAR(3)  |
|  service\_dep3  |          |   VARCHAR(3)  |
|  service\_dep4  |          |   VARCHAR(3)  |
|  service\_dep5  |          |   VARCHAR(3)  |
| skn\_file\_name |          |  VARCHAR(100) |

### DB2

**em\_tran**

|       NAME       |  NULL 여부 |     TYPE     |
| :--------------: | :------: | :----------: |
|   **tran\_pr**   | NOT NULL |    BIGINT    |
|   trna\_refkey   |          |  VARCHAR(20) |
|     tran\_id     |          |  VARCHAR(20) |
|  **tran\_phone** | NOT NULL |  VARCHAR(15) |
|  tran\_callback  | NOT NULL |  VARCHAR(15) |
| **tran\_status** |          |    CHAR(1)   |
|  **tran\_date**  | NOT NULL |   TIMESTAMP  |
|  tran\_rsltdate  |          |   TIMESTAMP  |
| tran\_reportdate |          |   TIMESTAMP  |
|    tran\_rslt    |          |    CHAR(1)   |
|     tran\_net    |          |    CHAR(3)   |
|   **tran\_msg**  |          | VARCHAR(255) |
|    tran\_etc1    |          |  VARCHAR(64) |
|    tran\_etc2    |          |  VARCHAR(16) |
|    tran\_etc3    |          |  VARCHAR(16) |
|    tran\_etc4    |          |    BIGINT    |
|  **tran\_type**  | NOT NULL |    INTEGER   |

**em\_tran\_mms**

|       NAME      |  NULL 여부 |      TYPE     |
| :-------------: | :------: | :-----------: |
|     mms\_seq    | NOT NULL |     BIGINT    |
|    file\_cnt    | NOT NULL |    INTEGER    |
|    build\_yn    |          |    CHAR(1)    |
|    mms\_body    |          | VARCHAR(2000) |
|   mms\_subject  |          |  VARCHAR(40)  |
|   file\_type1   |          |   VARCHAR(3)  |
|   file\_type2   |          |   VARCHAR(3)  |
|   file\_type3   |          |   VARCHAR(3)  |
|   file\_type4   |          |   VARCHAR(3)  |
|   file\_type5   |          |   VARCHAR(3)  |
|   file\_name1   |          |  VARCHAR(100) |
|   file\_name2   |          |  VARCHAR(100) |
|   file\_name3   |          |  VARCHAR(100) |
|   file\_name4   |          |  VARCHAR(100) |
|   file\_name5   |          |  VARCHAR(100) |
|  service\_dep1  |          |   VARCHAR(3)  |
|  service\_dep2  |          |   VARCHAR(3)  |
|  service\_dep3  |          |   VARCHAR(3)  |
|  service\_dep4  |          |   VARCHAR(3)  |
|  service\_dep5  |          |   VARCHAR(3)  |
| skn\_file\_name |          |  VARCHAR(100) |

### Informix

**em\_tran**

|       NAME       |  NULL 여부 |           TYPE          |
| :--------------: | :------: | :---------------------: |
|   **tran\_pr**   | NOT NULL |          SERIAL         |
|   trna\_refkey   |          |      VARCHAR(20,0)      |
|     tran\_id     |          |      VARCHAR(20,0)      |
|  **tran\_phone** | NOT NULL |      VARCHAR(15,0)      |
|  tran\_callback  | NOT NULL |      VARCHAR(15,0)      |
| **tran\_status** |          |         CHAR(1)         |
|  **tran\_date**  | NOT NULL | DATETIME YEAR TO SECOND |
|  tran\_rsltdate  |          | DATETIME YEAR TO SECOND |
| tran\_reportdate |          | DATETIME YEAR TO SECOND |
|    tran\_rslt    |          |         CHAR(1)         |
|     tran\_net    |          |         CHAR(3)         |
|   **tran\_msg**  |          |      VARCHAR(255,0)     |
|    tran\_etc1    |          |      VARCHAR(64,0)      |
|    tran\_etc2    |          |      VARCHAR(16,0)      |
|    tran\_etc3    |          |      VARCHAR(16,0)      |
|    tran\_etc4    |          |         INTEGER         |
|  **tran\_type**  | NOT NULL |         INTEGER         |

**em\_tran\_mms**

|       NAME      |  NULL 여부 |       TYPE      |
| :-------------: | :------: | :-------------: |
|     mms\_seq    | NOT NULL |     INTEGER     |
|    file\_cnt    | NOT NULL |     INTEGER     |
|    build\_yn    |          |     CHAR(1)     |
|    mms\_body    |          | VARCHAR(2000,0) |
|   mms\_subject  |          |  VARCHAR(40,0)  |
|   file\_type1   |          |   VARCHAR(3,0)  |
|   file\_type2   |          |   VARCHAR(3,0)  |
|   file\_type3   |          |   VARCHAR(3,0)  |
|   file\_type4   |          |   VARCHAR(3,0)  |
|   file\_type5   |          |   VARCHAR(3,0)  |
|   file\_name1   |          |  VARCHAR(100,0) |
|   file\_name2   |          |  VARCHAR(100,0) |
|   file\_name3   |          |  VARCHAR(100,0) |
|   file\_name4   |          |  VARCHAR(100,0) |
|   file\_name5   |          |  VARCHAR(100,0) |
|  service\_dep1  |          |   VARCHAR(3,0)  |
|  service\_dep2  |          |   VARCHAR(3,0)  |
|  service\_dep3  |          |   VARCHAR(3,0)  |
|  service\_dep4  |          |   VARCHAR(3,0)  |
|  service\_dep5  |          |   VARCHAR(3,0)  |
| skn\_file\_name |          |  VARCHAR(100,0) |
