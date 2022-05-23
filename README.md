## 타입스크립트 스터디

#### [타입스크립트 프로그래밍 책](http://www.yes24.com/Product/Goods/90265564)을 읽고 공부한 내용을 정리했습니다.

- chapter 3. 타입의 모든 것 
타입스크립트가 타입을 추론하게 하거나, 명시적으로 선언해서 사용하는 방법이 있다.

![image](https://user-images.githubusercontent.com/26318691/169843371-bbed1016-1c4c-4845-b3c4-e6b4da5ef829.png)

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
  
- object <br/>
- 타입별칭 <br/>
- 유니온 <br/>
- 인터섹션 <br/>
- 배열 <br/>
- 튜플 <br/>
- null, undefined, void, never <br/>
- 열거형(enum) <br/>
