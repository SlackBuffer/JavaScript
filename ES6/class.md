- `class` 的写法是语法糖
    - `class` 的类型是 "function"
- 类声明的要点
    - `class` 声明不会被提升（包括类的表达式），表现得就像用 `let` 声明的效果一样
    - `class` 里的代码自动运行在严格模式
    - 类里的所有方法不可枚举
    - 类的内部不可以覆盖类的值
    - 建议把类的所有实例实行放在 `constructor` 函数里
- 命名的类表达式只在类的内部能被访问到，类的外部访问不到
- `extends()`
- `super(args)` === `Father.call(this, args)`，使得子类继承父类 `constructor` 方法里的属性
    - 只有子类（使用了 `extends` 的类）才可以使用 `super()`
    - `super()` 负责初始化 `this`，必须在调用 `super()` 之后才能访问 `this`
    - 避免 `super()` 的调用的唯一方法是在类的构造函数里返回一个对象
- 子类若定义了 `constructor` 方法则必须使用 `super()`，否则报错
    - 若不使用 `constructor`，`super()` 会被自动调用
        - 此时子类的所有参数都会被传给父类，不必要
        - 所以最好不省略，然后指定要传入的参数

    ```js
    class Square extends Rectangle {
        // no constructor

    }
    // equivalent ot 

    class Square extends Rectangle {
        constructor(...args) {
            super(...args);
        }
    }  
    ```

- 子类上的方法会屏蔽父类上的同名方法
    - 用 `super.foo()` 指定调用父类上的方法
- 子类也可以访问到父类的静态成员
- ES6 支持对任何可以解析为函数，并有 `[[Construct]]` 和 `prototype` 属性的表达式使用 `extends`
- 继承內建
    - ES5 的 classical inheritance 的 `this` 先是指向子类，再修饰以父类的属性
    - ES6 基于类的继承，`this` 先是指向父类，再被子类的 `constructor` 修饰，使得 `this` 可以得到父类的所有內建属性 
- [ ] `Symbol.species` 
- [ ] `new.target`