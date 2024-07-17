# 프로세스와 스레드

## 관련 질문
<details>
  <summary>
    쿠키와 세션의 차이에 대해 설명해주세요
  </summary>
  <blockquote>
    - 쿠키: 웹 서버가 클라이언트의 로컬 저장소에 저장하는 작은 데이터 파일입니다.
만료기한을 설정할 수 있으며, 주로 서버측에서 설정합니다.<br>
만료기한 설정시에는 브라우저를 종료해도 데이터가 날아가지 않습니다.<br>
클라이언트 측에 저장되기에 비교적 보안이 약합니다.<br>
일반적으로 하나의 쿠키당 최대 4KB의 데이터를 저장할 수 있으며, 각 도메인은 약
20개의 쿠키를 저장할 수 있습니다.
<br><br>
- 세션: 웹 서버에 사용자별로 저장되는 상태 정보입니다.<br>
클라이언트는 세션ID만을 가지고 있으며 이 ID는 쿠키 또는 URL 매개변수를 통해 전달됩니다.
    <br>
일반적으로 브라우저가 닫히거나 서버에서 정한 세션 타임아웃이 지나면 정보가 만료됩니다.
    <br>
쿠키에 비해 상대적으로 보안이 높습니다.
    <br>
서버의 메모리 또는 저장 용량에 따라 세션의 크기 제한이 달라지며,
일반적으로 쿠키보다 훨씬 많은 데이터를 저장할 수 있습니다.
  </blockquote>
</details>
<br/>
<details>
  <summary>
  	컴퓨터의 메모리 계층을 나누는 이유에 대해 설명하세요.
  </summary>
  <blockquote>
    속도, 비용, 용량의 균형을 맞추기 위해서입니다.
각각의 메모리 계층은 특정한 목적을 가지고 있으며, 
전체 시스템의 성능을 최적화하는 데 기여합니다. 
이 구조를 통해 컴퓨터는 빠르게 접근해야 하는 데이터와 
상대적으로 덜 자주 접근하는 데이터를 효율적으로 관리할 수 있습니다.
  </blockquote>
</details>
<br/>
<details>
  <summary>
  	프로세스의 상태 전이 과정과, 각 상태의 역할에 대해 설명하세요.
  </summary>
  <blockquote>
    프로세스의 주요 상태 전이 과정은 운영 체제에서 프로세스가 생성되고 
종료될 때까지의 다양한 상태 변화를 설명합니다.

생성 = 프로세스가 생성되는 중입니다.
운영 체제는 프로세스 제어 블록(PCB)을 초기화하고 필요한 자원을 할당합니다.

준비 = 프로세스가 CPU가 할당되기를 대기 중인 상태입니다.

실행 = 프로세스가 CPU를 사용하여 실제로 실행 중인 상태입니다.

대기 = 프로세스가 특정 이벤트(예: I/O 완료)를 기다리고 있는 상태입니다.

종료 = 프로세스가 실행을 완료하고 모든 자원이 해제된 상태입니다.
프로세스는 더 이상 실행되지 않으며, PCB가 삭제됩니다.
  </blockquote>
</details>
<br/>
<details>
  <summary>
  	프로세스 내 정적 영역과 동적 영역의 차이에 대해 설명하세요.
  </summary>
  <blockquote>
    정적 영역 = 프로그램 실행 중 메모리 할당이 고정된 데이터를 저장하는 공간입니다.
주로 프로그램 코드와 전역 변수, 정적 변수 등을 포함합니다.
컴파일 타임에 크기와 위치가 결정되며, 
프로그램이 종료될 때까지 그 크기와 위치가 변하지 않습니다.
주소가 고정되어 있어 접근 속도가 빠릅니다.
불필요한 동적 할당을 피해 메모리를 절약합니다.
<br><br>
동적 영역 = 동적 영역은 프로그램 실행 중에 필요에 따라 메모리를 할당하고
해제할 수 있는 영역입니다. 
힙(Heap)이라고도 불리며, 주로 동적으로 생성된 객체와 변수들을 포함합니다. 
런타임 동안 크기와 위치가 변할 수 있습니다.
<br><br>    
동적 영역의 주소 공간 배치 난수화 (ASLR) = 실행 중인 프로그램의 메모리 주소를 무작위로 배치하여 보안을 강화하는 기술입니다. 이 방법은 공격자가 특정 메모리 주소를 예측하기 어렵게 만들어, 버퍼 오버플로우 등의 취약점을 악용한 공격을 방지합니다.

    <출처: "ASLR randomizes the memory addresses used by system and application processes, including the stack, heap, and memory-mapped libraries." (Source: "Security Engineering: A Guide to Building Dependable Distributed Systems" by Ross Anderson)>
  </blockquote>
</details>
<br/>
<details>
  <summary>
  	페이징을 공유하는 메커니즘에 대해 설명하세요.
  </summary>
  <blockquote>
    페이징 공유(Shared Paging)는 운영체제에서 메모리 효율성을 높이기 위해 여러 프로세스가 동일한 페이지를 공유하는 메모리 관리 기법입니다. 이는 주로 공유 라이브러리나 코드 세그먼트를 여러 프로세스가 동시에 사용할 때 유용합니다.
    <br>
    <br>
    여러 프로세스가 동일한 라이브러리를 사용할 때, 해당 라이브러리를 메모리에 한 번만 로드하고 여러 프로세스가 이를 공유합니다. 이렇게 하면 메모리 사용량이 줄어듭니다.
    <br>
    <br>
    각 프로세스의 페이지 테이블에 공유 페이지에 대한 항목이 존재하여, 동일한 물리적 메모리 페이지를 가리키게 됩니다.
    <br>
    <br>
    주로 코드와 같이 변하지 않는 데이터가 공유되며, 각 프로세스가 이를 읽기 전용으로 접근합니다. 필요시, 쓰기 작업이 발생하면 해당 페이지를 복사하여(Copy-on-Write) 각 프로세스가 독립적으로 수정할 수 있도록 합니다.
    <br>
    <br>
	<출처 : "Shared paging is a memory management scheme where multiple processes can share pages, particularly those containing code or read-only data." (Source: "Operating System Concepts" by Abraham Silberschatz, Greg Gagne, and Peter B. Galvin)>
  </blockquote>
</details>
<br/>
<details>
  <summary>
  	페이징 환경에서 메모리를 보호하는 방법에 대해 설명하세요.(메모리 보호 비트에 대해)
  </summary>
  <blockquote>
    메모리 보호 비트는 CPU 하드웨어와 운영체제에서 메모리 접근 권한을 제어하기 위해 사용하는 메커니즘입니다. 이러한 비트는 각 메모리 페이지에 대해 설정되며, 페이지 테이블 엔트리에 포함됩니다.
    <br>
    <br>
    각 페이지 테이블 엔트리(Page Table Entry, PTE)에 보호 비트가 포함되어 있으며, CPU는 메모리 접근 시 이 비트를 참조하여 접근 권한을 검사합니다.
    <br>
    <br>
접근 권한이 없는 메모리 페이지에 접근하려고 할 경우, CPU는 페이지 폴트(Page Fault) 예외를 발생시켜 운영체제가 이를 처리하도록 합니다.
  </blockquote>
</details>
<br/>
  <details>
  <summary>
  	프로그램을 통해 카메라에 접근하는 과정을 시스템 콜과 하드웨어 인터럽트라는 용어를
사용해서 설명하세요.
  </summary>
  <blockquote>
    I/O에 직접 접근이 불가하기 때문에 시스템 콜이 OS를 통해 I/O에 접근, 시스템 콜을 통해 작업이 끝났음을 알립니다.
하드웨어 인터럽트는 작업이 끝났음을 CPU에 알려줄 때 일어납니다.
  </blockquote>
</details>
<br/>
    <details>
  <summary>
  	임계 영역에 대해 설명해주세요.
  </summary>
  <blockquote>
    임계 영역은 여러 프로세스나 스레드가 공유 자원에 접근하는 코드 부분입니다. 동시 접근 시 데이터 일관성이 깨질 수 있어, 이를 해결하기 위한 동기화 기법이 필요합니다.
    <br>
    <br>
뮤텍스(Mutex): 상호 배제를 보장하는 락으로, 한 번에 하나의 프로세스만 임계 영역에 접근할 수 있게 합니다.
    <br>
    <br>
세마포어(Semaphore): 카운터를 사용해 여러 프로세스가 자원에 접근하는 것을 제어합니다.
    <br>
    <br>
모니터(Monitor): 고수준 동기화 기법으로, 뮤텍스와 조건 변수를 사용해 임계 영역을 보호합니다. 프로그래밍 언어 수준에서 제공되기도 합니다.
    <br>
    <br>
    조건 변수(Condition Variable): 모니터와 함께 사용되어 특정 조건이 만족될 때까지 스레드를 블록 상태로 만듭니다.
  </blockquote>
</details>
<br/>
    <details>
  <summary>
  	페이지 폴트와 쓰래싱에 대해 설명하세요.
  </summary>
  <blockquote>
    페이지 폴트: 프로세스가 접근하려는 메모리 페이지가 현재 물리적 메모리에 없을 때 발생하는 예외 상황.
    <br>
    <br>
    쓰래싱: 프로세스가 페이지 폴트가 과도하게 발생하여 CPU가 실제 작업을 수행하지 못하고, 대부분의 시간을 페이지 교체 작업에 소비하는 현상.
    <br>
    <br>
    페이지 폴트의 해결 방안
    <br>
    <br>
    워킹셋: 특정 시간 동안 프로세스가 자주 참조하는 페이지들의 집합. 이를 통해 운영체제는 프로세스가 필요로 하는 페이지들을 메모리에 유지하여 페이지 폴트를 줄입니다.
    <br>
    <br>
	PFF: 페이지 폴트 발생 빈도를 측정하여 메모리 관리 정책을 조절하는 방법. 페이지 폴트 빈도가 높으면 프로세스에 더 많은 메모리를 할당하고, 낮으면 메모리를 회수합니다.
  </blockquote>
</details>
<br/>

<hr/>

## 프로세스란?
> 프로그램의 실행중인 인스턴스.

<br/>

## 프로세스의 메모리 구조
> 크게 네 가지 영역으로 나뉜다.

1. code 영역
- 실행할 프로그램의 코드가 저장
2. data 영역
- 전역변수와 정적변수가 저장
- 초기화된 전역변수는 bss 영역에 저장되는데,
  이는 휘발성 메모리인 ROM과 구분해서 비휘발성 메모리인 RAM에 저장하기 위함
3. stack 영역
- 지연변수, 매개변수, 리턴값 등 잠시 사용되었다가 사라지는 데이터를 저장
4. heap 영역
- 동적 데이터 영역
- 메모리 주소값에 의해서만 참조되고 사용됨

> code, data, stack은 컴파일 시 크기 결정, heap은 런타임 시 크기 결정 <br>
code, data는 컴파일 시 메모리 할당
stack, heap은 런타임 시 할당

<출처: stack의 크기 결정 시기 "Stack size is determined at compile time but memory is allocated at runtime." (Source: "Modern Compiler Implementation in C" by Andrew W. Appel)>
<br/>


## 프로세스의 컴파일 과정

> 프로그램은 컴파일러가 컴파일하여 컴퓨터가 이해하는 기계어로 번역되는 파일이 되는 것을 의미한다.
C 언어 기반의 프로그램은 컴파일을 거쳐야 하지만 파이썬 같은 인터프리터 언어는 컴파일 과정 필요 없이 한줄씩 읽어서 실행한다.

- 전처리: 코드에서 주석을 제거하고 #include 같은 헤더 파일을 병합해 매크로를 치환한다.
- 컴파일러: 오류 처리, 코드 최적화를 하고 어셈블리어로 변환한다.
- 어셈블러: 어셈블리어는 목적 코드(object code)로 변환된다.
- 링커: 프로그램 내에 있는 라이브러리/파일들과 목적 코드를 결합해서 실행 파일을 만든다. 실행 파일은 .exe/.out 확장자를 가진다.


## PCB(Process Control Block)
>운영체제가 프로세스를 제어하기 위해 정보(CPU 레지스터 값들)를 저장해 놓는 곳으로 프로세스의 상태 정보를 저장하는 구조체이다.
프로세스 생성시 PCB 가 만들어지며 주기억장치에 저장되다가 프로세스가 완료되면 PCB도 함께 제거된다.

### PCB의 구조
- 포인터: 프로세스의 현재 위치를 저장하는 포인터 정보

- 프로세스 상태: 프로세스의 상태 (생성, 준비, 실행, 대기, 종료) 에 대한 정보를 저장

- 프로세스 식별자: 모든 프로세스에는 각 프로세스를 식별하는 고유한 ID, PID 가 할당

- 프로그램 계수기: 프로세스가 실행해야 하는 다음 명령어의 주소

- 레지스터: 누산기, 베이스, 레지스터 및 범용 레지스터를 포함하는 CPU 레지스터에 있는 정보

- 메모리 제한: 운영 체제에서 사용하는 메모리 관리 시스템에 대한 정보가 포함
  페이지 테이블, 세그먼트 테이블 등이 포함될 수 있음

### 컨텍스트 스위칭
> CPU가 현재 작업중인 프로세스에서 다른 프로세스로 넘어갈 때, 이전의 프로세스 정보를 PCB에 저장하고 새롭게 실행할 프로세스의 정보를 PCB에서 읽어와 레지스터에 적재하는 과정을 말한다.

## 멀티프로세싱
> 멀티 프로세스는 운영체제에서 하나의 응용 프로그램에 대해 동시에 여러 개의 프로세스를 실행할 수 있게 하는 기술을 말한다.<br>
하나의 부모 프로세스가 여러 개의 자식 프로세스를 생성함으로서 다중 프로세스를 구성하는 구조이다.<br>
한 프로세스는 실행되는 도중 프로세스 생성 시스템 콜을 통해 새로운 프로세스들을 생성할 수 있는데,<br> 다른 프로세스를 생성하는 프로세스를 부모 프로세스(Parent Process)라 하고, 다른 프로세스에 의해 생성된 프로세스를 자식 프로세스(Child Process)라 한다.
부모 프로세스와 자식 프로세스는 각각 고유한 PID(Process ID)를 가지고 있다.<br>부모 프로세스는 자식 프로세스의 PID를 알고 있으며, 이를 통해 자식 프로세스를 제어할 수 있다. 또한, 자식 프로세스는 부모 프로세스의 PID와 PPID(Parent Process ID)를 알고 있어, 이를 통해 부모 프로세스와의 통신이 가능하다.
다만, 부모 프로세스와 자식 프로세스는 엄연히 서로 다른 프로세스로 독립적으로 실행되며,<br>독립적인 메모리 공간을 가지고 있어 서로 다른 작업을 수행한다. 대표적인 예로 웹 브라우저의 상단 탭(Tab) 이나 새 창을 들 수 있다. 각 브라우저 탭은 같은 브라우저 프로그램 실행이지만, 각기 다른 사이트 실행을 행하기 때문이다.

### IPC(Inter Process Communication)
> 프로세스는 커널이 제공하는 IPC 설비를 이용해서 프로세스간 통신을 할 수 있다.

## 스레드
>  하나의 프로세스 내에 있는 실행 흐름.


## 멀티스레딩
> 하나의 프로세스 안에 여러개의 스레드가 있는 것을 말한다. 따라서 하나의 프로그램에서 두가지 이상의 동작을 동시에 처리하도록 하는 행위가 가능해진다.

멀티 스레드는 하나의 프로세스 내에서 여러 개의 스레드를 생성되기 때문에, heap 영역과 같은 공유 메모리에 대해 스레드 간에 자원을 공유가 가능하다. 이를 통해, 프로세스 간 통신 (IPC)을 사용하지 않고도 데이터를 공유할 수 있기 때문에, 자원의 효율적인 활용이 가능해 시스템 자원 소모가 줄어든다.