# 리눅스 명령어

## 1) TOP 명령어

 * 서버의 실시간 사용률이나 메모리 사용률을 대표적으로 볼 수 있음.

 * Cpu사용이 많은 순서대로 프로세스 목록을 보여줌.

 실행하면 다음과 같은 결과가 나온다.


 <img src="https://user-images.githubusercontent.com/106548276/171981577-ded66262-97e7-464e-b3cb-86e6238f5e22.jpg" width="60%" height="60%"/>

*첫번째 줄: 현재 시간과 서버가 구동된 날짜, 서버 사용자 수와 load ,평균을 보여줌*

*두번째 줄: 총 수행중인 프로세스의 개수와 현재 실행중인 프로세스 개수를 알려줌*

*세번째 줄: CPU의 사용률을 볼 수 있음 ( us, sy, id / 일반적으로 us+sy = Cpu 사용률, id = 여유 Cpu)*

*네번째 줄: 메모리 관련 정보 제공 ( 윗 줄은 실제 메모리 사용률, 아랫 줄은 스왑 메모리에 대한 내용 )*

```c
top -d 1
```
-> 위와 같이 입력하면 3초마다의 주기를 1로 변경할 수 있음.

같이 사용하는 명령어들은 아래의 표와 같다.

|명령어|설명|
|--|--------|
|1 |Cpu 코어별 사용 현황|
|m |메모리 사용률 시각화 표시|
|shift+p|Cpu 사용률이 높은 프로세스를 기준으로 나열|
|shift+m|메모리 사용률이 높은 프로세스를 기준으로 나열|
|shift+t|수행 시간이 긴 프로세스를 기준으로 나열|
|k|kill 할 프로세스 PID를 입력할 수 있음|
|H|상단의 Tasks 기준을 쓰래드로 변경|
|u|모니터링할 user를 선택하여, 해당 권한 프로세스 감시|

## 2) ps 명령어

 * process status의 약자로 현재 실행중인 프로세스 목록을 확인할 수 있음.
 
 ```c
 ps
 ```
 -> pid, cmd 등 프로세스의 기본적인 내용만 출력
 ```c
 ps -p 1
 ```
 -> 프로세스 번호가 1인 프로세스 출력
 ```c
 ps -u seek
 ```
 -> 계정이 seek인 프로세스들을 출력
 ```c
 ps -ef | more
 ```
 -> 모든 프로세스를 풀 포맷으로 출력, more 명령어를 이용하여 페이지 단위로 출력
 ```c
 ps -ef | grep seek
 ```
 -> 모든 프로세스를 풀 포맷으로 출력한 목록에서 grep을 이용해 seek이 포함된 행을 출력

|   |필드 정보|
|---|-----|
|UID|User ID|
|PUD|Process ID|
|PPID|부모 Process ID|
|STIME|프로세스의 시작시간|
|TTY|연결되어 있는 터미널이 무엇인지|
|TIME|프로세스가 소비한 총 시간|
|CMD|프로세스 실행 명령어|
|C|Cpu 사용량|

|  |대표 옵션|
|--|------|
|-e|모든 프로세스를 출력|
|-f|Full format으로 출력(UID, PID . .)|
|-l|긴 format으로 출력|
|-p|특정 PID의 프로세스를 보여준다|
|-u|특정 사용자의 프로세스를 보여준다|

## 3) jobs 명령어

  * 작업이 중지된 상태, 백그라운드로 진행 중인 작업 상태, 변경되었지만 보고 되지 않은 작업 상태 등을 표시하는 명령어임
  
  |옵션|설명|
  |--|------|
  |-l|프로세스 그룹 ID를 state 필드 앞에 출력|
  |-n|프로세스 그룹 중에 대표 프로세스 ID를 출력|
  |-p|각 프로세스 ID에 대해 한 행씩 출력|
  |command|지정한 명령어를 실행|
  
 ### jobs로 알 수 있는 세션의 상태 값
 
 |상태|설명|
 |---|------|
 |Running|작업이 일시 중단되지 않았고 종료하지 않고 계속 진행 중임|
 |Done|작업이 완료되어 0을 반환하고 종료 했음을 의미|
 |Done(code)|작업이 정상적으로 완료되었으며, 0이 아닌 코드를 반환 했음을 의미|
 |Stopped|작업이 일시 중단|
 |Stopped(SIGTSTP)|SIGTSTP 신호가 작업을 일시 중단|
 |Stopped(SIGSTOP)|SIGSTOP 신호가 작업을 일시 중단|
 |Stopped(SIGTTIN)|SIGTTIN 신호가 작업을 일시 중단|
 |Stopped(SIGTTOU)|SIGTTOU 신호가 작업을 일시 중단|

## 4) kill 명령어

  * 대게 프로세스를 죽일 때 사용하는데 원래 내부적으로는 프로세스에 시그널을 보내 원하는 작업을 하게 하는 명령어

*사용 구문*
```c
kill [옵션] [pid]
```
예를 들어 실행중인 특정 프로세스를 죽이고 싶다면 ps 명령어를 통해 해당 프로세스의 pid를 얻고 kill명령어의 파라미터로 넘겨 실행하면 프로세스를 종료시킬 수 있음

*사용 예시*
```c
kill 12345
```
-> pid가 '12345'인 프로세스를 종료
```c
kill -9 12345
or
kill -SIGKILL 12345
```
-> pid가 '12345'인 프로세스를 강제 종료
```c
kill -l
```
-> kill 명령어에서 지원하는 시그널 목록을 출력

## 5) 매크로 q 사용 방법 ( vim 에디터 )

**커맨드 모드( esc를 누른 상태에서 )**

**1. 'q'를 누르고 a~z 사이 문자로 매크로 recoding을 시작한다**

**커맨드 모드로 돌아와서 'q'를 누르면 매크로 recoding이 끝이 난다**

**매크로를 사용하려면 커맨드 모드에서 @+a~z를 입력하면 된다**

***@a~z : 1회 실행***

***@@ : 방금 실행한 매크로 실행***

***10@a~z : 매크로 10회 실행***

