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



### DB 전송 시 status 변화

tran\_status : 1 (전송요구)\
tran\_status : 2 (SMSG에 전송됨, 결과 대기중)\
tran\_status : 3 (SMSG에서 결과 받음)\
tran\_date: 전송 요청시간, 이 값이 현재시간과 같거나 과거 ( before\_time 설정시간 ) 이며, tran\_status=‘1’ 인 것이 전송 대상이 된다. 전송 후 tran\_status 는 바로 ‘2’가 된다.
