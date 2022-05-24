## 타입스크립트 스터디

#### [타입스크립트 프로그래밍 책](http://www.yes24.com/Product/Goods/90265564)을 읽고 공부한 내용을 정리했습니다.

- chapter 3. 타입의 모든 것 
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

