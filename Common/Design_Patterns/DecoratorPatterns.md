---
title: 데코레이터 패턴
---

# 데코레이터 패턴(Decorator Pattern)

## OCP(Open-Closed-Principle)
- 클래스는 확장에 대해서는 열려 있어야 하지만 코드 변경에 대해서는 닫혀 있어야 한다.
    - 클래스는 추가를 통해 코드 기능을 확장할 수는 있어야 하지만 이미 작성된 코드를 변경하는 것으로 해당 클래스를 사용하는 다른 클래스들에게 영향을 주어서는 안된다. 
    
    - 해석?: 하위버전에 호환성을 지키기 위해서는 현재 사용하던 상태로 사용가능해야하지만 코드중복을 막기위해 해당 클래스를 확장하여 새로운 기능을 사용할 수 있도록 할 수 있어야 한다는 의미???


## 데코레이터 패턴
- 객체에 추가적인 요건을 `동적`으로 첨가한다. 데코레이터는 `서브 클래스를 만드는 것`을 통해서 `기능을 유연하게 확장`할 수 있는 방법을 제공


- 데코레이터의 수퍼클래스는 자신이 장식하고 있는 객체의 수퍼클래스와 같다.
- 한 객체를 여러 개의 데코레이터로 감쌀 수 있다.
- 데코레이터는 자신이 감싸고 있는 객체와 같은 슈퍼클래스를 가지고 있기때문에 원래 객체가 들어갈 자리에 데코레이터 객체를 집어넣어도 상관 없습니다.
- `데코레이터는 자신이 장식하고 있는 객체에게 어떤 행동을 위임하는 것 외에 원하는 추가적인 작업을 수행할 수 있습니다.`
- 객체는 언제든지 감쌀 수 있기 때문에 실행중에 필요한 데코레이터를 마음대로 적용할 수 있습니다.

### 데코레이터 `추상 구성요소` 구현

```java
public abstract class Window {
    String opName="Window"

    public String getOperatingSystem(){
        return opName;
    }
    // 운영체제 이름을 리턴해주는 시스템

    public abstract double cost();
    // 가격을 넘겨주는 메서드
}
// 운영체제의 수퍼클래스를 추상클래스로 생성한다.
```

### 데코레이터 `구상 구성요소` 구현

```java
public class Window10 extends Window {
    public Window10(){
        opName = "window10"
    }

    public double cost(){
        return 133.4;
    }
}

public class Window7 extends Window {
    public Window7(){
        opName = "window7"
    }

    public double cost(){
        return 100.4;
    }
}

```

### 데코레이터 `추상 데코레이터` 구현

```java

public abstract class WindowDecorator extends Window{
    public abstract String getOperatingSystem();
}


public class Home extends WindowDecorator{
    Window window;

    public Home(Window window){
        this.window=window;
    }

    public String getOperatingSystem(){
        return window.getOperatingSystem() + " HOME";
    }

    public double cost(){
        return window.cost()+ 30.0;
    }

}

public class Pro extends WindowDecorator{
    Window window;

    public Pro(Window window){
        this.window=window;
    }

        public String getOperatingSystem(){
        return window.getOperatingSystem() + " PRO";
    }

    public double cost(){
        return window.cost()+ 50.0;
    }
}

public class Professional extends WindowDecorator{
    Window window;

    public Professional(Window window){
        this.window=window;
    }

        public String getOperatingSystem(){
        return window.getOperatingSystem() + " Professional";
    }

    public double cost(){
        return window.cost()+ 70.0;
    }
}
```


### 데코레이터 테스트 코드

```java
public class WindowsTest{
    public static void main(String args[]){
        Window window = new Window7()
        System.out.println(window.getOperatingSystem() + " $" + window.cost());
        // Window7 $ 100.4
        Window window2 = new Window10()
        window2 = new Home(window2);
        System.out.println(window2.getOperatingSystem() + " $" + window2.cost());
        // Window10 HOME $ 163.4
        Window window3 = new Window10()
        window3 = new Pro(window3);
        window3 = new Professional(window3);
        System.out.println(window3.getOperatingSystem() + " $" + window3.cost());
        // Window10 PRO Professional $ 253.4
    }

}

```
