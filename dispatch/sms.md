# SMS

## SMS 발송

**SMS 발송 시 반드시 있어야 하는 필드**

* **tran\_pr, tran\_phone, tran\_status, tran\_date, tran\_msg, tran\_type**

**tran\_pr**은 AUTO INCREMENT

**tran\_status** -> 1

**tran\_date** -> 시스템 시간 함수 혹은 현재시간, 예약발송을 원하는 시간을 대입하여야 합니다.



### MSSQL

```sql
Insert into em_tran(
tran_phone, tran_callback, tran_status, tran_date, tran_msg , tran_type) 
values ('010-000-0000', '010-000-0000', '1', getdate(), 'Test Message입니다' ,4);
```

### Oracle

```sql
Insert into em_tran(
tran_pr, tran_phone, tran_callback, tran_status, tran_date, tran_msg , tran_type) 
values(
em_tran_pr.nextval, '010-000-0000', '010-000-0000', '1', sysdate, 'Test Message입니다' ,4);
```

### MYSQL

```sql
Insert into em_tran(
tran_phone, tran_callback, tran_status, tran_date, tran_msg , tran_type) 
values ('010-000-0000', '010-000-0000', '1', sysdate(), 'Test Message입니다' ,4);
```

{% hint style="warning" %}
그 외 DB는 insert 시 tran\_date 값을 현재시간으로 지정 해 주시면 됩니다.
{% endhint %}





## Callback-URL 발송

필수 필드는 위의 SMS 발송과 같습니다.

URL 전송임을 구분하기 위해서 추가로 tran\_type 필드를 조정해주어야 합니다. trantype -> 5

{% hint style="warning" %}
URL전송을 위해서는 특정한 포맷을 맞추어서 DB에 입력하여야 합니다.

URL전송의 경우도 data자체는 tran\_msg에 입력됩니다. URL은 보통 Title과 URL 두 가지 부분으로 이루어져 있기 때문에, 이를 지원하려면 "URL TITLE" 즉, URL이 먼저 나오고 중간에 스페이스 하나로 분리한 후, 타이틀을 써주면 됩니다. URL 이후 최초로 나오는 스페이스가 구분자가 됩니다.\
예를 들어, http://wap.test.co.kr 을 테스트라는 이름으로 전송하고 싶다면

'http://wap.test.co.kr 테스트'

라고 입력하면 됩니다.
{% endhint %}

### **MSSQL**

```sql
Insert into em_tran(
tran_phone, tran_callback, tran_status, tran_date, tran_msg, tran_type ) 

values (
'010-000-0000', '010-000-0000', '1', current, 'http://wap.test.co.kr 테스트',5);
```

### Oracle

```sql
Insert into em_tran(
tran_pr, tran_phone, tran_callback, tran_status, tran_date, tran_msg, tran_type ) 

values (
em_tran_pr.nextval, '010-000-0000', '010-000-0000',
 '1', sysdate, 'http://wap.test.co.kr 테스트',5 );
```

### MYSQL

```sql
Insert into em_tran (
tran_phone, tran_callback, tran_status, tran_date, tran_msg, tran_type ) 

values ('010-000-0000', '010-000-0000', 
'1', sysdate(),'http://wap.test.co.kr 테스트',5);
```

그 외 database에 대해서는 DBMS 담당자에게 문의해주시길 바랍니다.

