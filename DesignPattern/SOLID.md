# ✨ SOLID 원칙

- 시간이 지나도 유지보수와 확장이 쉬운 소프트웨어를 만드는데 사용되는 원칙
- 디자인패턴의 장점, 필요성 등을 설명할 때 꼭 필요한 원칙
- a.k.a. 객체지향 5대 원칙
- 각 원칙의 첫 글자를 따서 만든 명칭

# 1️⃣ SRP (Single Responsibility Principle, 단일 책임 원칙)

```
어떤 클래스를 변경해야하는 이유는 오직 하나
```

- 변경해야하는 이유 = 책임!
- 따라서, 1클래스 1책임이라는 원칙
- 만약 책임이 많아지면, 한 책임의 변화가 다른 책임에 영향을 주게 됨 ㅜㅜ
- 이 원칙을 만족하면 불필요한 상속 및 구현을 줄여 **가독성이 좋아지고 유지보수가 쉬워지며, 재사용성이 높아짐!**

# 2️⃣ OCP (Open-Closed Principle, 개방폐쇄원칙)

```
기존의 코드를 변경하지 않고 기능을 수정하거나 추가할 수 있도록 설계
```

- 변경 => Closed
- 수정하거나 추가 => Open
- 즉, 확장에 열려있고 변경에 닫혀 있는 설계를 해야한다는 원칙
- 이를 만족하지 않으면 새로운 기능을 추가하는 것이 어려워지는 변경의 유연함과 관련된 원칙
- 변하는 부분과 변하지 않는 부분을 구분해 설계하면 해당 원칙을 만족할 수 있음

# 3️⃣ LSP (Liskov Substitution Principle, 리스코프 치환법칙)

```
부모 객체와 이를 상속한 자식 객체가 있을 때 부모 객체를 호출하는 동작에서 자식 객체가 부모 객체를 완전히 대체할 수 있어야 함
```

## 🟨 3-1. 리스코프 치환법칙의 대표적인 예시 - 직사각형과 정사각형

### ① Rectangle - 직사각형 Class

```
public class Rectangle
{
    protected int width;
    protected int height;
    
    // 너비 반환 함수
    public int getWidth()
    {
        return width;
    }

    //너비 할당 함수
    public void setWidth(int width)
    {
        this.width = width;
    }

    // 높이 반환 함수
    public int getHeight()
    {
        return height;
    }

    // 높이 할당 함수
    public void setHeight(int height)
    {
        this.height = height;
    }
    
    // 넓이 반환 함수
    public int getArea()
    {
        return width * height;
    }
}
```

- Rectangle은 직사각형을 구현한 객체
- 너비와 높이를 지정하고 반환할 수 있으며 지정된 값으로 자신의 넓이를 계산할 수 있음
- 정사각형도 직사각형의 한 종류이니 직사각형을 상속하면 정사각형 객체를 쉽고 빠르게 만들 수 있을 것 같음


### ② Square - 정사각형 Class

```
public class Square extends Rectangle
{
    // 너비 할당 함수
    @Override
    public void setWidth(int width)
    {
        super.setWidth(width);
        super.setHeight(getWidth());
    }
    
    // 높이 할당 함수
    @Override
    public void setHeight(int height)
    {
        super.setHeight(height);
        super.setWidth(getHeight());
    }
}
```

- 직사각형 객체 Rectangle을 상속해 정사각형 객체 Square를 쉽게 구현함
- 정사각형은 너비와 높이가 같으므로 너비와 높이를 일치시켜주도록 오버라이딩을 수행함

### ③ Rectangle 넓이 구하기

```
public class Main
{
    public static void main(String[] args)
    {
        Rectangle rectangle = new Rectangle();
        rectangle.setWidth(10);
        rectangle.setHeight(5);
        
        System.out.println(rectangle.getArea());
    }
}
```

```
// OUTPUT
50
```

- 너비 10 높이 5인 직사각형의 넓이 50이 정상적으로 반환

### ④ Square로 넓이 구하기

- 리스코프 치환원칙에 따르면 부모 객체를 자식 객체가 완전히 대체할 수 있다 함
- 따라서, Rectangle을 상속받은 Square로 대체해 넓이를 다시 구해보자
- 해당 결과도 상기 결과와 같이 50이 반환되어야 함!

```
public class Main
{
    public static void main(String[] args)
    {
        Rectangle rectangle = new Square();
        rectangle.setWidth(10);
        rectangle.setHeight(5);
        
        System.out.println(rectangle.getArea());
    }
}
```

```
// OUTPUT
25
```

- 마지막에 수행된 ```setHeight(5)```가 객체의 너비와 높이를 모두 5로 할당함
- 따라서, 넓이도 25가 반환된 것!
- 즉, 해당 코드는 리스코프 치환 원칙에 위배되는 코드
- 곰곰히 생각해보면 직사각형과 정사각형은 사각형의 특징을 서로 가지고 있긴 하지만 모두 사각형의 종류일 뿐 하나가 다른 하나를 완전히 포함하는 구조가 아님
- 이렇게 잘못된 객체를 상속하거나 올바르게 확장하지 못 할 경우 겉으로 보기엔 정상적이지만 올바른 객체가 아님

## 🟩 3-2. 정리

- 상속되는 객체는 부모 객체를 완전히 대체해도 반드시 아무런 문제가 없어야 한다는 뜻
- 부모 객체의 동작을 완벽하게 대체할 수 있는 관게만 상속하도록 코드를 설계해야 함
- 이를 지키기 위해 가급적 부모 객체의 일반 메소드를 그 의도와 다르게 오버라이딩 하지 않게 해야 함
- 자식 객체가 자신만의 동작을 추가하기 위해 부모 객체의 모세도를 오버리아딩한다는 걸 감안하면 준수하기 까다로운 원칙

# 4️⃣ ISP (Interface Segregation Principle, 인터페이스 분리 원칙)

```
클라이언트는 자신이 사용하지 않는 메소드에 의존 관계를 맺으면 안됨
```

- 클라이언트에서 Interface와 논리적으로 결합되어 필요한 메소드만 호출해 낮은 의존성을 가지라는 뜻
- 단일책임원칙과 연관
- ISP(인터페이스 분리 원칙)와 SRP(단일 책임 원칙)은 객체가 커지지 않도록 막는 원칙
- 이를 통해 변경 시 영향을 최소화할 수 있음!

# 5️⃣ DIP (Dependency Inversion Principle, 의존관계 역전 원칙)

```
고수준 모듈이 저수준 모듈에 의존해서는 안되고 저수준 모듈이 고수준 모듈에서 정의한 추상타입에 의존해야 함
```

![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/42f9996c-fd34-4f50-bbd7-0610d5bc0222)

> ✋ 여기서 잠깐! 고수준 모듈과 저수준 모듈은 뭘까?
> - 고수준 모듈 : 어떤 의미 있는 단일 기능을 제공하는 모듈 (interface, 추상 클래스)
> - 저수준 모듈 : 고수준 모듈의 기능을 구현하기 위해 필요한 하위 기능의 실제 구현 (메인클래스, 객체)

- 요구사항이 정해지면 상세수준(저수준모듈, 구체적인 클래스)의 변경이 발생할 가능성이 높아짐
- 하지만, 상위수준(고수준모듈, 인터페이스 혹은 추상클래스)은 한 번 안정화되면 쉽게 변하지 않기 때문입니다!
- 사실 고수준 클래스가 저수준 클래스를 사용하므로 고수준 클래스가 저수준 클래스에 의존하는 것이 자연스러워 보일 수 있음
- 하지만, 고수준이 저수준에 의존하게 되면 저수준 클래스의 빈번한 변경과 새로운 것을 추가하는 행위에 고수준 클래스가 영향을 받기 쉬우므로 의존관계를 역전시켜야 함

---

###### 참고

- [[디자인패턴] SOLID 원칙](https://velog.io/@cchloe2311/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4-SOLID-%EC%9B%90%EC%B9%99)
- [[OOP] 객체지향 5원칙(SOLID) - 리스코프 치환 원칙(Liskov Subsituation Principle)](https://blog.itcode.dev/posts/2021/08/15/liskov-subsitution-principle)
- [[OOP] 객체지향 5대 원칙(SOLID) - 의존성 역전 원칙 (DIP)](https://velog.io/@harinnnnn/OOP-%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5-5%EB%8C%80-%EC%9B%90%EC%B9%99SOLID-%EC%9D%98%EC%A1%B4%EC%84%B1-%EC%97%AD%EC%A0%84-%EC%9B%90%EC%B9%99-DIP)
