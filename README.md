# FSM_Motor_PWM_control_Timer
timer additional
![image](https://user-images.githubusercontent.com/82801399/196065588-da6bd97c-53e6-42ba-8768-8992c99b4bbc.png)


![image](https://user-images.githubusercontent.com/82801399/196070107-508e6be1-6f3d-4a9c-a87f-db885842f3de.png)


![image](https://user-images.githubusercontent.com/82801399/200523575-069faa2a-cbb7-427f-987e-5998f1dcbbe1.png)


예약 기능을 가진 선풍기 구현 verilog 코드다.

가운데 버튼은 power off 버튼이며, 상하 버튼을 통해 선풍기(모터)의 출력을 바꿀 수 있다. 윗 버튼을 통해 PWM state가 증가하는데 최대치가 되면 윗 버튼을 눌러도 PWM state는 유지된다. 마찬가지로 아랫 버튼을 통해 PWM state는 감소하며 최소치(모터 off)에서는 PWM state가 유지된다.


좌우 버튼을 통해 예약꺼짐 기능 조절이 가능한데, 현재 코드상 10초 단위로 0~30초까지 가능하다. timer mode 스위치를 올리면 남은 시간이 0이 될 때까지만 출력이 유지되다가 PWM state가 0이 된다.

power off버튼과 리셋 스위치와의 차이점은 power off 버튼은 FSM Motor 및 Timer에서만 영향을 주어 각각의 상태를 0으로 초기화하지만 리셋 스위치의 경우 더 앞단의 모듈인 clock divider부터 영향을 주어 각 clock들을 전부 초기화시킨다. 기능적으로 큰 차이가 있는 것은 아니지만 설계 단계에서 영향을 주는 부분이 다르다. 


마무리 날짜 2022.10.16.

https://mgchoi.tistory.com/86

최종 동작
https://www.youtube.com/shorts/tzfOFJJJuNg


history

1일차 2022.10.13.

https://mgchoi.tistory.com/85

https://github.com/316415/FSM_LightStand_PWM

https://www.youtube.com/shorts/Qo-kExtJVFI

2일차 2022.10.14.

https://mgchoi.tistory.com/86

https://github.com/316415/FSM_Motor_PWM_control

https://www.youtube.com/shorts/hEFoCiUW_ck

3~4일차 2022.10.15. ~ 2022.10.16.

