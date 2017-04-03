## TypeScript

* javascript compile언어

* Benefits
  * Static typing을 사용함으로써 좀더 예측가능한 코드가 되고, 디버깅이 쉬워진다.
  * Compile Step이 있음으로써 코드가 런타임에 동작하기 전에 에러를 알아낼수 있다.
  * Angular2에 사용됨.

* Installation
  * npm install -g typescript
    * npm 설치 on Mac
      * brew install node
  * tsc -v

* Text Editor
  * Visual Studio Code

* Compiling
  * tsc {filename}.ts
  * will make {filename}.js , if it is already exist, overwrite
  * --watch = option to automatically compile when changes are made

* Static Typing
  * var burger: string = 'hamburger'
    * 타입 정의를 위한 latter은 js파일로 컴파일 이후에 사라짐
  * function speak(food: string, energy: number): void { ... }
    * 리턴타입도 js파일로 컴파일 이후에는 사라짐.
  * Common data types
    * Number
    * String
    * Boolean
    * Any
    * Arrays : number[], Array<number>
    * Void

* Interface
  * 특정 object가 어떠한 structure에 fits한지 체크할때 사용
  * javascript로 translate될때 interface는 사라진다.
  * order는 체크하지 않으며, 단지 properties가 존재하는지, 의도한 타입인지 체크한다.
  * property가 없거나, 잘못된 타입이거나, 이름이 다를때 컴파일러가 에러를 보여줌.

* classes
  * OOP 스타일을 비슷하게 지원함.
  *

  ```javascript
  class Menu {
    // Our properties:
    // By default they are public, but can also be private or protected.
    items: Array<string>;  // The items in the menu, an array of strings.
    pages: number;         // How many pages will the menu be, a number.

    // A straightforward constructor.
    constructor(item_list: Array<string>, total_pages: number) {
      // The this keyword is mandatory.
      this.items = item_list;    
      this.pages = total_pages;
    }

    // Methods
    list(): void {
      console.log("Our menu for today:");
      for(var i=0; i<this.items.length; i++) {
        console.log(this.items[i]);
      }
    }
  }
  ```

* Generics
  ```javascript

  function genericFunc<T>(argument: T): T[] {    
    var arrayOfT: T[] = [];    // Create empty array of type T.
    arrayOfT.push(argument);   // Push, now arrayOfT = [argument].
    return arrayOfT;
  }

  var arrayFromString = genericFunc<string>("beep");
  console.log(arrayFromString[0]);         // "beep"
  console.log(typeof arrayFromString[0])   // String

  ```

* let vs var
  * scope
    * let = block scope
    * var = function scope
  * ...?
