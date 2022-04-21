# 사전 준비

### System

CPU : Pentium 200 이상

전용선 : 56K 이상

HDD : 2GB 의 여유공간 (100만 건당 약 300MB 차지)

**Java JDK 1.6 이상**

DBro를 구동하기 위해 다우기술에 **System OS Version**과 **DB Version**을 알려주어, 해당 Binary File을 받아 설치해야 합니다.



### Database

고객 System과 연동을 위해 ID, Password 등을 미리 알아야 합니다. \
또한 DB사용을 위해서는 JDBC의 URL 과 JDBC Driver Type 을 알아야 합니다.

**연동할 수 있는 Database ID, Password**

기존에 사용하던 ID를 사용하거나 새로운 ID를 만들어서 사용합니다. \
ID 생성 방법은 DBMS의 매뉴얼을 참고

**Database**

DBro가 사용할 Database를 새로 생성합니다. \
기존에 사용하던 것을 사용해도 무방하나 DBro용으로 따로 만들어 사용하는 것을 권장합니다.

**DB 지원 버전 안내**

|    DB    |       지원버전       |             비고             |
| :------: | :--------------: | :------------------------: |
|   MSSQL  | 7.0 , 2000\~2012 |           최신버전 권장          |
|   MYSQL  |    3.23.xx 이상    |           최신버전 권장          |
|  ORACLE  |       7i 이상      | 반드시 서버버전과 클라이언트 버전이 동일해야 함 |
| INFORMIX |      9.x 이상      |           최신버전 권장          |
|    DB2   |      9.xx 이상     |           최신버전 권장          |
|  SYBASE  |       15 이상      |           최신버전 권장          |

{% hint style="info" %}
**\[참고]**

1\. RDBMS서버의 위치가 리모트인 경우 RDBMS가 설치된 운영체제(OS)와는 상관이 없습니다.\
2\. DBro 설치서버에 각 RDBMS 클라이언트 설치 및 설정이 필요합니다. (JDBC 포함)\
3\. RDBMS가 DBro와 같은 시스템에 설치, 운영이 된다면 별도의 클라이언트 프로그램이 필요하지 않을 수도 있습니다. 단, 서버 설치 시 JDBC 드라이버 부분이 설치가 되어 있어야 합니다.
{% endhint %}

### 다우기술 SMSG 접속 환경

실행하기에 앞서 (주)다우기술 Service에 접속 할 수 있는 환경을 미리 알아야 하는데, 다음과 같습니다. \
이 항목은 DBro의 binary를 받을 때 같이 받는 것이므로, 혹시 빠져있다면 다시 연락하여 준비해야 합니다.

**SMSG host IP, Port**

네트워크상의 연결을 확인하기 위한 정보입니다. \
이 값이 있어야 DBro가 실행 시에 접속할 서버의 물리적 위치를 찾을 수 있습니다. (주)다우기술 Service측에서 받은 IP와 Port로 Telnet연결을 시도해서 연결이 되면 정상입니다.

**SMSG ID, Password**

설치된 DBro는 Server에서 인증이 되어 있어야 합니다. \
각 DBro는 고유 ID와 Password를 부여 받게 됩니다. 이 값이 세팅 되지 않으면 접속 후 인증에러를 내며 종료됩니다.