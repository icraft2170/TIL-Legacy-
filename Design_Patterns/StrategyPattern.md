---
title: 스트래티지 패턴(strategy pattern)
author: 손현호
---

# 스트래티지 패턴

- 알고리즘군을 정의하고 각각을 캡슐화하여 교환해서 사용할 수 있도록 만든다. 스트래지티 패턴을 활용하면 알고리즘을 사용하는 클라이언트와는 독립적으로 알고리즘을 변경할 수 있다.


## 상속

객체지향 프로그램에서 상속은 코드 재사용을 위해 부모클래스에 구현한 멤버및 메서드들을 자손 클래스에서 사용 할 수 있도록 하는것을 이야기한다.

```java
class Car{
    void driving(){
        //code
    };
}

class SportCar extends Car{
    void driving(){
        // overiding
    };
}

class CampingCar extends Car{
    void driving(){
        // overiding
    };
}

class ElectricCar extends Car{
    void driving(){
        // overiding
    };
}

```

위와 같이 이루어진 `Car`라는 클래스는 run() 이라는 `행동`을 할 수 있다. 이 때 기술 진보로 몇몇 차량에 자동 주행 기술(`automaticDriving()`)이라는 메서드를 추가해야 했다.

```java
class Car{
    void driving(){
        //code
    };

    void automaticDriving(){
        print("자동주행함.");
    }
}

class SportCar extends Car{
    void driving(){
        // overiding
    };
}

class CampingCar extends Car{
    void driving(){
        // overiding
    };
}

class ElectronicCar extends Car{
    void driving(){
        // overiding
    };
}

```

그래서 이와 같이 부모 클래스에 `자동주행기술`을 추가하게 되면 문제가 발생한다. 자동 주행 기술은 `SportCar와 ElectronicCar`에만 추가 되어야하는데, `CampingCar`에도 상속에 의해 추가되어 사용할 수 없는 기술이 추가되었다. <u>코드를 변경하는 과정에서 의도치 않은 결과가 생기는 것이다</u>

```java
interface AutoDriveable{
    void automaticDriving();
}


class Car{
    void driveng(){
        //code
    };
}

class SportCar extends Car implements AutoDriveable{
    void driving(){
        // overiding
    };
    
    void automaticDriving(){
        //overiding
    }
}

class CampingCar extends Car{
    void driving(){
        // overiding
    };
}

class ElectronicCar extends Car implements AutoDriveable{
    void driving(){
        // overiding
    };
    
    void automaticDriving(){
        //overiding
    }
}
```

위에 문제를 해결해주기 위해 `automaticDriving()` 메서드를 포함한 `AutoDriveable`이라는 인터페이스를 만들어 그 기능을 사용할 클래스에만 `구현`을 시켜 사용 할 수 있다. 하지만 이런 방법은 Car에 상속되는 수많은 클래스들중 해당 기능을 사용하는 내용을 전부 오버라이딩 해주어야 하고 이렇게 되면 많은 `코드중복`이 생긴다.

```java
interface AutoDriveBehavior{
    void automaticDriving();
}

class AutoStartDrive implements AutoDriveBehavior{
    void automaticDriving(){
        print("자동 주행 시작");
    }
}

class AutoStopDrive implements AutoDriveBehavior{
    void automaticDriving(){
        print("자동 주행 종료");
    }
}

```

인터페이스 `AutoDriveable`을 상속하는 클래스를 만들어 `automaticDriving()`을 구현 하게 하는 방법으로 행동을 클래스로 `캡슐화`하여 관련된 비슷한 행동들을 하나의 `알고리즘군`으로 묶어 냈다. 이 때 `AutoDriveable` 타입으로 각 하위클래스의 인스턴스를 생성함으로서 해당 알고리즘군의 행동들을 `다형성`을 이용하여 기능을 변경해 줄 수 있다.



```java
class Car{

    AutoDriveBehavior autodirve;

    Car(){
        autodirve = new AutoStopDrive();
    }

    void driving(){
        //code
    };

    void performAutoDriving(){
        autodirve.automaticDriving();
    }

    void setDriveBehavior(AutoDriveBehavior ad){
        autodrive = ad;
    }
    
}

```
`AutoDriveBehavior` 타입의 변수를  클래스 내부에 생성하고 그 클래스의 메서드를 호출을 해주는 `행동 메서드`를 만들어 행동 메서드에 `행동을 위임(delegation)`합니다
이렇게 행동을 위임하고 인스턴스의 생성을 동적으로 지정해줄 수 있는 `setDriveBehavior()`메서드를 사용하여 `알고리즘군` 내에서 `행동을 바꿔`가면서 행동할 수 있도록 해 줄 수 있습니다.

```java

class AutoCarTest{
    main(){
        Car myCar = new SportCar();
        myCar.performAutoDriving(); 
        //Car생성자로서 기본 값인 AutoStopDrive의 자동주행 안함 상태가 실행된다.
        myCar.setDriveBehavior(new AutoStartDrive());
        // 행동 알고리즘군중 AutoStartDrive()로 인스턴스를 변경
        myCar.performAutoDriving(); 
        // 변경된 행동 알고리즘인 자동주행 수행 상태가 실행된다. 
    }
}
```

이렇게 `알고리즘군`을 독립하여 `캡슐화` 함으로서 해당 알고리즘 군의 행동을 변경하거나. 코드를 대량으로 오버라이딩 하여 코드중복의 문제가 생기는 등의 상황을 피할 수 있게되었다.
이와 같이 특정 행동의 알고리즘 군을 클래스로 캡슐화시켜 구성을 활용해 사용할 수 있도록 한것을 `스트래티지 패턴` 이라고 한다.

> `has a` 관계를 우리는 구성(composition)을 이용하는 것이라고 부름


### 디자인 원칙

1. 애플리케이션의 달라지는 부분을 찾아내고, 달라지지 않는 부분으로부터 분리시킨다.
1. 구현이 아닌 인터페이스에 맞춰서 프로그래밍한다.
1. 상속보다는 구성을 활용합니다.
