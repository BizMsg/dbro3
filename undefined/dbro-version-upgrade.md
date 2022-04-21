# DBro Version Upgrade

{% hint style="warning" %}
1. 기존 모듈을 백업후 진행해주시기 바랍니다.
2. 버전 업그레이드는 모듈을 종료후 진행주시기 바랍니다.
{% endhint %}

**1. 외부 라이브러리 참조**

JAVA 모듈이 외부 라이브러리를 참조하도록 변경되었습니다.\
기존 lib 폴더가 없다면 신규 dbro 파일내 lib 폴더를 dbro.jar과 같은 위치에 이동시킵니다.

**2. dbro.jar 교체**

신규 기능이 적용된 모듈로 교체합니다.

**3. 로그 라이브러리 교체**

logback을 사용하도록 변경되었습니다.\
lib/log 파일을 신규 dbro 파일내 lib/log 파일로 변경해주시길 바랍니다. \
\
기존 : log4j-1.2.15.jar\
변경 : logback-classic-1.2.10.jar, logback-core-1.2.10.jar, slf4j-api-1.7.32.jar
