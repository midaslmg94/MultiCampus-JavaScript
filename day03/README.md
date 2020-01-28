#### 200128 화요일 

- 참고자료 : [MDN web docs](https://developer.mozilla.org/ko/docs/Web/JavaScript)

- window.onload = function(){}  : function() 안에 있는 코드는 

  - div 태그가 밑에 있기 때문에 사용

    ```javascript
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <script>
            window.onload = function () {
                let disp = document.getElementById("display");
                for (let num = 1; num <= 9; num++) {
                    for (let dan = 2; dan <= 9; dan++) {
                        disp.innerText += `${dan} X ${num} =${dan*num} \t`;
                    }
                    disp.innerText += "\n";
                }
            }
            
        </script>
    </head>
    
    <body>
        안녕
        안녕
        <pre id="display"></pre>
    </body>
    ```

    - document.getElementById("display")를 변수 disp에 넣어서 사용할 수 있다.

- \t 문자는 브라우저에 따라 제대로 인식이 안되는 경우가 있기 때문에 div 태그 말고 pre 태그로 사용한다.\





- innerHTML

- ```javascript
  <script>      
  	window.onload = function () {
              let output = '';
              for (let i = 1; i <= 9; i++) {
                  output='';
                  for (let j = 1; j <= i; j++) {
                      output+=j;
                  }
                  console.log(output);
                  document.getElementById("display").innerHTML += output+'<br>'; 
              } // html에서 줄바꿈을 위해서는 br 태그를 쓴다
          }
          
  </script>
  ```



- for in 과 for of

  - for in : 배열의 인덱스를 반환
  - for of : 배열의 값을 반환

  ```javascript
  <script>
          window.onload = function(){
              const values = [100, '백', 200, '이백', 300, '삼백'];
              let sum = 0;
              for(let i in values){
                  //let v = Number(value[i]); 
                  if(!isNaN(values[i])){ 
                      sum += values[i];
                  }
              }
              console.log(`1. 배열에 포함된 숫자의 합은 ${sum}`);
              document.getElementById("result").innerText += `1. 배열에 포함된 숫자의 합은 ${sum}\n\n`;
      
              // for of 구문은 배열의 값을 반환
              sum=0;
              for(let i of values){
                  if(!isNaN(i)){
                      sum+=i;
                  }
              }
              console.log(`2. 배열에 포함된 숫자의 합은 ${sum}`);
              document.getElementById("result").innerText += `2. 배열에 포함된 숫자의 합은 ${sum}`;
          }
      
      </script>
  
  
  
  
  </head>
  <body>
      <div id="result"></div>
  </body>
  ```





------

#### 함수

- 함수 정의 방식 ​​

  - 함수 선언문 : 일반적으로 많이 쓰였던 방식(고전적)

    - 함수 리터럴과 동일함 ==> function add(int x, iny y){ return x+y;}
  
    - 함수 이름을 반드시 정의해야 한다.
  
  - 함수 선언 : function add(int x, int y){ return x+y} 
  
  - 함수 호출 : add(3, 4);
  
    
  
  - **함수 표현식** : 자바스크립트에서는 이 방식이 많이 쓰인다.
  
    - 자바스크립트에서 함수는 하나의 값으로 취급 ==> 문자열, 숫자처럼 변수에 할당 가능
  
      ```javascript
      let addFunction = function(x, y){return x+y;};
    addFunction(3,4);
      let sum = addFunction;
    addFunction(4,5);
      console.log(sum);
      ```
  
    - <span style="color:red">함수의 이름이 있는 경우(기명 함수) : 함수 표현식에 사용된 함수 이름은 외부 코드에서 접근 불가</span>
  
      ```javascript
      let sum = function add (x,y){return x+y;};
      console.log(sum(3,4));
    7
      console.log(add(3,4));
    Uncaught ReferenceError: add is not defined
          at <anonymous>:1:9
      ```
    ```
    
    - 함수의 이름이 없는 경우(익명 함수) 
    
    ​```javascript
      // 선언
    let 함수이름변수 = function(매개변수){ 함수본문 };
      
    // 호출
      함수이름변수(매개변수);
      
      
       <script>
              // 1부터 사용자가 입력한 숫자 만큼의 합을 반환하는 함수
              function sigma1(n) {
                  let sum = 0;
                  for (let i = 1; i <= n; i++) {
                      sum += i;
                  }
                  return sum;
              }
          
              // 함수표현식
              let sigma2 = function(n) {
                  let sum = 0;
                  for (let i = 1; i <= n; i++) {
                      sum += i;
                  }
                  return sum;
              };
      
      
              // 화살표 함수 : 리액트에서 많이 쓰임
              let sigma3(n) => {
                  let sum = 0;
                  for (let i = 1; i <= n; i++) {
                      sum += i;
                  }
                  return sum;
              };
              
              let num = prompt("숫자를 입력하세요");
              console.log(`1부터~${num}까지의합은 ${sigma1(num)}입니다.`);
      
      </script>
    ```
  
      
  
  - Function() 생성자 함수를 이용한 함수 생성
  
    ```javascript
    let add = new Function('x', 'y', 'return x+y');
    add(3,4);
    ```
  
    - 자바 스크립트 내부에서는 전부 이러한 방식으로 바뀌게 된다
    - 선언문 형식으로 정의된 함수와 표현문 형식으로 정의된 익명 함수가 공존하는 경우 선언문 형식이 먼저 생성된 후 익명 함수가 마지막에 생성
  



------

#### Array()

- 매개변수

  - 다양한 형식의 매개변수를 전달할 수 있다.

  ```javascript
  <script>  
  let arr1 = new Array();
          let arr2 = new Array(10);
          let arr3 = new Array(1,2,3,4); 
  
          console.log(arr1); // empty array -> size:0
          console.log(arr2); // empty array -> size:10
          console.log(arr3); // [1,2,3,4]
  </script>
  ```

- 가변인자 함수

  - 모든 함수는 `arguments`를 가지고 있다.

  - 파라미터의 개수가 정해지지 않은 함수

  - `for(i of arguments)`로 쓴다 

    ```javascript
        <script>
            // 매개변수로 전달된 숫자값의 합을 구하는 함수를 정의
            let sum = 0;
            function sumAll(){
                console.log(typeof arguments);
                console.log(arguments); 
                for(i of arguments){            
                    if(!isNaN(Number(i))){
                        console.log(i);
                        sum+=i;
                    }
                }
                return sum;
            }
            console.log(sumAll(1,"하나",2,"둘",3,"셋"));
            //console.log(sum);       
    
        </script>
    // 출력결과 : 배열처럼 입력이 들어감
    object
    Arguments(6)
    ▶	0: 1
    ▶	1: "하나"
    ▶	2: 2
    ▶	3: "둘"
    ▶	4: 3
    ▶	5: "셋"
    ▶	length: 6
    1
    2
    3
    6
    ```

  - 함수 예시([참고문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/find))

    ```javascript
        <script>
            // 파라미터로 전달된 숫자 중 첫번째 3의 배수를 반환하는 함수를 작성
            function f1() {
                for (i of arguments) {
                    if (i%3===0) {
                        console.log(i);
                        return;
                    }
                }
            }
            console.log(f1(3, 7, 11));
            console.log(f1(1, 7, 11, 15, 20, 22, 12));
            console.log(f1(1, 7, 12, 15));
    
            function f2(){
                return Array.from(arguments).find(i=>i%3===0);
            }
            console.log(f2(3, 7, 11));
            console.log(f2(1, 7, 11, 15, 20, 22, 12));
            console.log(f2(1, 7, 12, 15));
    
            // [...array_name] : 기존 배열을 새로운 이름의 배열로 만든다
            function f3(){
                return [...arguments].find(i=>i%3===0);
            }
            console.log(f3(3, 7, 11));
            console.log(f3(1, 7, 11, 15, 20, 22, 12));
            console.log(f3(1, 7, 12, 15));
        </script>
    ```

  

- 내부 함수

  - 함수 내부에서 함수를 정의하는 함수

  - 함수의 범위(scope)를 제한하기 위한 함수

  - `square()`함수가 2개 정의되어 있기때문에 `pytha`에서 원하는 `square`함수를 제대로 호출 불가

    ```javascript
       <script>
            function pytha(width, height) {
                return Math.sqrt(square(width) * square(height));
            }
    
            function square(x) {
                return x * x;
            }
            console.log(pytha(3, 4));
    
            function square(width, height, hypotenuse) {
                if (width * width + height * height === hypotenuse * hypotenuse)
                    return true;
                else
                    return false;
    
            }
        </script>
    ```

    

  - 해결 : `square()`를 `pytha()`내부에 넣어서 내부 함수로 사용한다.

    ```javascript
        <script>
            function pytha(width, height) {
                function square(x) {
                    return x * x;
                }
                return Math.sqrt(square(width) * square(height));
            }
    
            console.log(pytha(3, 4));
    
            function square(width, height, hypotenuse) {
                if (width * width + height * height === hypotenuse * hypotenuse)
                    return true;
                else
                    return false;
    
            }
        </script>
    ```

  
  
  
- 자기 호출 함수 : 생성하자마자 1번 호출

  - ```javascript
    <script>
            // 자기 호출 함수 : 생성하자마자 한번 호출되는 함수
            let f = function(){
                console.log("#1");
            };
            f();
    
            // 자기 호출 함수
            (function(){
                console.log("#2");
            })();
    
    </script>
    ```

  

- 콜백 함수

  - 동기 처리 : 앞 단계의 일이 끝날때 까지 기다렸다가 다음 단계의 일을 처리

  - 비동기 처리 :  앞 단계의 일이 끝나지 않았더라도 다음 단계의 일을 처리

    - 이벤트를 처리하는데 많이 사용한다.

    ```javascript
        <script>
            // 콜백 함수
            function callTenTimes(callback){ 
                for(let i=0; i<10;i++){
                    callback(); 
                }
            }
            let callback = function(){
                console.log("함수호출");
            }
            callTenTimes(callback);
        </script>
    ```



- 함수를 리턴하는 함수

  ```javascript
      <script>
          // 함수를 반환하는 함수
          function returnFunction(){
              return function(){
                  console.log("안녕");
              };
          }
          returnFunction()(); 
          let f = returnFunction();
          f();
      </script>
  
  // 출력결과
  안녕
  안녕
  ```

  

- 클로저

  - 함수에서 함수를 반환. 함수 내부에 사용된 변수의 소멸을 지연시킨다

    ```javascript
        <script>
            // 클로저
            function f(name){
                let output=`hello ${name}`;
                console.log("f()안 ",output);
                return function(){console.log(output);};
            }
            let f1 = f('홍길동');
            f1();
            //console.log("f()밖",output); 실행 안된다 
    			//Error:Uncaught ReferenceError: output is not defined 
    
            let f2 = f('리차드');
            f2();
        </script>
    
    // 출력결과
    f()안  hello 홍길동
    hello 홍길동
    f()안  hello 리차드
    hello 리차드
    ```

    - `output`은 함수 f()가 return 될 때 소멸되지만, 출력되는 모습을 보이고 있다. 이것이 클로저 현상이다.

​    

