# DBro 프로세스 구조

### DBro 프로세스 블록다이어그램

DBro는 실행 시 3개의 쓰레드가 동작합니다.

![](<../.gitbook/assets/image (5).png>)

**DBro**

실행하는 프로세스가 Daemon으로 되면서 남는 프로세스이며 나머지 프로세스를 실행합니다.

**DBro Sender**

주기적으로 DB를 Select하며, Select된 메시지를 SMSGW로 보냅니다.

**DBro Receiver**

MSGW로부터 오는 전송결과를 수신하여 DB를 Update합니다.
