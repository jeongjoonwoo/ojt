ECMAScript
===
ES6
---
### let,const
* 기존의 var로 모든 변수를 선언하였지만 문제가 존재하였습니다.
1. 함수레벨의 스코프
    * 함수의 코드블록만 스코프를 인정합니다.
    * for문의 변수 선언문에서 선언한 변수를 외부에서는 참조할 수 없습니다.
2. var 키워드 생략 허용
    * 개발자가 의도하지 않은 변수를 양산할 가능성이 있습니다.
3. 변수 중복허용
    * 개발자가 의도하지 않은 변수값의 변경이 일어날 가능성이 있습니다.
4. 변수 호이스팅
    * 선언 이전에 참조가 될 수 있습니다.
#### let
1. 블록 레벨 스코프
    * 자바스크립트는 함수 레벨 스코프를 따릅니다.
    ```
    var a = 15
    console.log(a) //15
    {
        var a = 30
    }
    console.log(a) //30
    ```
    * var 위 코드와 같이 전역변수로 선언하였지만 코드블록 내에서 다시 할당하면 30으로 값이 할당되어져 의도치 않게 값을 변경할수도있습니다.
    ```
    let a = 15
    console.log(a) //15
    {
        let a = 30
        let b = 45
    }
    console.log(a) // 15
    console.log(b) // 참조할 값이 없습니다.
    ```
    * 이렇듯이 코드블록 내부에 값이 재할당되거나 할당이 되어져도 전역에는 영향을 주지 않습니다.
2. 변수 중복 선언 금지
    * var은 변수가 중복선언이 허용되지만 let은 이미 선언되어졌다는 문법에러가 발생하며 선언이 되어지지 않습니다.
    ```
    var a = 10
    var a = 15 //a는 15의 값을 가집니다

    let b = 10 //let은 10의값을 고정으로 가집니다.
    let b = 15 //문법에러 발생
    ```
3. 호이스팅
    * 호이스팅은 사용이 되어져도 뒤에 변수가 선언되어지면 끌어올려 사용이 되어 오류가 발생하지 않습니다.
    ```
    console.log(a) //undefined
    var a = 10
    console.log(b) //문법에러 발생
    let b = 10
    ```
4. 클로저
    * 블록 레벨 스코프를 지원하는 let은 var보다 직관적입니다.
    * 블록에서 사용되어질 경우 var은 전역으로 영향을 주어서 배열등 값을 순차적으로 넣어줄 경우 이를 신경쓰고 넣어주어야합니다. let은 블록에 사용이 되어져도 블록내부에서만 유효하기 때문에 다른 블록에 영향을 주지 않습니다.
5. 전역객체에서의 let
    * let은 전역으로 선언된것처럼 보이나 사실상 전역객체의 프로퍼티가 아닙니다.
#### const
1. 선언과 초기화
* let과 const는 유사하지만 const는 값의 재할당이 불가능합니다. C언어의 #define이라고 생각하시면 됩니다.
* const는 이러한 이유로 반드시 선언과 할당이 동시에 이루어져야 합니다.
2. 상수
* 상수는 가동성과 유지보수의 편의를 위해 사용합니다.
* 고정된 값을 넣어 변경이 불가능하게 해주기 위해서 필요합니다.
3. const와 객체
* const로 객체를 선언하면 객체의 프로퍼티는 보호받지 못합니다.
* 허나 객체명은 변경이 되지 않습니다.
---
### 템플릿 리터럴
* 벡틱(`)을 사용합니다.
* 문자열 인터폴레이션 : 간단하게 문자열 내부에 다른 값을 넣어줄 수 있습니다.
* 벡틴 사이에 ${}을 활용하여 내부에 간단하게 값을 넣어줄 수 있습니다.
```
var a = 10
var b = 15
console.log(`a+b = ${a+b}`)
```
---
### 화살표 함수
* =>를 이용하여 간략한 방법으로 함수를 선언할 수 있습니다.
```
const pow = x => x *2
console.log(pow(10)) //100
```
* 콜백 함수로도 사용할 수 있습니다.
```
var arr = [1,2,3]
var pow = arr.map(function(x)=>{
    return x**2
})
console.log(pow) //1,4,9
```
#### this
* function 함수와 가장큰 차이점은 this입니다.
    * 화살표 함수에서의 this는 바인딩할 객체가 결정된것이 아니라 함수가 어떻게 호출 되었는지에 따라서 this에 바인딩할 객체가 동적으로 결정됩니다.
#### 화살표 함수를 사용해서는 안되는경우
* 메소드
    * 화살표 함수로 메소드를 정의하는 것을 피해야합니다.
    * 메소드를 호출할 경우 객체를 사용해야하는데 상위 컨텍스트인 window를 사용하여 메소드를 사용하는것은 바람직하지 않습니다.
* 프로토타입
    * 프로토타입도 이와 같은 문제가 발생합니다.
* 생성자 함수
    * 화살표 함수는 생성자 함수로 사용할 수 없습니다.
* addEventLister함수의 콜백함수
---
### 매개변수 기본값
* 함수를 호출할때 매개변수의 갯수만큼 인자를 전송하지 않아도 자바스크립트에서는 오류가 나지않고 undefined로 처리됩니다.
* 함수는 인수가 적절하게 전달 되었는지 함수 내부에서 확인이 필요합니다.
#### Rest파라미터
* 매개변수 앞에 ... 을 붙여서 정의한 매개변수를 의미합니다.
* REST파라미터는 전달되어진 인수를 배열로 만듭니다.
* REST는 파라미터가 할당된 인수를 제외한 나머지를 배열에 담아서 할당되어집니다.
#### arguments와 rest파라미터
* 가변 인자 함수는 파라미터를 통해 인수를 전달 받는것이 불가능합니다.
* arguments 객체는 유사배열 객체이므로 사용하려면 Function.prototype.call을 사용해야하는 번거로움이 있습니다.
#### Spread 문법
* 문법 대상을 이터러블이여야 합니다.
* ... 값 을 넣으면 내부의 개별 요소별로 나누어서 출력을 합니다.
* 함수를 인수로 사용하는경우
    * 배열을 분해하여 각각의 요소를 전달할경우 편하게 사용할 수 있습니다.
* 배열의 경우
    * concat : 배열에 새로운 요소의 일부로 만들고 싶은경우 사용합니다.
    ```
    var arr1=[1,2,3]
    console.log(arr1.concat([4,5,6])) //[1,2,3,4,5,6]

    const arr2 =[1,2,3]
    console.log([...arr],4,5,6) //[1,2,3,4,5,6]
    ```
    * push : 다른 배열의 요소를 삽입할때 사용합니다.
    ```
    var arr1=[1,2,3]
    var arr2=[4,5,6]
    Array.prototype.push.apply(arr1,arr2)
    console.log(arr1) //[1,2,3,4,5,6]

    const arr3=[1,2,3]
    const arr4=[4,5,6]

    arr3.push(...arr4)
    console.log(arr3) //[1,2,3,4,5,6]
    ```
    * splice : 기존에 존재하는 배열에 요소를 삽입할때 사용합니다.
    ```
    var arr1 = [1,2,3,6]
    var arr2 = [4,5]
    Array.prototype.splice.apply(arr1,[3,0].concat(arr2));
    console.log(arr1) //[1,2,3,4,5,6]
    
    const arr3 = [1,2,3,6]
    const arr4 = [4,5]
    arr3.splice(3,0,...arr4)
    console.log(arr3) //[1,2,3,4,5,6]
    ```
    * copy: 기존의 배열의 값을 복사할때 사용합니다. ES5에서는 slice를 사용했습니다.
    ```
    var arr1 = [1,2,3]
    var copy1 = arr.slice()
    console.log(copy1) //[1,2,3]

    cosnt arr2 = [1,2,3]
    const copy2 = [...arr]
    console.log(copy2) //[1,2,3]
    ```
---
### 프로퍼티 축약표현
* 프로퍼티 값으로 변수를 사용하는경우 프로퍼티 이름을 생략할 수 있습니다.
* 프로퍼티 키 동적생성
    * 프로퍼티 키를 동적으로 생성할 수 있습니다.
    * 객체[변수명] = 값을 활용하여 키값을 동적으로 생성할 수 있습니다.
    ```
    var obj = {
        name : 'kim',
        gender : 'male'
    }
    obj['age'] = 24
    console.log(obj.age) //24
    ```
* 메소드 축약표현
    * 객체 내부에 메소드를 선언하려면 기존에는 함수 선언식을 사용하여야 했지만 이제는 축약하여 사용할 수 있습니다.
    ```
    var obj = {
        name : 'kim',
        gender : 'male'
        sayHi(){
            console.log('hi' + this.name)
        }
    }
    obj.sayHi() //hi kim
    ```
* 프로퍼티에 의한 상속
    * 함수를 재생성하여 자식객체에 상속이 필수였지만. 이후에는 생략하고 객체에 프로퍼티 값으로 저장할 수 있게 되었습니다.
    ```
    var obj1 = {
        name : 'kim',
        sayHi(){
            console.log('hi' + this.name)
        }
    }

    var obj2 = {
        __proto__ : obj1,
        name : 'lee'
    }

    obj1.sayHi() //hi kim
    obj2.sayHi() //hi lee
    ```
---
### 디스트럭처링
* 구조화된 배열 또는 객체를 파괴하여 개별적인 변수에 할당하는것입니다.
* 배열 디스트럭처링
    * 배열의 요소를 각각 추출하여 리스트에 할당합니다.
    ```
    const arr = [1,2,3]
    const [one,two,three] = arr;
    console.log(one,two,three) //1,2,3
    ```
* 객체 디스트럭처링
    * 프로퍼티의 키를 사용해야 합니다.
    ```
    var obj = {
        name : 'kim'
        gender : 'male'
    }

    const {name,gender} = obj
    console.log(name , gender) //kim male
    ```
---
### 클래스
* 프로토타입 기반 객체지향 언어입니다.
* ES6 클래스는 class 키워드를 사용하여 정의합니다.
* 클래스 선언문도 변수 선언,함수 정의와 마찬가지로 호이스팅은 키워드를 사용한 모든 선언문에 적용됩니다.
#### 인스턴스 생성
* 마치 생성자 함수와 같이 new 연산자와 함께 클래스 이름을 호출하면 클래스의 인스턴스가 생성됩니다.
* Constructor
    * 인스턴스를 생성하고 클래스 필드를 초기화 하기 위한 특수한 메소드입니다.
    ```
    class cs{}

    const cs1 = new cs();
    console.log(cs1) // cs{}

    cs1.num = 1;
    console.log(cs1) // cs&nbsp;{num : 1}
    ```
### 클래스 필드
* 클래스 몸체에는 메소드만 선언할 수 있다. 클래스 필드를 선언하면 문법에러가 발생합니다.
* 클래스 필드의 선언과 초기화는 반드시 constructor내부에서 실시한다.
#### getter,setter
* getter 
    * 클래스 필드에 접근할때마다 클래스 필드의 값을 조작하는 행위가 필요할때 사용합니다.
    * get 키워드를 사용해 정의합니다.
* setter
    * 클래스 필드에 값을 할당할 때마다 클래스 필드의 값을 조작하는 행위가 필요할때 사용합니다.
    * set 키워드를 사용해 정의합니다.
#### 클래스 상속
* 클래스 상속은 코드 재사용에서 매우 유용합니다.
1. extends 키워드
* 부모 클래스를 상속받는 자식클래스를 정의 할때 사용합니다.
* 오버라이딩 : 상위클래스가 가지고 있는 메서드를 하위클래스가 재정의하여 사용하는 방식입니다.
* 오버로딩 : 매개변수 타입 또는 갯수가 다른, 같은이름의 메소드를 구현하고 매개변수에 의해 메소드를 구별하여 호출하는 방식입니다.
2. super 키워드
* 부모 클래스를 참조할때 부모클래스의 constructor를 호출할때 사용합니다.
* super 메소드는 자식클래스 constructor 내부에서 부모 클래스의 constructor를 호출합니다.
* super키워드는 부모 클래스에 대한 참조입니다.
---
### 모듈
* 재사용 가능한 코드조각을 말합니다.
* 모듈은 세부사항을 캡슐화 하고 공개가 필요한 API만을 외부에 노출합니다.
* 모듈은 파일단위로 불리되며, 명시적으로 모듈을 로드하여 재사용합니다.
* script태그에 타입을 module를 이용하여 사용합니다.
* 여러 이슈가 있습니다.
    * IE를 포함하여 구형 브라우저는 모듈을 지원하지 않습니다.
    * 브라우저가 모듈을 사용하더라도 트랜스파일링이나 번들링이 필요합니다.
    * 아직 지원하지 않는 기능이 있습니다.
#### 모듈스코프
* 모듈기능을 사용하지 않으면 분리된 자바스크립트 파일에 독자적인 스코프를 가지지 않고 전역을 고유합니다.
* 2가지 이상의 스크립트파일을 로드하면 전역변수를 공유합니다. 만약 a.js에서 선언되어진 전역변수를 b.js에서 재할당이 가능합니다.
* ES6 모듈은 파일 자체의 스코프를 제공합니다.
* 모듈 내에 선언한 변수는 모듈 외부에서 참조할 수 없습니다.
* export키워드
    * 내부에서 선언되어진 식별자를 외부에서 참조할 수 있게 해주기 위해서는 export를 사용해야합니다.
* import키워드
    * 모듈을 공개한 대상을 로드하려면 import를 사용해야합니다.
    * 모듈이 export한 식별자를 지정하지 않고 한번에 import하여 사용할 수 있습니다 이때 as를 사용하여 객체 프로퍼티로 할당됩니다.
    * 모듈에서 하나만 export할때는 default를 이용할 수 있습니다 이경우는 var,let,const는 사용할 수 없습니다
---
### Promise
* 비동기 callback중 발생항 에러의 예외처리가 힘들어진것을 해결해주었습니다.
* callback hell : 가독성을 나쁘게 하며 개발자가 실수를 유발할 수 있습니다.
* 프로미스 생성
    * 프로미스 생성자 함수를 통해 인스턴스화 합니다.
    * promise 생성자 함수는 비동기 작엄을 수행할 콜백함수를 인자로 전달 받습니다. 이때 resolve와 reject 함수를 인자로 전달 받습니다.
* 프로미스의 에러 처리
    * promise객체의 후속 처리 메소드를 사용하여 비동기 처리 결과에 대한 후속처리를 수행합니다.
    * promise객체의 후속처리는 catch를 활용하여 처리할 수 있습니다.
---
ES2016
---
### 제곱연산자
* 기존의 제곱 연산자는 Math객체의 pow를 이용했습니다.
* 제곱연산자를 ** 를 활용하여 사용할 수 있습니다.
```
var a = 2
Math.pow(a,3) //8
a**3 //8
```
### 배열.includes
*  배열에 해당 요소가 존재하는지 확인할 수 있습니다.
```
var arr=[1,2,3]
arr.includes(1) // true
```
---
ES2017
---
### 객체
* 객체에 키 값들이 아닌 객체값들을 확인할 수 있습니다.
```
var obj={
    a:'hello',
    b:'bye'
}
Object.values(obj) //['hello','bye']
```
* 객체 프로퍼티를 확인할 수 있습니다.
```
var obj={
    a:'hello',
    b:'bye'
}

Object.entries(obj) //["a", "hello"],["b", "bye"]
```
### 문자열
* 문자열 내부에 공백이나 글자를 넣을수 있습니다.
    * 문자열.padStar(길이,넣은문자)
    * 문자열.padEnd
    ```
    'hello'.padStar(10,'!') //"hello!!!!!"
    'hello'.padEnd(10,'!') /"!!!!!hello"
    ```
### async/await
* 비동기 코드를 작성할 떄 쉽고 명확하게 작성할 수 있습니다.
* async는 키워드 앞에 붙여줍니다.
* 비동기로 처리되는 부분 앞에 await를 붙여줍니다.
* await,async function도 promise를 반환합니다.


     



