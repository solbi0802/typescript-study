## 타입스크립트 스터디

#### [타입스크립트 프로그래밍 책](http://www.yes24.com/Product/Goods/90265564)을 읽고 공부한 내용을 정리했습니다.

- chapter 3. 타입의 모든 것 <br/>
타입스크립트가 타입을 추론하게 하거나, 명시적으로 선언해서 사용하는 방법이 있다.

![image](https://user-images.githubusercontent.com/26318691/169843371-bbed1016-1c4c-4845-b3c4-e6b4da5ef829.png)

<h3> 타입 </h3>

- any <br/>
 타입검사기가 동작하지 않기 때문에 가급적 사용하지 않는게 좋다.

  예시)
  ```
  let a: any = 666
  let b: ant = ['danger']
  let c = a + b 
  ```

- unknown <br/>
  타입을 미리 알 수 없을 때 사용. <br/>
  unknown의 타입을 검사해 정제하기 전까지는 unknown타입의 값을 사용할 수 없게 강제함 <br/>
  비교연산(==, ===, |, &&, ?), !, typeof, instanceof 연산자 지원 <br/>
  
  예시) 
  ```
  let a: unknown = 30 
  let b = a === 123 // boolean
  let c = a + 10 // 에러 : 타입이 'unknown'
  if (typeof a === 'number') {
    let d = a + 10 // number
  }
  ```
- boolean <br/>
  예시)
  ```
  let a = true  // boolean
  var b = false // boolean
  const c = true // true
  let d: boolean = true // boolean
  let e: true = true // true 
  let f: true = false // 에러 : 'false' 타입을 'true'타입에 할당 x 
  ```
  타입 리터럴 : 오직 하나의값을 나타내는 타입
  
- number <br/>
  예시) 
  ```
  let a = 1234 // number
  var b = Infinity * 0.10 // number
  const c = 5678 // 5678
  let d = a < b // boolean
  let e: number = 100 // number
  let f: 26.218 = 26.218 // 26.218
  let g: 26.218 = 10 // 에러 : '10' 타입을 '26.218' 타입에 할당 x  
  ```
  주로 a와 같은 방식을 사용

- bigint <br/>
  예시)
  ```
  let a = 1234n //bigint
  const b = 5678n // 5678n
  var c = a + b  // bigint
  let d = a < 1235 // boolean
  let e = 88.5n // 에러 : bigint 리터럴은 반드시 정수여야 함
  let f: bigint = 100n // bigint
  let g: 100n = 100n // 100n
  let h: bigint = 100 // 에러 : '100' 타입은 'bigint' 타입에 할당 x 
  ```
  타입스크립트가 bigint의 타입을 추론하게 하는 게 best
  
- string <br/>
 boolean, number와 같이 네 가지 방법으로 선언 가능하며, 가급적이면 추론하도록 두는 것이 좋음.

- symbol <br/>
  객체와 맵에서 문자열 키를 대신하는 용도로 사용. <br/>
  예시)
  ```
  let a = Symbol('a') // symbol
  let b: symbol = Symbnol('b') // symbol
  var c = a === b // boolean
  let d = a + 'x' // 에러 : '+' 연산 symbol 타입에 적용 x
  ```
  unique symbol
  ```
  const e = Symbol('e') // typeof e
  const f: unique symbol = Symbol('f') // typeof f
  let g: unique symbol = Symbol('f') // 에러 : unique symbol타입은 const여야 함
  ```

- object <br/>
  객체 리터럴
  ```
  let a = {
   b : 'x'
  }  {b : string}
  a.b // string 
  
  let a2: {b2: number } = {
      b2: 12
  } // {b: number} 
  ```
  object 타입 
  ```
  let person = {age: 20} 
  ```

- 배열 <br/>
T[ ], Array<T> 두가지 문법 지원
   ```
   let a:number [] = [1, 2, 3] 
   let a: Array<number> = [1,2,3]
   ```

- 튜플 <br/>
 배열의 길이가 고정되고 각 요소의 타입이 지정되어 있는 배열 형식. <br/>
 선언할 때 타입 명시해야함.
 예시)
  ```
  let a: [string, string, number] = ['park', 'choi', 1993]
  let friends: [string, ...string[]] = ['Sara', 'Tali', 'Chole', 'Claire']
  ```
 
- null, undefined, void, never <br/>
  null: 값이 없음
  undefined: 아직 값을 변수에 할당하지 않음
  void: return문을 포함하지 않는 함수
  never: 절대 반환하지 않는 함수 

- 열거형(enum) <br/>
 해당 타입으로 사용할 수 있는 값을 열거
 예시) 
 ```
 enum Language {
   English = 0,
   Spanish = 1, 
   Russian = 2
 }
 let a = Language.English // Language
 ```
<h3> 추가내용 </h3>

- 타입별칭 <br/>
 ```
 type Age = number
 type Person = {
   name: string
   age: Age
 }
 ```
+) type vs interface
타입 별칭과 인터페이스의 가장 큰 차이점은 타입의 확장 가능 / 불가능 여부 <br/>
인터페이스는 확장이 가능한데 반해 타입 별칭은 확장이 불가능함. <br/>
type 보다는 interface로 선언해서 사용해야함. <br/>

 
 - chapter 6. 고급타입 <br/>

## 타입 간의 관계

### - 서브타입


![Untitled](https://user-images.githubusercontent.com/26318691/175024554-4f2e7a1d-21ea-457e-bd08-4ab90eaa2e0a.png)

두 개의 타입 A와 B가 있고 B가 A의 서브타입이면 A가 필요한 곳에는 어디든 B를 안전하게 사용할 수 있다.

예시) A /  B

- 배열은 객체의 서브타입이다. → 객체를 사용해야하는 곳에 배열도 사용 O

- 튜플은 배열의 서브타입이다. → 배열을 사용해야 하는 곳에 튜플도 사용 O

- 모든 것은 any의 서브타입이다. → any를 사용해야 하는 곳에 객체도 사용 O

- never는 모든 것의 서브타입이다. → 어디에나 never를 사용 O

- Animal을 상속받는 Bird 클래스가 있다면 Bird는 Animal의 서브타입이다. → Animal을 사용해야 하는곳에 Bird도 사용O

### - 슈퍼타입
![Untitled 1](https://user-images.githubusercontent.com/26318691/175024593-5ae80cf5-1197-4688-a83d-29719fd0bfb5.png)

두 개의 타입 A와 B가 있고 B가 A의 슈퍼타입이면 B가 필요한 곳에는 어디든 A를 안전하게 사용할 수 있다.

예시) A /  B

-배열은 튜플의 슈퍼타입이다.  → 튜플을 사용해야하는 곳에 배열 사용 O

- 객체는 배열의 슈퍼타입이다.  → 객체를 사용해야하는 곳에 배열 사용 O

- any는 모든 것의 슈퍼타입이다. → 모든곳에 any 사용 O

- never는 누구의 슈퍼타입도 아니다. → never 사용 X

- Animal은 Bird의 슈퍼타입이다. → Bird를 사용해야하는 곳에 Animal 사용 O

### -가변성

제네릭 타입 등 복합 타입에서 다른 타입의 서브타입인 지 아닌지 쉽게 판단하기 어려움

서브타입( A<: B ) / 슈퍼타입 ( A >: B)

- 형태와 배열 가변성

```tsx
// 기존 사용자
type ExistingUser = {
  id: number
  name: string
}
// 새 사용자
type NewUser = {
  name: string
}

사용자 삭제 코드 추가 
function deleteUser(user: { id?: number, name: string }) {
  delete user.id
}

let existingUser: ExistingUser = {
  id: 123456,
  name: 'Ima User'
}

deleteUser(existingUser) 
```

 ☠️ deleteUser 함수가 실행되고 id가 삭제 되었는데도 existingUser.id를 호출하면 number 타입을 예상함

```tsx
// 기존 사용자
type LegacyUser = {
  id?: number | string
  name: string
}
let legacyUser: LegacyUser = {
  id: '793331',
  name: 'Solbi Shin'
}
사용자 삭제 코드 추가 
function deleteUser(user: { id?: number, name: string }) {
  delete user.id
}
 
사용자 삭제 코드 추가 
deleteUser(legacyUser) // 에러 발생!  
```

 ☠️ 슈퍼타입 id는 string | number | undefined 
      deleteUser는 id number | undefined만 처리 가능

- **불변** : 정확한 T를 원함
- **공변** : 서브타입을 원함
- 반변 : 슈퍼타입을 원함
- 양변 : 서브타입 또는 슈퍼타입을 원함

👉 모든 복합 타입의 멤버(객체, 클래스, 배열, 함수, 반환 타입)는 **공변**이며 함수 매개변수 타입만 **반변**

- 함수 가변성

```tsx
class Animal { }
class Bird extends Animal {
  chirp() { }
}
class Crow extends Bird {
  caw() { }
}

// Crow <: Bird <: Animal 성립

function chirp(bird: Bird): Bird {
	bird.chrip()
	return bird
}

chirp(new Animal) // 에러: Animal 타입을 매개변수 'Bird'타입에 할당 x 
chirp(new Bird)
chirp(new Crow) 

function clone(f: (b: Bird) => Bird): void {
  // ...
}

function birdToBird(b: Bird): Bird {
 // ...
}

clone(birdToBird)

function birdToCrow(d: Bird): Crow {
 // ...
}

clone(birdToCrow)

function birdToAnimal(d: Bird): Animal {
 // ...
}

clone(birdToAnimal) // 에러: Animal 타입은 Bird 타입에 할당 x 
```

### - 할당성

A라는 타입을 다른 B라는 타입이 필요한 곳에 사용할 수 있는 지를 결정하는 규칙

규칙1  A <: B (서브타입)

규칙2 A는 any

### - 타입 넓히기

```tsx
function f() {
	let a = null //any
	a = 'b' //any

	let b = null //any
	b = 1 //any

	return a || b // string | number
}

f() // string | number
```

- const 타입 
[타입 어서션 활용](https://www.notion.so/443476f6fdf647c484a252874c05f722)

```tsx
let a = {x: 3} // {x: number}
let b: {x: 3} // {x: 3}
let c = {x: 3} as const // {readonly x: 3} 좁은 타입으로 추론
```

- 초과 프로퍼티 확인

신선한(fresh) 객체 리터럴 타입(타입 스크립트가 추론한 타입) T를 다른 타입 U에 할당하려할 때 
T가 U에 존재하지 않는 프로퍼티를 갖고 있으면 타입스크립트에서 에러로 판단

```tsx
type Options = {
  baseURL: string
  cacheSize?: number
  tier?: 'prod' | 'dev'
}

class API {
  constructor(private options: Options) { }
}

new API({
 baseURL: 'https://api.mysite.com',
 tier: 'prod'
})

new API({
 baseURL: 'https://api.mysite.com',
 **badTier**: 'prod'
})

new API({
 baseURL: 'https://api.mysite.com',
 badTier: 'prod'
} **as Options**)
 
let **badOptions** = {
 baseURL: 'https://api.mysite.com',
 badTier: 'prod'
}

new API(**badOptions**)

let options: **Options** = {
 baseURL: 'https://api.mysite.com',
 badTier: 'prod'
}

new API(options)
```

### - 정제

타입 검사할 때 타입 질의(typeof, instanceof, in), 제어 흐름 문장(if, ?, ||, switch)까지 고려하여 정제

- 차별된 유니온 타입

```tsx
type UserTextEvent = {
  value: string,
  target: HTMLInputElement
}

type UserMouseEvent = {
 value: [number, number],
 target: HTMLElement
}

type UserEvent = UserTextEvent | UserMouseEvent

// Error
let v: UserEvent = {
	value: 'a',
	target: '' as unknown as HTMLElement
}

// UserEvent type?
type UserEvent = {
	value: string | [number, number],
	target: HTMLInputElement | HTMLElement,
}

function handle(event: UserEvent) {
  if (typeof event.value === 'string') {
      event.value    // string
      event.target  // HTMLInputElement | HTMLElement
      // ...
      return 
  }
  event.value. // [number, number]
  event.target // HTMLInputElement | HTMLElement
}
```

```tsx
type UserTextEvent = {
  type: 'TextEvent', value: string,
  target: HTMLInputElement
}

type UserMouseEvent = {
 type: 'MouseEvent', value: [number, number],
 target: HTMLElement
}

type UserEvent = UserTextEvent | UserMouseEvent

function handle(event: UserEvent) {
  if (event.type === 'TextEvent') {
      event.value    // string
      event.target  // HTMLInputElement
      // ...
      return 
  }
  event.value. // [number, number]
  event.target // HTMLInputElement
}
```

## - 종합성

필요한 모든 상황을 제대로 처리했는지 타입 검사기가 체크하는 기능

```tsx
type Weekday = 'Mon' | 'Tue' | 'Wed' | 'Thu' | 'Fri'
type Day = Weekday | 'Sat' | 'Sun'

function getNextDay(w: Weekday): Day {
   switch (w) {
     case 'Mon': return 'Tue'
   }
}
// 에러 : 함수에 마무리 반환문이 없고 반환타입에 undefined 포함 x

```

## -  고급 객체 타입

- 객체타입의 타입 연산자
    - 키인 연산자
    
     
    
    ```jsx
    type APIResponse = {
      user: {
         userId: string
         friendList: {
           count: number
           friends: {
             firstName: string
             lastName: string
           }[]
         }
       }
    } 
    
    **type FriendList = APIResponse['user']['friendList']**
    
    function renderFriendList(friendList: FriendList) {
      ...
    }
    ```
    
    - keyof 연산자
    
        
    
    ```jsx
    type ResponseKeys = keyof APIResponse // 'user'
    type UserKeys = keyof APIResponse['user'] // 'userId' | 'friendList'
    type FriendListKeys = keyof APIResponse['user']['friendList'] 
                                          // 'count' || 'friends'
    
    ```
    
- Record 타입

  

```jsx
type Weekday = 'Mon' | 'Tue' | 'Wed' | 'Thu' | 'Fri' 
type Day = Weekday | 'Sat' | 'Sun'

let nextDay: **Record<Weekday, Day**> = {
  Mon: 'Tue'
}
// 에러 : '{Mon: "Tue"}' 타입에는 R**ecord<Weekday, Day**> 타입 중 
// 빠진 값(Tue, Wed, Thu,Fri)이 있음
```

- 매핑된 타입

   한 객체 당 최대 한 개의 매핑된  타입을 가질 수 있음

 

```tsx
type Account = {
  id: number
  isEmployee: boolean
  notes: string[]
}

type OptionalAccount = {
  [K in keyof Account]?: Account[K]
}

type NullableAccount = {
  [K in keyof Account]: Account[K] | null
}

type ReadonlyAccount = {
  readonly [K in keyof Account]: Account[K]
}

type Account2 = {
  -readonly [K in keyof ReadonlyAccount]: Account[K]
}

type Account3 = {
  [K in keyof OptionalAccount]-?: Account[K]
}
```

- 내장 매핑된 타입
    - Record<Keys, Values>
    - Partial<Object>
    - Required<Object>
    - Readonly<Object>
    - Pick<Object, Keys>
- 컴패니언 객체 패턴
같은 이름을 공유하는 객체와 클래스를 쌍으로 연결

## - 고급 함수 타입들

- 튜플의 타입 추론 개선
- 사용자 정의 타입 안전 장치

## -조건부 타입

```jsx
type IsString<T> = T extends string
   ? true
   : false

type A = IsString<string> 
type B = IsString<number> 
```

 

- 분배적 조건부
- string extends T ? A : B   === string extends T ? A : B

       - (string | number) extends T ? A : B. ===

         (string extends T ? A : B) | (number extends T ? A : B)
       - (string | number | boolean) === (string extends T ? A : B) | (number extends T ? A : B) 
        | (booelan extneds T ? A :B) 

 

- infer 키워드
조건의 일부를 제네릭 타입으로 선언

```jsx
type ElementType2<T> = T extends (infer U)[] ? U : T
type B = ElementType2<number[]> // number
```

- 내장 조건부 타입들
    - Exclude<T, U>
    - Extract<T, U>
    - NonNullable<T>
    - ReturnType<F>
    - InstanceType<C>

## -탈출구

- 타입 어서션
    - 타입  B가 있고  A <: B <: C를 만족하려면 B는 실제로 A거나 C라고 어서션(assertion: 단언, 확언) 할 수 있다
    - 자신의 슈퍼타입이나 서브타입으로만 가능
    - <>,  as 두가지 문법 제공
    
- Nonnull 어서션
어떤 값이 null 이나 undefined가 아니라 T 임을 단언하는 문법
- 확실한 할당 어서션
타입스크린트가 변수를 사용할 때 값이 이미 할당되어 있는 지 검사

## - 이름 기반 타입 흉내내기

타입 브랜딩

```jsx
type CompanyID = string & { readonly brand: unique symbol }
type OrderID = string & { readonly brand: unique symbol }
type UserID = string & { readonly brand: unique symbol }
type ID = CompanyID | OrderID | UserID
```
