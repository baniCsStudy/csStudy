객체지향의 특징 4가지를 간단하게 설명해주세요
캡슐화, 상속성, 추상화, 다형성

객체지향이나 절차지향으로 프로그래밍 해본 경험과 왜 해당 패러다임을 사용했는지 간단하게 설명해주세요
# 프로그래밍 패러다임

## 객체 지행의 특징
- 추상화: 복잡한 시스템에서 핵심개념, 기능만 간추려낸것
- 캡슐화: 객체의 속성과메서드를 하나로 묶고 일부를 외부에 감추어 은닉하는것
- 상속성: 상위클래스의 특성을 하위클래스가 이어받아 재사용하거나 확장하는것 
- 다형성: 하나의 메서드나 클래스가 다양한 방법으로 동작하는것(오버로딩, 오버라이딩)
> - 오버로딩: 같은이름을 가진 메서드를 여러개 두는것(메서드 타입, 매개변수 유형, 갯수 등으로 여러개 구현. 정적다형성. 컴파일중 발생)
> - 오버라이딩: 메서드 오버라이딩을 주로 의미. 상위클래스로부터 상속받은 메서드를 하위클래스가 재정의 하는것(동적다형성. 런타임중 발생)

## 설계원칙(SOLID)

S : 단일책임 원칙 - 모든클래스는 하나의 책임만 가져야함  
O : 개방-폐쇄원칙 - 유지보수시 쉽게 확장가능하고 수정할땐 닫혀있어야함. 기존코드는 잘 변경하지 않고 확장은 쉬워야함.  
L : 리스코프 치환 원칙 - 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위타입 인스턴스로 바꿀 수 있어야함.부모자식객체가 바뀌어도 문제없어야함.  
I : 인터페이스 분리 원칙 - 하나의 일반적인터페이스보다 구체적인 여러개의 이터페이스를 만들어야함.  
D : 의존역전 원칙 - 자신보다 변하기 쉬운것에 의존하던것을 추상화된 인터페이스나 상위클래스를 두어 변하기 쉬운것의 변화에 영향받지 않게하는 원칙  
