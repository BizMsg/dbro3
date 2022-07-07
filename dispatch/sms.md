# SMS

## SMS 발송

**SMS 발송 시 반드시 있어야 하는 필드**

* **tran\_pr, tran\_phone, tran\_status, tran\_date, tran\_msg, tran\_type**

**tran\_pr** -> AUTO INCREMENT

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

