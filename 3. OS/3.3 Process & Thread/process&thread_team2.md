# 프로세스와 스레드

## 관련 질문
<details>
  <summary>1, 3, 0, 3, 5, 6, 3의 참조 페이지를 3개의 페이지 프레임을 가진 기억장치에서 FIFO 알고리즘을 사용하여 교체했을 때 '6'과 교체되는 페이지는 무엇인가요.</summary>
  <blockquote>
    FIFO 알고리즘은 오래된 페이지가 우선적으로 교체되는 방식을 따릅니다. 따라서 3개의 프레임에 (1, 3, 0) (1, 3, 0) (5, 3, 0) (5, 6, 0) (5, 6, 3) 으로 할당됩니다. 그러므로 '6'과 교체되는 페이지는 '3' 입니다.
  </blockquote>
</details>
<br/>
<details>
  <summary>임계영역과 경쟁 조건에 대해 설명하고 해결방법이 무엇인지 설명해주세요.</summary>
  <blockquote>
    임계 영역은 둘 이상의 스레드가 동시에 되는 상황이 되어 접근 타이밍 등에 따라 결과값이 달라지는 상태인 경쟁조건을 발생시킬 수 있는 코드 블록을 의미합니다. 공유된 자원에 여러 프로세스가 동시에 접근하면 임계 영역 안에서 경쟁 조건이 발생할 수 있습니다. 이를 해결하기 위해 한번에 하나의 프로세스만 접근할 수 있도록 제한을 두는 방식을 취해야하고 대표적으로 뮤텍스, 세마포어, 모니터를 활용하는 방식이 있습니다.
  </blockquote>
</details>
<br/>
<details>
  <summary>IPC에 대하여 설명하고 관련된 예시를 들어주세요.</summary>
  <blockquote>
    IPC(Inter Process Communication)는 프로세스간 데이터를 주고받고 공유 데이터를 관리하는 메커니즘 입니다. 종류로는 공유 메모리, 파일, 소켓, 익명 파이프, 명명된 파이프, 메시지 큐 등이 있습니다. 
  </blockquote>
</details>
<br/>

<hr/>

### 프로세스와 컴파일 과정

- **프로세스:** 컴퓨터에서 실행되고 있는 프로그램
- **스레드:** 프로세스 내 작업의 흐름을 의미

- **컴파일 과정**
1. 전처리 : 소스코드의 주석을 제거하고 헤더 파일을 병합해 매크로를 치환한다.
2. 컴파일러 : 오류 처리, 코드 최적화 작업을 하고 어셈블리어로 변환한다.
3. 어셈블러 : 어셈블리어는 목적 코드로 변환되며 확장자는 운영체제 마다 다르다.
4. 링커 : 프로그램 내의 라이브러리 함수 또는 다른 파일들과 목적 코드를 결합하여 .exe .out 의 확장자를 갖는 실행 파일을 만든다.


### 프로세스의 상태

- 생성 상태 : 프로세스가 생성된 상태, fork(), exec() 함수를 통해 생성, PCB가 할당된다.
    - fork : 부모 프로세스의 주소 공간을 그대로 복사하며 새로운 자식 프로세스를 생성하는 함수
    - exec : 새롭게 프로세스를 생성하는 함수
- 대기 상태 : 메모리 공간이 충분하면 메모리를 할당 받고 그렇지 않으면 대기한다. CPU 스케줄러로부터 소유권이 넘어오기를 기다리는 상태
- 대기 중단 상태 : 메모리 부족으로 일시 중단된 상태
- 실행 상태 : CPU 소유권과 메모리를 할당받고 인스트럭션을 수행 중인 상태, CPU burst가 일어났다고도 표현
- 중단 상태 : 어떤 이벤트가 발생한 후 기다리며 프로세스가 차단된 상태. 입출력 장치에 의한 인터럽트로 이런 현상이 많이 발생한다.
- 일시 중단 상태 : 대기 중단과 유사한 상태
- 종료 상태 : 메모리와 CPU 소유권 모두 놓고 가는 상태

### 프로세스의 메모리 구조

1. 스택과 힙
    - 동적 할당 : 런타임 단계에서 메모리를 할당 받는 것
    - 스택 : 지역 변수, 매개 변수, 실행되는 함수에 의해 늘어나거나 줄어드는 메모리 영역
        - 함수가 호출될 때마다 호출될 때의 환경 등 특정 정보가 스택에 계속해서 저장
        - 잠시 사용했다가 사라지는 데이터를 저장하는 영역
    - 힙 : 동적으로 할당되는 변수들을 담는다. 런타임 시 크기가 결정된다.

2. 데이터 영역과 코드 영역
    - 정적 할당 : 컴파일 단계에서 메모리를 할당하는 것
    - BSS segment : 전역 변수 또는 static, const로 선언되어 있고 초기화되지 않은 변수들이 할당
    - Data segment : 전역 변수 또는 static, const로 선언되어 있고 0이 아닌 값으로 초기화된 변수가 할당
    - code segment : 프로그램의 코드가 들어간다.

### PCB

- 운영체제에서 프로세스에 대한 메타데이터를 저장한 데이터를 의미한다.

- **PCB의 구조**
- 프로세스 스케줄링 상태 : 프로세스가 CPU에 대한 소유권을 얻은 이후의 상태
- 프로세스 ID
- 프로세스 권한 : 컴퓨터 자원 또는 I/O 디바이스에 대한 권한 정보
- 프로그램 카운터 : 프로세스에서 실행해야 할 다음 명령어의 주소에 대한 포인터
- CPU 레지스터 : 프로세스 실행을 위해 저장해야 할 레지스터에 대한 정보
- CPU 스케줄링 정보 : CPU 스케줄러에 의해 중단된 시간 등에 대한 정보
- 계정 정보: CPU 사용량, 실행한 유저의 정보
- I/O 상태 정보 : 프로세스에 할당된 I/O 디바이스 목록

- **컨텍스트 스위칭**
- PCB를 기반으로 프로세스의 상태를 저장하고 로드시키는 과정
- 한 프로세스에 할당된 시간이 끝나거나 인터럽트에 의해 발생한다.
- 싱글 코어 작업의 경우 프로세스 A의 PCB를 저장한 후 프로세스 B의 PCB를 로드한다. 인터럽트 또는 시스템콜이 발생하면 프로세스 B의 PCB를 저장한 후 프로세스 A의 PCB를 로드한다.
- 컨텍스트 스위칭이 일어날 때 유휴시간이 발생한다.
- 비용으로 캐시미스가 발생한다.

### 멀티프로세싱

- 여러 개의 프로세스를 통해 동시에 두 가지 이상의 일을 수행할 수 있는 것
- 하나 이상의 일을 병렬 처리 할 수 있으며, 다른 메모리나 프로세스에 문제가 생겨도 다른 프로세스를 통해 처리할 수 있다.

- 웹 브라우저
    - 웹 브라우저의 멀티프로세스 구조
        - 브라우저 프로세스 : 주소 표시줄, 북마크 막대, 뒤로가기 버튼 등을 담당. 네트워크 요청이나 파일 접근 같은 권한을 담당한다.
        - 렌더러 프로세스 : 웹 사이트가 보이는 부분의 모든 것을 제어
        - 플러그인 프로세스 : 웹 사이트에서 사용되는 플러그인을 제어
        - GPU 프로세스 : GPU를 이용해서 화면을 그리는 부분을 제어

- IPC(Inter Process Communication) : 프로세스끼리 데이터를 주고받고 공유 데이터를 관리하는 메커니즘 
    - 공유 메모리
        - 여러 프로세스에 동일한 메모리 블록에 대한 접근 권한이 부여되어 프로세스가 서로 통신할 수 있도록 공유 메모리를 생성해서 통신하는 것
    - 파일
        - 디스크에 저장된 데이터 또는 파일 서버에서 제공한 데이터
    - 소켓
        - 동일한 컴퓨터의 다른 프로세스나 네트워크의 다른 컴퓨터로 네트워크 인터페이스를 통해 전송하는 데이터
    - 익명 파이프
        - 프로세스 간에 FIFO 방식으로 읽히는 임시 공간인 파이프를 기반으로 데이터를 주고 받으며 단방향 방식의 읽기 전용, 쓰기 전용 파이프를 만들어서 작동하는 방식
    - 명명된 파이프
        - 파이프 서버와 하나 이상의 파이프 클라이언트 간의 통신을 위한 명명된 단방향 또는 양방향 파이프
    - 메시지 큐
        - 메시지를 큐 데이터 구조 형태로 관리하는 것

### 스레드와 멀티스레딩

- 스레드
    - 프로세스의 실행 가능한 가장 작은 단위
- 멀티스레딩
    - 프로세스 내 작업을 여러 개의 스레드로 처리하는 기법

### 공유 자원과 임계 영역

1. 공유 자원
    - 시스템 안에서 각 프로세스, 스레드가 함께 접근할 수 있는 모니터, 프린터, 메모리, 파일, 데이터 등의 자원이나 변수
    - 경쟁 상태: 공유 자원을 두 개 이상의 프로세스가 동시에 읽거나 쓰는 상황, 접근의 타이밍이나 순서 등에 의해 결과 값이 영향을 받을 수 있는 상태

2. 임계 영역
    - 둘 이상의 프로세스, 스레드가 공유 자원에 접근할 때 순서 등의 이유로 결과가 달라지는 코드 영역
    - 임계 영역을 해결하기 위한 방법은 크게 뮤텍스, 세마포어, 모니터 세 가지가 있다.

### 교착 상태(Deadlock)
- 두 개 이상의 프로세스들이 서로가 가진 자원을 기다리며 중단된 상태
- 교착 상태의 원인
    - 상호 배제: 한 프로세스가 자원을 독점해 접근이 불가능한 상태
    - 점유 대기: 특정 프로세스가 점유한 자원을 다른 프로세스가 요청하는 상태
    - 비선점: 다른 프로세스의 자원을 강제적으로 가져올 수 없음
    - 환형 대기: 서로가 서로의 자원을 요구하는 상황

- 교착 상태의 해결 방법
    - 자원 할당시 적절한 설계
    - ‘은행원 알고리즘’
    - 교착 상태가 발생하면 사이클이 있는지 찾아보고 관련된 프로세스를 제거한다.
    - 교착 상태를 처리하는 비용이 크므로 발생 시 사용자가 작업을 종료한다.