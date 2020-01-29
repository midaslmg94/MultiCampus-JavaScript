#### 200129 수요일 

- 기본 매개변수

  - 매개변수가 들어가야 할 곳에 들어가지 않으면 다음과 같은 오류가 발생한다.

  ```javascript
  <script>
          function add(a,b,c){
              return a+b+c;
          }
          console.log(add(1));
          console.log(add(1,2));
          console.log(add(1,2,3));
  
      </script>
  
  #출력결과
  NaN
  NaN
  6
  ```

  - 변수는 뒤쪽부터 기본값으로 세팅해준다

  ```javascript
   <script>
          function add(a,b=0,c=0){
              return a+b+c;
          }
          console.log(add(1));
          console.log(add(1,2));
          console.log(add(1,2,3));
  
  </script>
  #출력결과
  1
  3
  6
  ```

  - 익명함수로 사용

    ```javascript
    <script>
            let sum = function add(a,b=0,c=0){
                return a+b+c;
            }        
            console.log(sum(1));
            console.log(sum(1,2));
            console.log(sum(1,2,3));
    
    </script>
    ```

  - `function`도 쓰기 귀찮다면 화살표 함수를 사용 **요새는 이것이 자주 쓰인다.**

    ```javascript
    <script>
            let sum = (a,b=0,c=0)=>{
                return a+b+c;
            };        
            console.log(sum(1));
            console.log(sum(1,2));
            console.log(sum(1,2,3));
    
    </script>
    ```



- 전개 연산자 : 마침표 3개(...)를 찍어서 표기하는 연산자

  - 배열 형태의 데이터를 받음

  ```javascript
  
      <script>
          function test1() {
              console.log(arguments[0]);
              console.log(arguments[1]);
              console.log(arguments[2]);
          }
          // 전개 연산자 
          function test2(...values) {
              console.log(values[0]);
              console.log(values[1]);
              console.log(values[2]);
          }
  
          test1(1, 2, 3);
          test2(1, 2, 3);
      </script>
  
  # test1과 test2는 같은 결과 출력
  ```

  - 배열 형태의 데이터를 넘겨줌

  ```javascript
    function test3(a,b, ...values){// 반드시 입력해야하는 것은 a,b로 처리.
              console.log('a',a);
              console.log('b',b);
              values.forEach(i=>console.log('values',i));
          }
          let arr = [1,2,3,4,5];// 데이터가 배열 형태일때도 사용 가능
          test3(...arr); // 풀어서 전달해줘야 함
  # 출력
  a 1
  b 2
  values 3
  values 4
  values 5
  ```



------

#### 객체

- 배열과 객체의 차이 

  - 배열 : **인덱스**를 사용하여 원소에 접근

    ```javascript
    // 배열
    let colors = ['빨강', '파랑', '노랑'];
        console.log(colors);
        console.log(colors[0]);
        console.log(colors[1]);
        console.log(colors[2]);
    
    # 출력결과
    (3) ["빨강", "파랑", "노랑"]
    	0: "빨강"
    	1: "파랑"
    	2: "노랑"
    	length: 3
    	__proto__: Array(0)
    빨강
    파랑
    노랑
    
    ```

  - 객체 : **키**를 사용하여 원소에 접근

    ```javascript
    // 객체
    let person = {
        name: '홍길동',
        age: 23,
        isMarried: false,
        sex: 'male',
         // 속성 이름에 공백이 들가는 경우는 따옴표를 꼭 써야 한다.
        'favorite colors' : ['red','blue','black'],
        hello: function(){return ("안녕, 나는 홍길동이야");}, // person 객체의 메소드
        getFullName:function(){
           return this.lastName+this.firstName;
        }
    };
        console.log(person);
        console.log(person.name);
        console.log(person['age']);
        console.log(person.isMarried);
        console.log(person.sex);
        console.log(person['favorite colors']);
        console.log(person['favorite colors'][0]);
        console.log(person['favorite colors'][1]);
    	console.log(person.hello());
        console.log(person.getFullName());
    # 출력결과
    {name: "홍길동", age: 23, isMarried: false, sex: "male", favorite colors: Array(3)}
    홍길동
    23
    false
    male
    (3) ["red", "blue", "black"]
    red
    blue
    안녕, 나는 홍길동이야
    홍길동
    ```

    - 객체에 정의되어 있는 함수를 메소드라고 한다.
    - `this` : 객체가 가지고 있는 속성

  - `for-in`구문

    ```javascript
    <script>
            //  객체 요소에 접근하기 위해서는 속성의 이름을 이용
            let person = {
                firstName : "길동", 
                lastName : "홍", 
                id : 1234, 
                getFullName : function() {
                    return this.lastName + this.firstName;
                }
            };
            
            //  for in 구문을 이용해서 객체 내부를 출력
            for (let key in person) {
                console.log(`${key} : ${person[key]}`);
            }
    </script>
    
    ```

- `in` 키워드 : 해당 객체에 그 원소가 있는지 없는지 true, false 반환

- `with` 키워드 : 객체의 이름을 쓰지 않고 쓰기?

  ```javascript
  <script>
  // in 키워드
  let scores ={
  	C:90,
      Java:80,
      Python:100
  };
  console.log(`score 객체에 Java 항목이 포함되어 있나요? ${'Java' in scores}`);
  console.log(`score 객체에 JavaScript 항목이 포함되어 있나요? ${'JavaScript' in scores}
  `);
  </script>
  # 출력결과
  score 객체에 Java 항목이 포함되어 있나요? true        
  score 객체에 JavaScript 항목이 포함되어 있나요? false
  
  
  // with 키워드
  with(scores) {
  	console.log(`C:${C}`);
      console.log(`Java:${Java}`);
      console.log(`Python:${Python}`);
  }
  
  // 객체에 속성을 집어 넣기 
  console.log("#1", 'JavaScript' in scores); // return false
  scores.JavaScript = 100;
  console.log("#2", 'JavaScript' in scores); // return true
  
  // 객체의 속성 변경
  console.log("#3", scores.JavaScript); // print 100
  scores.JavaScript = 50;
  console.log("#4", scores.JavaScript); // print 50
  ```

- `toString`메소드 : 객체가 가지고 있는 모든 속성과 속성값을 반환하는 메소드

  - 빈 객체를 생성하고 객체의 속성을 집어넣음

    ```javascript
     <script>
        let person = {};
        person.name='홍길동';
        person.age=25;
        person.isMarried=false;
    // toString : 객체가 가지고 있는 모든 속성과 속성값을 반환하는 메소드 
        person.toString = function(){
            let output='';
            for(let key in person){
                if(key!='toString'){
                    output+=`${key}:${person[key]}\n`;
                }
            }
            return output;
        }
        console.log(person.toString());
    ```

  - 객체의 속성을 삭제하는 연산자 : `delete`

    ```javascript
        // delete : 객체의 속성을 삭제
        delete person.name;
        console.log(person.toString());
        
        delete(person.isMarried);
        console.log(person.toString());
        </script>
    
    ```

- 함수를 추가해서 재사용성을 높이자

  - 학생 성적 객체에 학생별 총점, 평균을 구하는 메소드를 추가

    ```javascript
    <script>
    let students = [];
    students.push({ name: 'aaa', korean: 46, math: 65, english: 25, science: 64 });
    .
    .
    .
    students.push({ name: 'jjj', korean: 24, math: 42, english: 71, science: 88 });
    //	학생별 총점, 평균점을 구하는 메소드를 추가
    students.forEach(student=>{// 배열의 요소 하나를 가져옴
    	// 총점을 구하는 메소드 추가
        student.getSum=function(){
            return this.korean + this.english + this.math+this.science;
        };
    
        // 평균을 구하는 메소드 추가
        student.getAvg=function(){
            return this.getSum()/4;
        };
    });
    
    	//	학생별 총점, 평균점을 출력
    students.forEach(student=>{
    	console.log(`이름:${student.name}, 총점:${student.getSum()}, 평균:${student.getSum()}`);
        
         // with를 사용해서 출력
        with(student){
        	console.log(`이름:${name},총점:${student.getSum()},평균:${student.getAvg()}`);
        }
    });
    ```

  - 함수로 입력

    ```javascript
    <script>
    function makeStudent(name, korean, math, english, science) {
    	let result = {
    		name: name,
            korean: korean,
            math: math,
            english: english,
            science: science,
            getSum: function () {
            	return this.korean + this.math + this.english + this.science;
            },
            getAvg: function () {
            	return this.getSum() / 4;
            }
        };
        return result;
    };
    	let students = [];
            students.push(makeStudent('aaa', 46, 65, 25, 64));
            students.push(makeStudent('bbb', 56, 63, 85, 62));
            students.push(makeStudent('ccc', 56, 63, 22, 43));
            students.push(makeStudent('ddd', 12, 25, 26, 23));
            students.push(makeStudent('eee', 18, 85, 25, 25));
            students.push(makeStudent('fff', 32, 22, 79, 25));
            students.push(makeStudent('ggg', 52, 26, 42, 42));
            students.push(makeStudent('hhh', 22, 25, 41, 56));
            students.push(makeStudent('iii', 87, 79, 25, 86));
            students.push(makeStudent('jjj', 24, 42, 71, 88));
    
    	students.forEach(student => {
        	with(student) {
            	console.log(`이름:${name}, 총점:${getSum()}, 평균:${getAvg()}\n`);
    		}
        })
    </script>
    ```

  

- 옵션 객체





- 참조 복사와 값 복사

  - ```javascript
     <script>
            // 기본 자료형의 값 복사 -- 깊은 복사
            let oldValue=10;
            let newValue=oldValue;
            console.log(oldValue, newValue); // 10, 10
            oldValue=100;
            console.log(oldValue, newValue); // 100, 10
            
            // 참조 자료형의 참조 복사 -- 얕은 복사
            let oldArray=[10,20];
            let newArray=oldArray;
            console.log(oldArray, newArray); // [10,20], [10,20]
            oldArray[0]=100;
            newArray[1]=999;
            console.log(oldArray, newArray); // [100,999], [100,999]
    
            // 객체 자료형의 복사 -- 얕은 복사
            let oldObject = {name:'aa', age:53};
            let newObject = oldObject;
            console.log(oldObject, newObject);// {name:"aa", age:53} {name:"aa", age:53}
    
            oldObject.name = 'bb';
            newObject.age = 30;
            console.log(oldObject, newObject); // {name:"bb", age:30} {name:"bb", age:30}
        
    
            // 어렵당..
            function clone(obj){
                let output={};
                for(let key in obj){
                    output[key]=obj[key];
                }
                return output;
            }
            let oldObject2 = {name:'xyz', age:123};
            let newObject2 = clone(oldObject2);
            console.log(oldObject2, newObject2);// {name:"xyz", age:123} {name:"xyz", age:123}
    
            // 자기가 바꾼 값만 바뀜. 서로간에 영향을 미치지 않음
            oldObject2.name='zzz';
            newObject2.age=999;
            console.log(oldObject2, newObject2);// {name:"zzz", age:123} {name:"xyz", age:999}
            
        </script>
    ```



- 전개 연산자를 사용한 테크닉

  - 배열의 복사(깊은 복사)

  ```javascript
  <script>
          // 전개 연산자를 사용해서 배열을 넘겨주기 -- 깊은 복사가 된다
          // 배열의 값을 복사할 때 for loop을 사용하지 않아도 된다.
          let oldArray=[1,2,3,4];
          let newArray=[...oldArray];
          console.log(oldArray, newArray); // [1,2,3,4] [1,2,3,4]
  
          oldArray[0]=100;
          newArray[1]=200;
          console.log(oldArray, newArray); // [100,2,3,4] [1,200,3,4]
  </script>
  ```

  - 배열의 합병

  ```javascript
  <script>
          // 전개 연산자를 사용해서 배열 합치기
      let arrayA=[1,2,3];
      let arrayB=['a','b','c'];
  	let newArray2 = [...arrayA, ...arrayB];
  	console.log(newArray2); // [1,2,3,'a','b','c']
  </script>
  ```

  - 객체의 복사(깊은 복사)

  ```javascript
  <script>
  // 전개 연산자를 사용한 객체의 깊은 복사
      let objA = {name:'aaa', age:10};
     	let objB = {...objA};
  	console.log(objA, objB);  // {name: "aaa", age: 10} {name: "aaa", age: 10}
      objA.name='bbb';
  	objB.age=100;
  	console.log(objA, objB);  // {name: "bbb", age: 10} {name: "aaa", age: 100}
  </script>
  ```

  