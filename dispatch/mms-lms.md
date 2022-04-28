# LMS/MMS

멀티미디어의 전송과 관리를 위하여 기존의 em\_tran 테이블은 전송에 관련된 정보를 보관하고, em\_tran\_mms는 콘텐트에 대한 정보를 관리합니다.

즉, 콘텐트 정보를 사전에 작성하여 다수의 대상에게 동일한 내용을 한번에 보낼 수 있습니다.\
\
MMS전송 시 em\_tran의 tran\_type을 '6'으로 조정해야 하고, tran\_etc4의 필드에 em\_tran\_mms의 mms\_seq를 참조합니다.

메시지 전송 전에 em\_tran\_mms의 정보가 입력이 되어야 하며, 콘텐트 정보는 DBro에서 참조 가능한 위치에 있어야 합니다.



### 파일 타입

file\_type 정보&#x20;

**TXT** &#x20;

MMS의 본문 정보\
규격: 최대 2,000byte 이내의 텍스트 파일, 코드형식은 EUC-KR\
\* 핸드폰에서 표시 불가능한 특수문자를 입력하는 경우 전송이 실패될 수 있음\
\* 본문의 작성은 자유롭게 작성이 가능



**IMG**

MMS의 이미지 정보

규격: 해상도->220 x 184(권장), 파일크기:->40Kbyte이하, JPG \*이미지의 해상도는 변경이 가능하지만 특정 폰에서 표시를 하지 못하는 경우가 있음(“콘텐트에 오류가 있음”으로 표기됨)\
\*이미지는 최대 3장까지 지정이 가능. 단, 모든 통신사에 3장이 모두 전송이 되는 것은 아님(수신 폰의 기종이나 통신사의 지원 여부를 확인 할 것)



**ADO**

MMS의 오디오 정보

규격: 샘플링 16KHz 이하의 MA3형식\
\*전송은 되지만 일부 단말기는 포맷을 지원하지 않음



**MOV**&#x20;

MMS의 비디오 정보\
규격: 해상도-> 220x184(권장), SKT:->파일크기 350KB 이하, 파일형식 .skm, KT/LGT->파일크기 300KB 이하, 파일형식 .k3g



### **파일 이름**

DBro에서 참조 가능한 위치에 있는 File의 Full Path입니다.

{% hint style="danger" %}
발송하는 시점에 콘텐츠 파일을 참조하게 되므로 발송 전까지는 해당 콘텐츠를 삭제하거나 이동하지 마십시오.
{% endhint %}

****

### **service\_dep**

ALL&#x20;

file\_type **** , file\_name 에 지정한 콘텐트가 모든 통신사와 호환이 되는 경우



### 발송 쿼리

**Oracle**

```sql
INSERT INTO em_tran_mms(
mms_seq, file_cnt, mms_body, mms_subject, , file_type1, file_name1,service_dep1)

VALUES(
em_tran_mms_seq.nextval,2 , '본문 내용','메시지 제목’,
 'IMG','D:\MMSTestFile\01.IMG', 'ALL' );
```

**MYSQL**

```sql
INSERT INTO em_tran_mms (mms_seq, file_cnt, mms_body, mms_subject, ,
file_type1, file_name1,service_dep1)

VALUES (
1, 2 , '본문 내용','메시지 제목’, 'IMG','D:\MMSTestFile\01.IMG', 'ALL' );
```



{% hint style="info" %}
**참고사항**

1\. **mms\_body** 필드 입력 값은 하나의 'TXT' 파일로 인식이 된다. ( **file\_cnt** 필드 값에 반영 필요 )

2\. 이미지 파일 첨부 발송 시 **file\_type**은 반드시 IMG 이어야 한다.\
(이때 **file\_type**을 JPG, BMP, SIS 등으로 입력하여 발송하면 실패 될 수 있음.)

3\. SMS 발송 시 한글이 정상적으로 보이지만 MMS 발송 시 한글이 깨지는 경우는 MMS 컨텐츠 파일 (.skn) 생성 시, 시스템 캐릭터 셋의 영향을 받기 때문이다.

\-> 아래와 같이 DBro 구동 스크립트를 작성하여 LANG 설정 값을 **ko\_KR.euckr** 로 지정해야 한다.
{% endhint %}



**1.서버 한글 캐릭터셋 확인 (리눅스 기준)**

`$ locale -a | grep ko`&#x20;

_ko\_KR_\
_ko\_KR.euckr_ \
_ko\_KR.utf8_\
_korean_ \
_korean.euc_

**2.DBro 기동 스크립트 작성 (DBro 프로세스 실행 시, LANG 설정 값 지정 위함)**

`$ vi start.sh`

```shell
#!/bin/bash
export LANG=ko_KR.euckr
java -jar /home/dbro/dbro.jar /home/dbro/dbro.conf > /dev/null &
```



**3. DBro 프로세스 재시작 ( 실행 시, 2번에서 작성한 스크립트로 실행 )**&#x20;

1\) 기존 프로세스 종료\
`$ ps -ef | grep dbro`\
\*\*\*\* 29335      1        0        May23 pts/0      00:00:07 java -jar /home/dbro/dbro.jar&#x20;

/home/dbro/dbro.conf&#x20;

`$ kill 29335`

2\) 프로세스 실행&#x20;

`$ ../start.sh`