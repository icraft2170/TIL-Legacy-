---
title: Observer Pattern
---

# 옵저버 패턴
- 한 객체의 상태가 바뀌면 그 객체에 의존하는 다른 객체들한테 연락이 가고 자동으로 내용이 갱신되는 방식으로 `일대다(one-to-many)의존성`을 정의합니다.
- `Subject`가 데이터의 변화등의 변화를 감지하면 그에 대한 내용을 `Subject`가 추가한  `Observer`들에게 정보를 전달하는 패턴으로.


## 디자인 원칙 (Loose Coupling)

- 서로 상호작용을 하는 객체 사이에서는 가능하면 `느슨하게 결합하는 디자인`을 사용해야 한다.
- 이렇게 느슨한 결합을 하는 디자인에서는 유지보수가 쉬워진다.


> `느슨하게 결합하는 디자인(Loose Couping)`이란?
- 적은 동등 
- 낮은 의존도 (독립성↑ 캡슐화??)
- 적은 데이터 흐름 (왜? 어째서?)


>`--> 추상적으로 다가오는 부분이 있다. 많은 예시로 구체화 시켜나갈 필요가 있음<--`


### Subject와 Observer 인터페이스의 구성


```java
public interface Subject{
    public void registerObserver(Observer o);
    public void removeObserver(Observer o);
    public void notifyObserver();
}

public interface Observer{
    public void update(전달되는 파라미터);
}
```

### Subject 인터페이스 구현

```java
public OnClickListener implements Subject {
    private ArrayList observers;
    // 옵저버 등록시 저장할 ArrayList
    private double clickLocationX;
    private double clickLocationY;
    
    public OnClickListener(){
        observers = new ArrayList();
    }

    // 옵저버 등록
    public void registerObserver(Observer o){
        observers.add(o);
    }

    // 옵저버 삭제
    public void removeObserver(Observer o){
        int i = observers.indexOf(o);
        if (i >= 0) {
            observers.remove(i);
        }
    }


    public void notifyObserver(){
        for (int i=0; i< observers.size();i++){
            Observers observer = (Observer)observers.get(i);        
            observer.update(clickLocationX,clickLocationY)
        }
    }

    public void clickMonitor() {
        notifyObserver();
    }

    public void setClickMonitor(double clickLocationX,double clickLocationY){

        this.clickLocationX=clickLocationX;
        this.clickLocationY=clickLocationY;
        clickMonitor();
    }
    // 왜 notifyObserver();를 직접 넣지 않고 한단계 거쳤을까... 이렇게되면 반응이 오지 않았을때도 기능을 실현할 수 있게될텐데?(의문)
}
```


### Observer 구현


```java
public interface ButtonAction{
    public void action();
}

public class PlusButton implement Observer, ButtonAction{
    private double xLocation;
    private double yLocation;
    private double clickLocationX;
    private double clickLocationY;
    private Subject onClickListener;

    public PlusButton(Subject onClickListener,double xLocation,double yLocation){
        this.onClickListener = onClickListener;
        // 객체에 대한 레퍼런스를 저장해 두면 유용하게 쓸 수 있을 것입니다.(탈퇴시)
        onClickListener.registerObserver(this);
        this.xLocation=xLocation;
        this.yLocation=yLocation;
        // Subject객체에 옵저버 등록
    }

    public update(double clickLocationX,double clickLocationY){
        this.clickLocationX = clickLocationX;
        this.clickLocationY = clickLocationY;
        if((xLocation==clickLocationX)&&(yLocation==clickLocationY)){
            action();
        }
    }

    public void action(){
        System.out.print("+");
    }

}


public class MinusButton implement Observer, ButtonAction{
    private double xLocation;
    private double yLocation;
    private double clickLocationX;
    private double clickLocationY;
    private Subject onClickListener;

    public PlusButton(Subject onClickListener,double xLocation,double yLocation){
        this.onClickListener = onClickListener;
        // 객체에 대한 레퍼런스를 저장해 두면 유용하게 쓸 수 있을 것입니다.(탈퇴시)
        onClickListener.registerObserver(this);
        this.xLocation=xLocation;
        this.yLocation=yLocation;
        // Subject객체에 옵저버 등록
    }

    public update(double clickLocationX,double clickLocationY){
        this.clickLocationX = clickLocationX;
        this.clickLocationY = clickLocationY;
        if((xLocation==clickLocationX)&&(yLocation==clickLocationY)){
            action();
        }
    }

    public void action(){
        System.out.print("-");
    }

}

```

### TEST 구현

```java
public class ButtonStation{
    public static void main(String[] args){
        OnClickListener onClickListener = new OnClickListener();

        PlusButton plusButton = new PlusButton(onClickListener,10.0,20.0);
        MinusButton minusButton = new MinusButton(onClickListener,20.0,10.0);

        onClickListener.setClickMonitor(10.0,20.0);
        // "+"출력
        onClickListener.setClickMonitor(20.0,10.0);
        // "-"출력
    }
}

```