# TYPESCRIPT

### TypeScript란?

1. Language

2. Compile Language (cf. Java Script : Interpreted Languate)  

   : 컴파일 과정에서 **Type**이 가장 중요하다.

3. Transpile

4. 정적 타입 언어

5. Source Code(Type Script) -> Compile(Type Script Compiler) => Java Script

---

### 각종 명령어

1. npm init -y : npm 패키지 생성
2. npm i typescript : typescript 설치
3. npm run transpile : npm 스크립트로 파일 컴파일
   - package.json 파일 **transpile : tsc 파일명**
   - .ts => .js
4. npm i typescript -g : typescript를 글로벌하게 설치
5. tsc 파일명.ts : cli 명령어로 컴파일
6. tsc --init : 컴파일러 초기 Setting
   - tsconfig.json  파일 생성
   - target, module등 설정
   - tsconfig.json 파일이 있으면 tsc 명령어로 컴파일 가능
7. tsc -w : watch 모드(변경되면 변경을 탐지해서 컴파일)

---

### 기본 자료형

사용자가 만든 타입은 결국 기본 자료형들로 쪼개진다.

##### JavaScript 기본 자료형

- Boolean
- Number
- String
  - Template Sting
    - 행에 걸쳐 있거나, 표현식을 넣을 수 있는 문자열
    - 표현식은 ${expr} 형태로 사용
- Null
- Undefined
- Symbol
- Array
  - Array<Type>
  - Type[]

##### TypeScript 기본 자료형

- Any(최대한 쓰지 않는게 좋다.)
- Void
- Never
- Enum
  - 원소의 결과값은 string 형
- Tuple
  - 배열인데 타입이 한 가지가 아닌 경우

---

### 변수 선언

##### var

- 함수 스코프
- 호이스팅 가능(변수 선언이 밑에 있어도 변수 사용 가능)
- 재선언 가능

##### let, const

- const는 타입을 명시하지 않으면 리터럴 타입으로 인식
- 블록 스코프
- 호이스팅 불가
- 재선언 불가

---

### Type Assertions

*타입이 이것이다.*라고 컴파일러에게 알려주는 것

형변환(실제 데이터 구조 변환)과는 다르다.

방법

- 변수 as 강제할 타입
- <강제할 타입> 변수

---

### TypeAlias

인터페이스와 유사해 보임

~~~ typescript
let a: any;
let b: string|number;
b = '스트링';
b = 0

function test(arg: string|number): string|number{
  return arg;
}

type StringOrNumber = string|number;
let c: StringOrNumber;

function test2(arg: StringOrNumber): StringOrNumber{
  return arg;
}
~~~

---

### Interface

~~~ typescript
const person: {name: string, age: number} = {
  name: "Jione",
  age: 23
};

interface Person{
  name: string;
  age: number;
  address?: string;
}

const inPerson: Person = {
  name: "jione",
  age: 23
};

function hello(p: Person): void{
  console.log('안녕하세요 ${p.name} 입니다.');
}
~~~

##### indexable type

2가지 Type만 설정 가능 : string, number

~~~typescript
interface Person2{
  [index: number]: string;
}

const p2: Person2 = {};
p2[0] = 'hi';
p2[100] = 'hello';

interface StringArrayDictionary{
  [index: number]: string;
  [index: string]: string;
}
const aad: StringArrayDictionary = {};
add[100] = '백';
add.hundred = '백';
~~~

##### function in interface 

~~~typescript
interface Person{
  name: string;
  hello(): string;
}

const person: Person = {
  name: 'Mark',
  hello(): string{
    return 'Hello';
  }
};
~~~

##### class implements interface

~~~typescript
interface IPerson{
  name: string;
  hello(): void;
}

class Person implements IPerson{
  name: string = null;
  
  constructor(name: string){
    this.name = name;
  }
  
  hello(): void{
    console.log('안녕하세요 ${this.name} 입니다.');
  }
}

const person: Person = new Person('Mark');
//인터페이스의 선언만 사용하겠다.
const person: IPerson = new Person('Mark2');
~~~

##### interface extends interface

~~~typescript
interface Person{
  name: string;
  age?: number;
}

interface Korean extends Person{
  city: string;
}

const k: Korean = {
  name: '최지원',
  city: '서울'
};
~~~

---

### Class

~~~typescript
class Person{
    name: string;
    age: number;

    constructor(name: string) {
        this.name = name;
    }
}

const person = new Person('Jione');
console.log(person.name);
~~~

~~~typescript
class Person{
  protected _name: string = 'Mark';
  private _age: number = null;
  
  constructor(name: string, age: number){
    this._name = name;
    this._age = age;
  }
  
  hello(): void{
    console.log(this._name);
  }
}

const person: Person = new Person('Jione', 23);
person.hello();
~~~

~~~typescript
class Person{
  constructor(protected _name: string, protected _age: number){
  }
  
  hello(): void{
    console.log(this._name);
  }
}
const person: Person = new Person('Jione', 23);
person.hello();
~~~

##### 상속

~~~typescript
class Child extends Person{
  constructor(){
    super('', 5);
  }
}
const child: Child = new Child();
child.hello();
~~~

##### getter, setter

~~~typescript
class Person{
  constructor(private _name: string, priavate _age: number){
  }
  
  hello(): void{
    console.log(this._name);
  }
  
  get name(): string{
    return this._name;
  }
  
  set name(newName: string){
    this._name = newName;
  }
}
~~~

---

### Generic

~~~typescript
function hello<T>(message: T): T{
  return message;
}
hello('jione');
hello(35);
~~~

##### 배열 생성

~~~ typescript
const a: string[] = [];
const b: Array<striong> = [];

function hello<T>(messages: T[]): T{
  return messages[0];
}
~~~

