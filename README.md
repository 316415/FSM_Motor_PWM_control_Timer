# FSM_Motor_PWM_control_Timer
timer additional
![image](https://user-images.githubusercontent.com/82801399/196065588-da6bd97c-53e6-42ba-8768-8992c99b4bbc.png)


![image](https://user-images.githubusercontent.com/82801399/196070107-508e6be1-6f3d-4a9c-a87f-db885842f3de.png)


![image](https://user-images.githubusercontent.com/82801399/200523575-069faa2a-cbb7-427f-987e-5998f1dcbbe1.png)


예약 기능을 가진 선풍기 구현 verilog 코드다.

가운데 버튼은 power off 버튼이며, 상하 버튼을 통해 선풍기(모터)의 출력을 바꿀 수 있다. 윗 버튼을 통해 PWM state가 증가하는데 최대치가 되면 윗 버튼을 눌러도 PWM state는 유지된다. 마찬가지로 아랫 버튼을 통해 PWM state는 감소하며 최소치(모터 off)에서는 PWM state가 유지된다.


좌우 버튼을 통해 예약꺼짐 기능 조절이 가능한데, 현재 코드상 10초 단위로 0~30초까지 가능하다. timer mode 스위치를 올리면 남은 시간이 0이 될 때까지만 출력이 유지되다가 PWM state가 0이 된다.

power off버튼과 리셋 스위치와의 차이점은 power off 버튼은 FSM Motor 및 Timer에서만 영향을 주어 각각의 상태를 0으로 초기화하지만 리셋 스위치의 경우 더 앞단의 모듈인 clock divider부터 영향을 주어 top motor 전부를 초기화시킨다. 기능적으로 큰 차이가 있는 것은 아니지만 설계 단계에서 영향을 주는 부분이 다르다.




Basys3 chip에서 발생하는 system clock은 100MHz로 그 주파수를 낮출 필요가 있었다. 상대적으로 1MHz로 다소 빠르게 작동하도록 설정한 clock divider 모듈은 연결 라인에서 버튼 및 FSM Motor 그리고 PWM이 보인다. PWM의 원활한 동작을 위해 상대적으로 주파수를 높게 책정했다. 버튼 모듈은 디바운스를 설정해 채터링을 방지했다. 버튼에서 들어오는 입력 신호에 따라 state를 결정하고 그에 따른 동작을 하드웨어가 진행할 수 있도록 신호를 선별하는 MUX나 신호를 변환하는 Decoder 모듈을 만들었다.

FSM Timer는 연결된 라인에서는 시간 계산이 편한 1kHz가 되도록 clock divider에서 분주비를 설정하였다.(input 100MHz --> output 1kHz) 시간 값을 FND를 통해 출력하므로 카운터를 적절히 나누는 작업을 진행했다. FND가 출력할 수 있는 자릿수는 4개인데 앞의 두 개는 시간, 뒤의 두 개는 PWM state를 출력한다. 이에 따라 각각 자릿수에 적절한 숫자를 출력하기 위해 digit divider 모듈과 FND position을 위한 4X1 MUX 모듈을 만들었다. 자릿수의 숫자가 적절하게 FND에 출력될 수 있도록 BCD to FND decoder 모듈을 제작했다. FND는 0,1,2,3을 반복해서 세는 position counter의 출력신호에 맞춰 자리와 숫자를 매칭했고 동시 출력이 아니라 자릿수마다 단일 출력이 되는 구조이다. 그러나 충분히 빠르기에 잔상을 통해 동시 출력으로 보이도록 만들었다.




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

