# SMS

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
그 외 DB에 대해서는 담당자에게 문의해주세요.
{% endhint %}
