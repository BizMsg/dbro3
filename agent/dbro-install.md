# DBRO install

Binary 배포판에는 다음과 같은 파일들이 들어 있습니다.

**dbro.jar**

주 실행 파일로서 아래에 나타난 내부 실행 파일들을 구동하고 감시하는 역할을 하면 다음의 기능을 포함하고 있습니다.

* SMSGW에 접속하여 메시지를 망으로 송신하는 기능
* SMSGW에 접속하여 망에서 돌아온 전송 결과들을 수집하는 기능
* transaction table에 쌓여있는 Record를 월별 Log table로 이동시켜주는 기능

**dbro.conf.sample**

dbro.conf 파일을 만들기 위한 참고 파일로서, 이 문서에서 언급하는 구성 방식에 대한 샘플이 들어 있는 파일입니다.\


### 설치

**Linux**

1. 디렉터리 생성 (**영문으로 명명**)
2. dbro.conf.sample -> dbro.conf
3. 설정 수정 (DBRO Configuration 참고)
4. 실행 스크립트(start.sh) 작성 및 Agent (dbro3) 행

> 1\) 서버 한글 캐릭터셋 확인 (리눅스 기준)
>
> `$ locale -a | grep ko`
>
> _ko\_KR_\
> _ko\_KR.euckr_ \
> _ko\_KR.utf8_\
> _korean_ \
> _korean.euc_
>
> 2\) DBro 기동 스크립트 작성 (DBro 프로세스 실행 시, LANG 설정 값 지정 위함)
>
> `$ vi start.sh`
>
> ```shell
> #!/bin/bash
> export LANG=ko_KR.euckr
> java -jar /home/dbro/dbro.jar /home/dbro/dbro.conf > /dev/null &
> ```
>
> 3\) DBro 프로세스 재시작 ( 실행 시, 2번에서 작성한 스크립트로 실행 )&#x20;
>
> &#x20;\- 기존 프로세스 종료\
> `$ ps -ef | grep dbro`\
> \*\*\*\* <mark style="color:red;">29335</mark>      1        0        May23 pts/0      00:00:07 java -jar /home/dbro/dbro.jar /home/dbro/dbro.conf&#x20;
>
> `$ kill` <mark style="color:red;">29335</mark>
>
> &#x20;\- 프로세스 실행&#x20;
>
> `$ ./start.sh`

****

**Windows**

1. 방화벽 상태 점검 (UFIT G/W - IP 및 PORT 오픈)
2. 윈도우 서비스 등록

> 32비트 운영체제
>
> &#x20;    **serviceinstall32.bat** (서비스 등록), **serviceuninstall32.bat** (서비스 제거)
>
> 64비트 운영체제
>
> &#x20;   **serviceinstall64.bat** (서비스 등록), **serviceuninstall64.bat** (서비스 제거)
>
> \
> JAVA\_HOME : JDK 설치 경로
>
> DBRO1\_HOME : DBro 압축 해제 경로\
> DBRO1\_SERVICE\_NAME : 서비스 등록 명&#x20;

&#x20; 3\. 커맨드 창에서 인스톨 파일 실행

* `32비트 운영체제`\
  &#x20;`D:\dbro>serviceinstall32.bat`
* `63비트 운영체`\
  &#x20;`D:\dbro>serviceinstall64.bat`

&#x20; 4\. 서비스 등록 및 시

\[제어판]-\[관리도구]-\[서비스] 창에 "**DBRO1\_SERVICE\_NAME**" 로 지정한 서비스 등록여부 확인 \
\- DBro 서비스 시작

{% hint style="info" %}
Java 7 버전 이상의 경우,\
Windows와 JAVA의 일부 라이브러리 버전 오류로 정상 기동이 안 될 수 있습니다.

→ 해결 방법 : JAVA\_HOME\bin\msvcr100.dll 파일을 c:\windows\system32 폴더에 복사
{% endhint %}



### 운영체제 별 실행방법

**리눅스**

`$java -jar dbro.jar ./dbro.conf &`

**AIX**

`$nohup java -jar dbro.jar ./dbro.conf &`

**HPUNIX, Solaris**

`$nohup java -jar dbro.jar ./dbro.conf > /dev/null &`

**Windows**

설치 가이드에 따라 서비스 등록한 후 서비스 시작



#### 실행 확인

프로세스 확인 : `ps -ef | grep dbro.jar`&#x20;



{% hint style="info" %}
DBro 프로그램이 정상적으로 실행되면 \
em\_tran _/_ em\_tran\_mms _/_ em\_log\_YYYYMM 3개의 테이블이 자동으로 생성됩니다.

실제 메시지 전송을 하면 이통사로부터 전송 결과를 받아 em\_log\_YYYYMM와 같은 형식으로 로그 테이블을 월 별로 생성합니다.

\
\
\
이후 **메시지 발송** 항목을 참고하여 전송 테스트를 할 수 있습니다.
{% endhint %}





