🟣 디자인 패턴이란?

프로그램을 설계할 때 자주 발생했던 문제점들을 피하기 위해 하나의 '규약' 형태로 만들어 놓은 설계 패턴.

🟣 사용 이유

디자인 패턴을 참고하여 개발할 경우 개발의 **효율성**과 **유지보수성**, **운용성**이 높아지며 프로그램의 **최적화**에 도움이 된다.


🟣 디자인 패턴 유형

> 목적에 따라 생성, 구조, 행위 패턴으로 나눌 수 있다. 
**생성** 패턴은 **객체 인스턴스 생성**에 관여하며 _클래스 정의와 객체 생성 방식을 구조화, 캡슐화_ 하는 패턴이다.
**구조** 패턴은 **더 큰 구조 형성 목적**으로 클래스나 객체의 조합을 다루며 
**행위** 패턴은 클래스나 객체들이 **상호작용**하는 방법과 **역할 분담**을 다루는 패턴을 의미한다.

**[ 생성 패턴 : 5개 ]**
✅ 싱글톤 패턴
-
**📌 개념**
싱글톤 패턴(Singleton pattern)은 전역 변수를 사용하지 않고 객체를 하나만 생성하도록 하며, 생성된 객체를 어디에서든지 참조할 수 있도록 하는 디자인 패턴이다. **(1 클래스 1 객체)**

**📌 장점**
- 하나의 인스턴스를 만들어 놓고 해당 인스턴스를 다른 모듈들이 공유하며 사용하기 때문에 인스턴스 생성에 드는 비용을 줄일 수 있다.
- 메모리 낭비를 방지한다.
- 다른 클래스의 인스턴스들이 데이터를 공유하기 쉽다.

**📌 단점**
- 멀티 스레드 환경에서는 하나의 인스턴스만 생성됨을 보장하지 않는다.
- 싱글톤 인스턴스가 너무 많은 일을 하거나 많은 데이터를 공유시킬 경우 모듈 간의 결합을 강하게 만들 수 있다.
- 테스트(TDD)에서 문제가 된다. 단위 테스트에서 테스트가 서로 독립적이어야 하며 테스트를 어떤 순서로든 실행할 수 있어야 하는데, 싱글톤 인스턴스는 자원을 공유하고 있기 때문에 테스트가 결정적으로 격리된 환경에서 수행되려면 매번 인스턴스의 상태를 초기화시켜줘야 한다.

```
# 보통, 싱글톤 객체의 .get_instance() 로 인스턴스를 받아온다.
singleton_1 = Singleton.get_instance()
singleton_2 = Singleton.get_instance()

# 이렇게 받아온 두 인스턴스는 동일한 인스턴스다.
singleton_1 == singleton_2  # True
```
---
✅ 프로토타입(Prototype) 패턴
-
**📌 개념**
기존의 인스턴스를 그대로 복제(clone) 하여 새로운 객체를 생성하는 방법이다. (싱글톤과 반대개념)

**📌 장점**
- 객체를 생성해주기 위한 별도의 객체 생성 클래스가 필요하지 않다.
- 객체의 각 부분을 조합해서 생성되는 형태에도 적용이 가능하다.

**📌 단점**
- 생성될 객체들의 자료형인 클래스들이 모두 clone() 메서드를 구현해야 한다.

**📌 활용 상황**
- 런타임에 새로운 클래스를 추가하고 삭제할 때 유용하다.
- 동적으로 클래스에 따라 응용프로그램을 설정해야 할 때 유용하다.

**자바에서 Stack Memory & Heap Memory**

https://jiwondev.tistory.com/86

```
# 보통, 프로토타입 객체의 .clone() 으로 인스턴스를 복사한다.
original = Prototype()
prototype = original.clone()

# 이렇게 받아온 두 인스턴스는 동일한 객체는 아니지만, 내부 데이터는 같다.
original == prototype  # False
original.data == prototype.data  # True
```
![24](https://user-images.githubusercontent.com/60287901/208282952-01f4f8c6-7c7a-49f4-aaf6-ea9e65fd317e.png)

---
✅ 팩토리메서드(Factory Method) 패턴
-
**📌 개념**
상속 관계에 있는 두 클래스에서 상위 클래스가 중요한 뼈대(인터페이스)를 결정하고, 하위 클래스가 객체 생성에 관한 구체적인 내용(인스턴스 생성)을 결정하는 패턴이다.

**📌 장점**
- 상위 클래스가 하위 클래스와 분리되기 때문에 **느슨한 결합**을 가지게 된다.
- 상위 클래스에서는 하위 인스턴스 생성 방식에 대해 전혀 알 필요가 없기 때문에 **유연성**이 높아지며 **유지보수성**이 증가한다.
- 수정에는 닫혀있고 확장에는 열려있다(Open-Closed Principle=OCP 원칙을 지킬 수 있음)

**📌 단점**
- 클래스가 많아진다.

```
# 보통, Factory 객체의 `get` 메쏘드의 파라미터로 생성할 객체의 타입을 넘겨준다.
samsung_keyboard = KeyboardFactory.get_keyboard("samsung")
lg_keyboard = KeyboardFactory.get_keyboard("lg")

# 생성된 객체는 다음과 같이 구체적인 클래스 인스턴스다.
samsung_keyboard  # SamsungKeyboard
lg_keyboard  # LgKeyboard
```

---
✅ 추상팩토리(Abstract Factory) 패턴
-
**📌 개념**
구체적인 클래스를 지정하지 않고 관련성이 있거나, 독립적인 객체들을 생성하기 위한 인터페이스를 제공하는 패턴이다.

**📌 장점**
- 팩토리 메서드 패턴과 마찬가지로 수정에는 닫혀 있고 확장에는 열려있다.
- 여러 개의 비슷한 집합 객체 생성을 하나의 팩토리에 모아둘 수 있다.

**📌 단점**
- 클래스가 많아진다.

🙄 팩토리 메서드와 추상팩토리의 차이점이 뭔데욥?

가장 큰 차이점은 팩토리 메서드 패턴은 어떤 객체를 생성할지에 집중하고 추상 팩토리 패턴은 연관된 객체(팩토리)들을 모아둔다는 것에 집중합니다.

```
# 키보드 팩토리의 팩토리(추상 팩토리)를 통해 키보드 팩토리를 얻는다.
CommonKeyboardFactory = AbstarctKeyboardFactory.get_keyboard_factory("common")

# 이후는 팩토리 패턴과 동일하다.
samsung_common_keyboard = CommonKeyboardFactory.get_keyboard("samsung")
lg_common_keyboard = CommonKeyboardFactory.get_keyboard("lg")

samsung_keyboard  # SamsungCommonKeyboard
lg_keyboard  # LgCommonKeyboard
```

---
✅ 빌더(Builder) 패턴
-
**📌 개념**
복잡한 인스턴스를 조립하여 만드는 구조로, 복합 객체를 생성할 때 객체를 생성하는 방법(과정)과 객체를 구현(표현)하는 방법을 분리함으로써 동일한 생성 절차에서 서로 다른 표현 결과를 만들 수 있는 디자인 패턴
** get, set, 메소드 분리해서 만드는게 빌더패턴!

**📌 장점**
- 생성 과정이 복잡한 인스턴스를 일관된 프로세스로 생성할 수 있다.
- 빌더의 메서드를 체이닝 형태로 호출하며 자연스럽게 인스턴스를 구성하고 최종적으로 객체를 생성하도록 유도할 수 있다. 
- 멤버 변수의 초기화와 검증을 각각의 멤버 변수별로 분리해서 작성할 수 있다.

**📌 단점**
- 클라이언트는 구체적인 인스턴스를 생성하기 전에 반드시 빌더를 생성해야 한다.
- 관리해야 할 클래스가 많아지고 구조가 복잡하다.

```
Student kangworld = new Student
    .StudentBuilder(32140033)
    .setName("kangworld")
    .setPhoneNumber("010-1234-5678")
    .setGrade("sophomore")
    .getStudent();
```
---

[코드 참조 velog]
https://velog.io/@ha0kim/Design-Pattern-%EA%B5%AC%EC%A1%B0-%ED%8C%A8%ED%84%B4Structural-Patterns

**[ 구조 패턴 : 7개 ]**
✅ 어댑터(Adapter) 패턴
-
**📌 개념**
인터페이스가 호환되지 않는 클래스들을 함께 이용할 수 있도록, 타 클래스의 인터페이스를 기존 인터페이스에 덧씌운다.
![22](https://user-images.githubusercontent.com/60287901/208283014-60ebd98d-f33a-4c4c-af34-c20f5c4ab039.png)

> 클라이언트에서 어댑터를 사용하는 방법
1. 클라이언트에서 타겟 인터페이스를 사용하여 메소드를 호출함으로써 어댑터에 요청을 한다.
2. 어댑터에서는 어댑티 인터페이스를 사용하여 그 요청을 어댑티에 대한 하나 이상의 메소드 호출로 변환한다.
3. 클라이언트에서는 호출 결과를 받긴 하지만 중간에 어댑터가 껴 있는지는 알지 못한다.


**📌 장점**
- 관계가 없는 인터페이스 간 같이 사용 가능
- 프로그램 검사 용이
- 기존 코드를 변경하지 않아도 되기 때문에 클래스 재활용성 증가

**📌 단점**
- 구성요소를 위해 클래스를 증가시켜야 하기 때문에 복잡도 증가
- 클래스 Adapter의 경우 상속을 사용하기 때문에 유연하지 못하다.
- 객체 Adapter의 경우 대부분의 코드를 다시 작성해야 하기 때문에 효율적이지 못하다.

---
✅ 브리지(Bridge) 패턴
-
**📌 개념**
구현부에서 추상층을 분리하여 각자 독립적으로 변형할 수 있게 하는 패턴이다.
추상적 개념(추상클래스, extends)과 구체적 구현(인터페이스, implements)을 서로 다른 두개의 인터페이스로 구현하는 디자인 패턴!
브릿지 패턴은 **캡슐화**(encapsulation),**집합**(aggregation)을 사용하고 다른 클래스들로 책임을 분리시키기 위해 **상속**(inheritance)를 사용한다.


**📌 장점**
- **인터페이스와 구현이 분리**된다.
- 서로 **독립적으로 확장**할 수 있다.
- 구현 세부사항을 클라이언트에게 은닉하여 캡슐화를 지킬 수 있다.

**📌 단점**
- 디자인이 복잡해진다.

**📌 활용 상황**
- 런타임에 실제로 사용될 구체적인 구현체가 결정되어야 할 때 유용하다.
- 구현할 클래스의 기능부 및 구현부가 지속적인 확장 가능성이 있을 때 유용하다.


---
✅ 합성 패턴(Composite pattern)
-
**📌 개념**
객체들의 관계를 트리 구조로 구성하여 전체-부분 계층을 표현하는 패턴으로 여러 개의 객체들로 구성된 복합 객체와 단일 객체를 클라이언트에서 구별없이(같은 타입으로!) 다루게 한다.
또한, 복합 객체(전체)와 단일 객체(leaf)를 같은 타입으로 취급하기 위한 인터페이스로 Component를 선언하는데, left 클래스와 전체에 해당하는 Composite 클래스에 공통 인터페이스를 정의한다.

**📌 장점**
- 전체-부분의 관계(Ex. Directory-File)를 갖는 객체들 사이의 관계를 정의할 때 유용하다.
- 클라이언트는 전체와 부분을 구분하지 않고 동일한 인터페이스를 사용할 수 있다.
- 객체들이 모두 같은 타입으로 취급되기 때문에 새로운 클래스 추가가 용이하다.

**📌 단점**
- 설계를 일반화 시켜 객체간의 구분, 제약이 힘들다.

**📌 활용 상황**
- 객체들 간에 계급 및 계층구조가 있고 이를 표현해야할 때
- 클라이언트가 단일 객체와 집합 객체를 구분하지 않고 동일한 형태로 사용하고자 할 때



---
✅ 데코레이터 패턴(Decorator Pattern)
-
**📌 개념**
객체의 결합을 통해 기능을 동적으로 유연하게 확장할 수 있게 해주는 패턴
객체에 추가적인 요건을 **동적으로 첨가**하며 기능 확장이 필요할 때 서브 클래스 대신 쓸 수 있는 유일한 대안이 될 수 있다.

즉, 기본 기능(ConcreteComponent)에 추가할 수 있는 기능의 종류가 많은 경우에 각 추가 기능을 Decorator 추상 클래스로 정의한 후 필요한 Decorator 객체(ConcreteDecorator)를 조합함으로써 추가 기능의 조합을 설계 하는 방식이다.

> 
합성패턴과 같이 ConcreteComponent와 Decorator 두 객체를 동등하게 다루기 위한 인터페이스인 Component가 상위에 존재한다.

**📌 장점**
- 객체에 동적으로 기능 추가가 간단하게 가능하다.

**📌 단점**
- 자잘한 데코레이터 클래스들이 계속 추가되어 클래스가 많아질 수 있다.
- 객체의 정체를 알기 힘들고 복잡해질 수 있다.

**📌 활용 상황**
객체가 상황에 따라 다양한 기능이 추가되거나 삭제되어야 할 때

```
public class ChristmasTreeMain {

    public static void main(String[] args) {
    
        // Christmas tree
        ChristmasTree tree = new DefaultChristmasTree();
        System.out.println(tree.decorate());

        // Christmas tree + Lights
        ChristmasTree treeWithLights = new Lights(
                new DefaultChristmasTree()
        );
        
        System.out.println(treeWithLights.decorate());

        // Christmas tree + Lights + Flowers
        ChristmasTree treeWithLightsAndFlowers = new Flowers(
                new Lights(
                        new DefaultChristmasTree()
                )
        );
        
        System.out.println(treeWithLightsAndFlowers.decorate());
    }
}
```
![23](https://user-images.githubusercontent.com/60287901/208283040-7244edee-ecc6-465b-84c3-0627bd7808b2.png)


🙄 기본 객체인 new DefaultChristmasTree() 에 기능 추가를 new Lights(new DefaultChristmasTree()); 와 같이 동적인 방식으로 하고 있다. 이게 가능한 이유는?

A. Decorator 객체의 생성자로 Component를 받음으로써 Decorator를 이어 붙일 수가 있고 super를 통해 넘어오는 Component 의 operation(decorate()) 을 먼저 수행하기 때문이다.
(이건 크리스마스 트리 관련 코드 볼 것)

---
✅ 프록시 패턴(Proxy Pattern)
-
**📌 개념**
실제 기능을 수행하는 객체(Real Object) 대신 **가상의 객체**(Proxy Object)를 사용해 로직의 흐름을 제어하는 디자인 패턴이다.
구체적인 업무를 담당하고 있는 클래스에 접근하기 전에, 간단한 사전 작업(전처리, 캐싱) 처리하는 클래스(Proxy)를 두는 구조를 프록시 패턴이라고 한다.
이 패턴은 주요 기능이 요청을 받아 수행하기 전에, 이 요청에 대한 부가적인 전처리들을 수행하는 로직을 세우고 싶을 때 사용한다.

**📌 장점**
- 기본 객체의 리소스가 무거운 경우, 프록시 객체에서 간단한 처리를 하거나 기본 객체를 캐싱 처리함으로써 부하를 줄일 수 있다.
- 기본 객체에 대한 수정 없이, 클라이언트에서의 사용과 기본 객체 사이에 일련의 로직을 프록시 객체를 통해 넣을 수 있다.
- 프록시는 기본 객체와 요청 사이에 있기 때문에, 일종의 방패(보안)의 역할도 한다.

**📌 단점**
- 프록시 객체가 중간에 껴있기 때문에, 간혹 응답이 느려질 수 있다. (캐싱이 안되어있는 초기 사용의 경우)

**📌 활용 상황**
- **기본 객체가 리소스 집약적**인 경우. 자잘한 작업들은 프록시 객체가 처리하게 한다.
- **기본 객체에 접근을 제어**해야하는 경우. 프록시 객체가 권한에 따라 접근 로직을 다르게 처리하게 한다.


---
✅ 퍼사드 패턴(Facade Pattern)
-
**📌 개념**
Facade (외관)는 "건물의 정면"을 의미하는 단어로 어떤 소프트웨어의 다른 커다란 코드 부분에 대하여 간략화된 인터페이스를 제공해주는 디자인 패턴을 의미한다.
서브 시스템에 있는 인터페이스들에 대한 통합 인터페이스를 제공하여 서브 시스템을 더 쉽게 사용할 수 있도록 만드는 더 높은 수준의 인터페이스.

**📌 장점**
- 서브 시스템에 대한 의존성을 한곳으로 모을 수 있다.(캡슐화)

**📌 단점**
- 퍼사드 클래스가 서브 시스템에 대한 모든 의존성을 가지게 된다.

---
플라이웨이트,,안해욥!

**[ 구조 패턴 : 11개 ]**
✅ 옵저버(Observer) 패턴
-
**📌 개념**
객체의 상태 변화를 관찰하는 관찰자들, 즉 옵저버들의 목록을 객체에 등록하여 **상태 변화**가 있을 때마다 메서드 등을 통해 객체가 직접 목록의 각 옵저버에게 통지하도록 하는 디자인 패턴

주체 객체와 상태의 변경을 알아야 하는 관찰 객체(Observer Object)는 1:1 or 1:N 관계


**📌 장점**
- 실시간으로 한 객체의 **변경사항을 다른 객체에 전파**할 수 있다.
- 느슨한 결합으로 시스템이 유연하고 객체간의 의존성을 제거할 수 있다.

**📌 단점**
- 너무 많이 사용하면 상태관리가 힘들다.
- 데이터 배분에 문제가 생길 수 있다.


---
✅ 전략(Strategy) 패턴
-
**📌 개념**
특정 컨텍스트에서 알고리즘을 별도로 분리하는 설계 방법

```
	// 전략패턴이 적용되지 않은 경우
    public class Calculator {
    
    	public double calculate(boolean isFirstGuest, boolean isLastGuest, List<Item> items) {
    		double sum = 0;
    		for (Item item : items) {
    			if (isFirstGuest) {
    				sum += item.getPrice() * 0.9;
    			} else if (!item.isFresh()) {
    				sum += item.getPrice() * 0.8;
    			} else if (isFirstGuest) {
    				sum += item.getPrice() * 0.8;
    			} else {
    				sum += item.getPrice();
    			}
    		}
    		return sum;
    	}
    }
    
    public class Item {
    	private final String name;
    	private final int price;
    
    	public Item(String name, int price) {
    		this.name = name;
    		this.price = price;
    	}
    
    	public int getPrice() {
    		return price;
    	}
    
    	public boolean isFresh() {
    		return true;
    	}
    }
```

계산이라는 컨텍스트에서 적용되는 다양한 할인 알고리즘을 별도로 관리하면 if-else 분기문 사용안하고 생성자로 코드 작성 가능!

**📌 장점**
- 컨텍스트 코드의 변경 없이 새로운 전략을 추가할 수 있다.
> 예를 들어 새로운 전략인 중간 손님을 대폭할인하는 정책이 추가되었다고 가정해보겠습니다. 그러면 아래와 같이 변할 것입니다.
기존 코드 : else-if 문이 추가될 것입니다.
전략패턴이 적용된 코드 : 새로운 클래스가 추가될 것입니다.
즉, 요구사항이 변경되었을 때 기존의 코드를 변경하지 않아도 된다는 것이 전략패턴의 장점이며 **새로운 전략에 대해서는 새로운 클래스를 통해 관리**하기 때문에 **OCP의 원칙**을 준수할 수 있는 패턴입니다

**📌 단점**
- 모든 상황에서 전략패턴이 유용한 것은 아니다.



---
나머지는 안녕,,,,

