# 리눅스 명령어

## 1) TOP 명령어

 * 서버의 실시간 사용률이나 메모리 사용률을 대표적으로 볼 수 있음.

 * CPU사용이 많은 순서대로 프로세스 목록을 보여줌.

 실행하면 다음과 같은 결과가 나온다.


 <img src="https://user-images.githubusercontent.com/106548276/171981577-ded66262-97e7-464e-b3cb-86e6238f5e22.jpg" width="60%" height="60%"/>

첫번째 줄: 현재 시간과 서버가 구동된 날짜, 서버 사용자 수와 load ,평균을 보여줌

두번째 줄: 총 수행중인 프로세스의 개수와 현재 실행중인 프로세스 개수를 알려줌

세번째 줄: CPU의 사용률을 볼 수 있음 ( us, sy, id / 일반적으로 us+sy = CPU 사용률, id = 여유 CPU) 

네번째 줄: 메모리 관련 정보 제공 ( 윗 줄은 실제 메모리 사용률, 아랫 줄은 스왑 메모리에 대한 내용 )

`c
top -d 1
`
