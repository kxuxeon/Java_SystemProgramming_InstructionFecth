# 📌 시스템 프로그래밍 [명령어 인출 프로그램]
####📕 PC 전원을 키고 부터 BIOS, CPU, Memory 까지 프로그램을 실행했을 때 명령어가 인출되는 과정 프로그래밍

# 📌 프로세스 스케줄러
>1. 컴퓨터의 전원을 키면 ROM BIOS가 실행되면서 CPU가 가지고 있던 예전
    레지스터값들을 지우고 PC를 ROM의 부트프로그램의 주소값으로 초기화시킨다.
>2. CPU, System Bus, RAM등 여러 구성요소를 테스트하고 오류가 없으면
   ROM BIOS로부터 참조를 해서 어느 드라이브에서 OS를 읽어 올 것인지 확인을
   하고 OS를 실행시킨다.
>3. loader가 프로세스드를 메모리에 load하면 CPU의 스케줄링에 의해
   프로세스들(주소)이 순차적으로 readyQueue에 쌓인다.
>4. Ready Queue에 제일 앞에 있는 프로세스의 주소를 확인 후 해당 프로세스
   PCB를 CPU레지스터에 설정한다.
>5. PC에 적힌 메모리의 주소값을 MAR로 보낸 후 명령어를 인출해 MBR로 옮기고
   PC의 값을 1씩 증가시킨다.
>6. MBR에 저장된 명령어 코드를 IR로 옮기고 인출된 명령어를 보고 결과에 따라
   연산을 수행한다. & Status Flag를 확인한다. (인터럽트 발생 전까지 반복)
>7. 인터럽트 요청이 오면 CPU가 직접 인터럽트 플래그(IE)와 인터럽트
   요청신호를 AND하여 인터럽트 플래그에 직접 설정한다. 인터럽트 플래그를
   보고 인터럽트 요청 신호가 온 것을 확인.
>8. 현재 PC의 내용과 State Register를 PCB에 저장하고 PC의 값을 ISR의 시작주소로
   설정한다.
>9. 인터럽트 서비스 루틴에 대한 정보가 있는 인터럽트 벡터를 찾아보고 인터럽트 루틴을 결정.
>> TimeOut
>>10. 실행 중이던 프로세스의 주소를 Ready Queue의 젤 뒤로 옮김.
>>11. Ready Queue를 보고 다음 프로세스의 PCB를 CPU의 레지스터에 설정하고 프로세스를 다시 한 줄씩 실행.
> 
>> I/O Started
>>10. CPU가 해당 I/O Device에 메모리의 주소를 알려주면 DMA를 통해
      I/O디바이스가 직접 메모리 주소로 가서 작업을 한다.
>>11. 실행 중인 프로세스를 Wait Queue에 넣고 context switching을 한 후
      다음 프로세스 실행.
> 
>> I/O Finished
>>  - 작업이 완료되면 DMA는 CPU에 인터럽트를 보낸다. CPU는 인터럽트   
    신호를 받으면 직접 State Flag를 설정한다.
>>  10. CPU에서 DMA를 보고 어느 프로세스에서 실행한 작업인지 확인 후 Wait
      Queue에 있는 해당 프로세스의 주소를 Ready Queue의 맨 마지막으로
      옮긴다.
> 
>> Terminate
>>10. 프로세스가 종료되면 할당되어 있던 모든 프로세스 메모리를 해제.

# 📌 실행 화면
![image](https://user-images.githubusercontent.com/48740872/135422308-457da78b-be01-4796-bd17-f18363b8e11c.png)


