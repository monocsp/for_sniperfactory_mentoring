# Object에 대하여

# TypeScript에서 Object 예시

## 클래스 정의 및 객체 생성

```typescript
class Car {
  make: string;
  model: string;
  speed: number;

  constructor(make: string, model: string) {
    this.make = make;
    this.model = model;
    this.speed = 0;
  }

  accelerate(amount: number): void {
    this.speed += amount;
  }

  brake(amount: number): void {
    this.speed -= amount;
  }
}

// 객체 생성
const myCar = new Car("Toyota", "Corolla");
myCar.accelerate(30);
console.log(`Speed: ${myCar.speed}`); // Output: Speed: 30
myCar.brake(10);
console.log(`Speed: ${myCar.speed}`); // Output: Speed: 20
```

## 정의

- **객체(Object)**는 프로그래밍에서 데이터와 이 데이터를 처리하는 방법(메서드)을 하나로 묶은 단위입니다.
- 객체는 특정 클래스의 인스턴스이며, 클래스는 객체의 청사진 또는 설계도입니다.

## 주요 특징

1. **상태 (State)**

   - 객체는 데이터를 저장하는 속성(프로퍼티)을 가지고 있습니다.
   - 예: 자동차 객체의 `속도`, `색상`, `제조사` 등.

2. **행위 (Behavior)**

   - 객체는 데이터를 처리하는 함수(메서드)를 가지고 있습니다.
   - 예: 자동차 객체의 `가속`, `제동` 등.

3. **식별성 (Identity)**
   - 객체는 고유의 식별자를 가지며, 이를 통해 다른 객체와 구별됩니다.
   - 예: 각각의 자동차 객체는 고유한 차량 식별 번호(VIN)를 가질 수 있습니다.

## 객체의 구성 요소

- **프로퍼티(Properties)**: 객체가 가지는 데이터 또는 상태를 나타냅니다.
- **메서드(Methods)**: 객체가 수행할 수 있는 동작이나 기능을 나타냅니다.

## 객체의 장점

1. **재사용성**: 객체는 재사용 가능한 코드 블록을 만듭니다. 한 번 정의된 클래스는 여러 인스턴스로 재사용될 수 있습니다.
2. **모듈성**: 객체는 소프트웨어를 모듈화하여, 유지보수와 확장을 쉽게 만듭니다.
3. **캡슐화**: 객체는 데이터를 은닉하고, 메서드를 통해 데이터에 접근하도록 하여 데이터 보호와 무결성을 유지합니다.

객체 지향 프로그래밍(Object-Oriented Programming, OOP)은 이러한 객체를 사용하여 소프트웨어를 설계하고 구현하는 패러다임입니다. OOP의 주요 개념으로는 클래스, 객체, 상속, 다형성, 캡슐화 등이 있습니다.
