# 메시지 발송

### DB 전송 시 status 변화

tran\_status 는 다음과 같은 상태 변화도를 갖습니다.

tran\_status : 1 (전송요구)\
tran\_status : 2 (SMSGW에 전송됨, 결과 대기중)\
tran\_status : 3 (SMSGW에서 결과 받음)

![](<../.gitbook/assets/image (2) (1) (1).png>)

{% hint style="info" %}
tran\_date: 전송 요청시간, 이 값이 현재시간과 같거나 과거 ( before\_time 설정시간 ) 이며, tran\_status='1' 인 것이 전송 대상이 됩다. 전송 후 tran\_status 는 바로 '2'가 됩니다.
{% endhint %}

{% hint style="warning" %}
상태값 '3'은 '1' 과 '2' 상태에서 올 수 있는데, '1' 에서 바로 '3'으로 되는 경우는 Phone 번호가 망 식별번호 오류 (011,016,017,018,019 가 아닌)인 경우와 메시지에 내용이 없는 경우에 발생합니다.
{% endhint %}
