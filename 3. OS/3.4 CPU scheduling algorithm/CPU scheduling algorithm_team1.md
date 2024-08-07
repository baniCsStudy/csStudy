# CPU 스케줄링 알고리즘

<hr/>

## CPU 스케줄러
> CPU 스케줄러는 운영체제의 커널 부분으로, 실행 가능한 프로세스들 중 하나를 선택하여 CPU를 할당하는 역할을 합니다.
> 
> 스케줄러는 시스템 성능을 최적화하고 공정한 자원 분배를 위해 다양한 스케줄링 알고리즘을 사용합니다.

<br/>

## 비선점형 방식
> 비선점형 스케줄링에서는 CPU를 할당받은 프로세스가 스스로 종료하거나 
> 
> I/O 요청 등으로 자발적으로 CPU를 반환할 때까지 계속 실행됩니다.

1. FCFS(First Come, First Served) or FIFO(First In, First Out)
- 가장 먼저 도착한 프로세스에게 CPU를 할당합니다.
- 비효율적인 CPU 사용과 긴 대기 시간이 발생할 수 있습니다. 특히 "Convoy Effect"가 나타날 수 있습니다.
```
Convoy Effect
- CPU를 많이 필요로 하지 않는 프로세스들이, CPU를 오랫동안 사용하는 프로세스가 끝나기를 기다리는 현상을 말한다.
```
2. SJN(Shortest-Job Next) or SJF(Shortest-Job First)
- 실행 시간이 가장 짧은 프로세스에게 CPU를 할당합니다.
- 실행 시간을 미리 알기 어렵고, 긴 프로세스가 계속 대기할 수 있습니다.
3. HRN / HRRN(Highest Response Ratio Next)
- "우선순위 = (대기시간 + 실행시간) / 실행시간" 을 통해서 계산되어집니다.
- "대기시간"이 길어질 수록, 더 큰 값을 가지게 되므로, "실행시간이 길다는 이유로,<br>실행시간이 짧은 프로세스에게 밀려서 오랫동안 기다린 프로세스가 더 높은 우선순위를 가지게 만든다".
4. 우선순위 스케줄링(Priority Scheduling)
- 우선순위가 가장 높은 프로세스에게 CPU를 할당합니다.
- 우선순위가 낮은 프로세스는 무한 대기 상태에 빠질 수 있습니다(Starvation).


## 선점형 방식
> 선점형 스케줄링에서는 운영체제가 CPU를 할당한 후에도 언제든지 CPU를 회수하고 다른 프로세스에게 할당할 수 있습니다.

1. RR(Round Robin)
- 각 프로세스에게 일정 시간(Time Quantum) 동안 CPU를 할당합니다. 
- 시간이 만료되면 다음 프로세스에게 CPU를 할당합니다.
- Time Quantum(CPU를 점유할 수 있는 최대 시간) 의 크기에 따라 성능이 달라질 수 있습니다. 
- 너무 작으면 CPU 오버헤드가 증가하고, 너무 크면 FCFS와 유사해집니다.
2. SRF / SRTF(Shortest Remaining Time First)
- 남은 실행 시간이 가장 짧은 프로세스에게 CPU를 할당합니다. 
- 새로운 프로세스가 도착할 때마다 남은 실행 시간을 비교하여 CPU를 선점할 수 있습니다.
- 실행 시간을 미리 알기 어렵고, 긴 프로세스가 계속 대기할 수 있습니다.
3. 선점형(Priority Scheduling)
- 우선순위가 높은 프로세스가 도착하면 현재 실행 중인 프로세스를 중단하고 우선순위가 높은 프로세스에게 CPU를 할당합니다.
- 우선순위가 낮은 프로세스는 무한 대기 상태에 빠질 수 있습니다(Starvation). 
- 이를 방지하기 위해 Aging 기법을 사용할 수 있습니다.
```
Aging 기법
시스템에서 특정 프로세스의 우선순위가 낮아서 무한정 기다리는 경우를 방지하기 위해서 기다린 시간에
비례해서 일정 시간이 지나면 우선순위를 한 단계식 높여주는 방법입니다.
Aging기법을 도입해 SJF에서 HRN으로, MLQ에서 MLFQ로 사용합니다. 
```
4. 다단계 큐 스케줄링(Multilevel Queue Scheduling)
- 프로세스들을 여러 개의 큐로 나누고, 각 큐에 다른 스케줄링 알고리즘을 적용합니다. 
- 예를 들어, 상위 큐는 Round Robin, 하위 큐는 FCFS를 사용할 수 있습니다.
- 구현이 복잡하고, 하위 큐의 프로세스가 계속 대기할 수 있습니다.
5. 다단계 피드백 큐 스케줄링(Multilevel Feedback Queue Scheduling)
- 프로세스가 CPU를 사용하는 시간에 따라 다른 큐로 이동할 수 있는 스케줄링 알고리즘입니다. 
- 자주 CPU를 사용하는 프로세스는 낮은 우선순위 큐로 이동하고, 적게 사용하는 프로세스는 높은 우선순위 큐로 이동합니다.
- 파라미터 설정이 어려울 수 있습니다.