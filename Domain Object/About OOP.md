# 객체 지향 프로그래밍 (Object-Oriented Programming, OOP)

## 정의

- **객체 지향 프로그래밍(OOP)**는 소프트웨어 개발에서 객체(Object)를 중심으로 설계하고 구현하는 프로그래밍 패러다임입니다.
- 객체는 데이터와 이 데이터를 조작하는 메서드를 하나로 묶은 것입니다.

## 주요 개념

1. **클래스(Class)**

   - 객체를 생성하기 위한 청사진 또는 설계도입니다.
   - 클래스는 객체의 속성(프로퍼티)과 동작(메서드)을 정의합니다.

2. **객체(Object)**

   - 클래스의 인스턴스입니다.
   - 객체는 상태(데이터)와 행위(메서드)를 가지며, 서로 다른 객체는 독립적인 데이터를 가질 수 있습니다.

### Person 클래스 정의

```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): string {
    return `Hello, my name is ${this.name} and I am ${this.age} years old.`;
  }
}

// 객체 생성 및 사용
const person1 = new Person("Alice", 30);
console.log(person1.greet()); // Output: Hello, my name is Alice and I am 30 years old.
```

3. **상속(Inheritance)**

   - 한 클래스가 다른 클래스의 속성과 메서드를 상속받아 재사용하는 것입니다.
   - 상속을 통해 코드 재사용성을 높이고, 클래스 간의 관계를 정의할 수 있습니다.

```typescript
class Student extends Person {
  grade: string;

  constructor(name: string, age: number, grade: string) {
    super(name, age); // 부모 클래스의 생성자 호출
    this.grade = grade;
  }

  study(): string {
    return `${this.name} is studying in grade ${this.grade}.`;
  }
}
```

4. **다형성(Polymorphism)**

   - 같은 메서드나 속성 이름이 다양한 객체에서 다르게 동작하는 것입니다.
   - 다형성은 주로 메서드 오버라이딩(override)과 오버로딩(overload)을 통해 구현됩니다.

```typescript
class Teacher extends Person {
  subject: string;

  constructor(name: string, age: number, subject: string) {
    super(name, age);
    this.subject = subject;
  }

  teach(): string {
    return `${this.name} is teaching ${this.subject}.`;
  }
}

// 다형성 예시
const people: Person[] = [
  new Student("Charlie", 18, "Senior"),
  new Teacher("David", 45, "Mathematics"),
];

people.forEach((person) => {
  console.log(person.greet());
  if (person instanceof Student) {
    console.log((person as Student).study());
  } else if (person instanceof Teacher) {
    console.log((person as Teacher).teach());
  }
});

// Output:
// Hello, my name is Charlie and I am 18 years old.
// Charlie is studying in grade Senior.
// Hello, my name is David and I am 45 years old.
// David is teaching Mathematics.
```

5. **캡슐화(Encapsulation)**

   - 객체의 데이터(속성)를 숨기고, 공개된 메서드를 통해서만 접근하도록 하는 것입니다.
   - 캡슐화는 데이터 보호와 객체 간의 독립성을 유지하는 데 도움을 줍니다.

```typescript
class Person {
  private ssn: string; // Private 속성
  public name: string;
  public age: number;

  constructor(name: string, age: number, ssn: string) {
    this.name = name;
    this.age = age;
    this.ssn = ssn;
  }

  greet(): string {
    return `Hello, my name is ${this.name} and I am ${this.age} years old.`;
  }

  getSSN(): string {
    return this.ssn; // Private 속성 접근을 위한 공개 메서드
  }
}

// 객체 생성 및 사용
const person2 = new Person("Eve", 25, "123-45-6789");
console.log(person2.greet()); // Output: Hello, my name is Eve and I am 25 years old.
console.log(person2.getSSN()); // Output: 123-45-6789
```

6. **추상화(Abstraction)**
   - 불필요한 세부 사항을 숨기고, 중요한 개념이나 기능만을 드러내는 것입니다.
   - 추상화는 복잡성을 줄이고, 객체의 인터페이스를 단순화합니다.

```typescript
abstract class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  abstract work(): string; // 추상 메서드

  greet(): string {
    return `Hello, my name is ${this.name} and I am ${this.age} years old.`;
  }
}

class Engineer extends Person {
  work(): string {
    return `${this.name} is working as an engineer.`;
  }
}

// 객체 생성 및 사용
const engineer = new Engineer("Frank", 35);
console.log(engineer.greet()); // Output: Hello, my name is Frank and I am 35 years old.
console.log(engineer.work()); // Output: Frank is working as an engineer.
```
