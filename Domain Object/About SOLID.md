# SOLID에 대하여

[SOLID in NextJS](https://dev.to/fajarriv/solid-principle-in-nextjs-using-typescript-3l3k)

[Mastering NextJS](https://iqbalpa.medium.com/mastering-next-js-best-practices-for-clean-scalable-and-type-safe-development-2ee5693e73a9)

# SOLID 원칙

SOLID는 객체 지향 프로그래밍 및 설계에서 따를 수 있는 다섯 가지 기본 원칙을 나타내는 약어입니다. 이 원칙들은 소프트웨어의 유연성, 유지보수성, 확장성을 향상시키기 위해 고안되었습니다.

## 1. SRP: 단일 책임 원칙 (Single Responsibility Principle)

- **원칙**: 클래스는 하나의 책임만 가져야 하며, 클래스는 그 책임을 완전히 캡슐화해야 합니다.
- **설명**: 하나의 클래스는 하나의 기능 또는 하나의 책임만 가져야 합니다. 클래스가 여러 책임을 가지게 되면 변경 사항이 발생했을 때 영향을 받는 부분이 많아집니다.

### 단일 책임 원칙 위반한 예시

```typescript
class User {
  constructor(public name: string, public email: string) {}

  // 사용자 정보 저장
  save(): void {
    // 데이터베이스에 사용자 정보 저장 로직
    console.log(`Saving user: ${this.name}`);
  }

  // 이메일 전송
  // User 클래스가 이메일 전송 방법이 변경되면 변경이 되어야 하므로 잘못된 방식
  sendEmail(message: string): void {
    // 이메일 전송 로직
    console.log(`Sending email to ${this.email}: ${message}`);
  }
}

// 객체 생성 및 사용
const user = new User("Alice", "alice@example.com");
user.save(); // Output: Saving user: Alice
user.sendEmail("Welcome!"); // Output: Sending email to alice@example.com: Welcome!
```

### 예시

```typescript
class User {
  constructor(public name: string, public email: string) {}
}

class UserRepository {
  addUser(user: User) {
    // 사용자 추가 로직
  }

  removeUser(user: User) {
    // 사용자 제거 로직
  }
}

class EmailService {
  sendEmail(user: User, message: string) {
    // 이메일 전송 로직
  }
}
```

## 2. OCP: 개방-폐쇄 원칙 (Open/Closed Principle)

- **원칙**: 소프트웨어 엔티티(클래스, 모듈, 함수 등)는 확장

가능하지만, 변경에는 닫혀 있어야 합니다.

- **설명**: 기존 코드를 수정하지 않고 기능을 추가할 수 있어야 합니다. 새로운 기능이 필요하면 기존 코드를 수정하지 않고, 새로운 클래스를 추가하는 방식으로 확장해야 합니다.

## OCP 원칙을 위배하는 예시

### 예시 코드

```typescript
class Rectangle {
  constructor(public width: number, public height: number) {}
}

class Circle {
  constructor(public radius: number) {}
}
/// AreaCalculator 클래스는 새로운 도형을 추가할 때마다 calculateArea 메소드를 수정해야한다.
/// AreaCalculator 클래스는 변경에 닫혀있지 않으므로 OCP에 위배된다.
class AreaCalculator {
  calculateArea(shape: any): number {
    if (shape instanceof Rectangle) {
      return shape.width * shape.height;
    } else if (shape instanceof Circle) {
      return Math.PI * shape.radius ** 2;
    }
    return 0;
  }
}

// 사용 예시
const rectangle = new Rectangle(10, 20);
const circle = new Circle(5);
const calculator = new AreaCalculator();

console.log(calculator.calculateArea(rectangle)); // Output: 200
console.log(calculator.calculateArea(circle)); // Output: 78.53981633974483
```

### 예시 코드

```typescript
interface Shape {
  area(): number;
}

class Circle implements Shape {
  constructor(private radius: number) {}

  area(): number {
    return Math.PI * this.radius ** 2;
  }
}

class Rectangle implements Shape {
  constructor(private width: number, private height: number) {}

  area(): number {
    return this.width * this.height;
  }
}

class AreaCalculator {
  calculate(shapes: Shape[]): number {
    return shapes.reduce((total, shape) => total + shape.area(), 0);
  }
}

// 사용 예시
const shapes: Shape[] = [new Circle(5), new Rectangle(10, 20)];
const calculator = new AreaCalculator();
console.log(calculator.calculate(shapes)); // Output: 278.53981633974485
```

## 3. LSP: 리스코프 치환 원칙 (Liskov Substitution Principle)

- **원칙**: 자식 클래스는 언제나 자신의 부모 클래스를 대체할 수 있어야 합니다.
- **설명**: 자식 클래스는 부모 클래스의 기능을 온전히 수행해야 하며, 이를 위해 부모 클래스의 계약을 준수해야 합니다.

### 예시

```typescript
class Bird {
  fly(): string {
    return "I can fly";
  }
}

class Eagle extends Bird {
  fly(): string {
    return "I am an eagle, I can fly high";
  }
}

class Penguin extends Bird {
  fly(): string {
    throw new Error("I cannot fly");
  }

  swim(): string {
    return "I can swim";
  }
}

function letBirdFly(bird: Bird) {
  console.log(bird.fly());
}

// 사용 예시
const eagle = new Eagle();
const penguin = new Penguin();

letBirdFly(eagle); // Output: I am an eagle, I can fly high
// letBirdFly(penguin);  // Error: I cannot fly
```

## 4. ISP: 인터페이스 분리 원칙 (Interface Segregation Principle)

- **원칙**: 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫습니다.
- **설명**: 인터페이스는 클라이언트의 필요에 맞춰 분리되어야 하며, 클라이언트는 자신이 사용하지 않는 메서드에 의존하지 않아야 합니다.

### 예시

```typescript
interface Workable {
  work(): void;
}

interface Eatable {
  eat(): void;
}

class Worker implements Workable, Eatable {
  work(): void {
    console.log("Working");
  }

  eat(): void {
    console.log("Eating");
  }
}

class Robot implements Workable {
  work(): void {
    console.log("Working");
  }
}

// 사용 예시
const human = new Worker();
const machine = new Robot();

human.work(); // Output: Working
human.eat(); // Output: Eating
machine.work(); // Output: Working
```

## 5. DIP: 의존 역전 원칙 (Dependency Inversion Principle)

- **원칙**: 고수준 모듈은 저수준 모듈에 의존해서는 안 되며, 이 둘은 모두 추상화에 의존해야 합니다.
- **설명**: 구현이 아닌 추상화에 의존함으로써, 상호 의존성을 줄이고 시스템의 유연성을 높입니다.

### 예시

```typescript
interface Logger {
  log(message: string): void;
}

class ConsoleLogger implements Logger {
  log(message: string): void {
    console.log(message);
  }
}

class FileLogger implements Logger {
  log(message: string): void {
    // 파일에 로그 작성 로직
    console.log(`Writing to file: ${message}`);
  }
}

class UserService {
  constructor(private logger: Logger) {}

  createUser(name: string): void {
    // 사용자 생성 로직
    this.logger.log(`User ${name} created`);
  }
}

// 사용 예시
const consoleLogger = new ConsoleLogger();
const fileLogger = new FileLogger();

const userServiceWithConsoleLogger = new UserService(consoleLogger);
userServiceWithFileLogger.createUser("Alice"); // Output: User Alice created

const userServiceWithFileLogger = new UserService(fileLogger);
userServiceWithFileLogger.createUser("Bob"); // Output: Writing to file: User Bob created
```

이 예시들은 TypeScript에서 SOLID 원칙을 적용하는 방법을 보여줍니다. SOLID 원칙을 준수하면 코드의 유지보수성, 확장성, 재사용성을 크게 향상시킬 수 있습니다.
