- 对象类别
    1. 普通对象：拥有所有 JS 对象的默认内部行为
    2. 外来对象：内部行为不同于默认行为
    3. 标准对象：由 ES6 定义，如 `Array`，`Date`；标准对象可以是普通对象或是外来对象
    4. 內建（build-in）对象：一段脚本开始执行后，存在于 JS 执行环境中；所有普通对象都是內建对象
- 对象属性初始化的简写

    ```js
    // es5
    function createPerson(name, age) {
        return {
            name: name,
            age: age
        };
    }
    // es6
    function createPerson(name, age) {
        return {
            name,
            age
        };
    }
    ```

- 对象字面量方法的简练写法

    ```js
    // es5
    var person = {
        sayHi: function () {
            console.log('hi');
        }
    };
    // es6
    var person = {
        sayHi() {
            console.log('hi');
        }
    };
    ```

    - es6 的写法的方法可以用 `super`
- computed property name

    ```js
    var suffix = ' name';
    var person = {
        ['first' + suffix]: 's',
        ['last' + suffix]: 'b'
    };
    console.log(person['first name']);  // 's'
    ```

# `Object.assign()`
- mixins：一个对象得到其它对象的方法和属性

    ```js
    function mixin(receiver, supplier) {
        Object.keys(supplier).forEach(function (key) {
            receiver[key] = supplier[key];
        });
    }
    ```

    - 浅拷贝
    - receiver 不通过继承的方式获得 supplier 的属性
- `Object.assign()` 实现和 mixins 一样的功能
- `Object.assign(receiverObj, supplierObj1,supplierObj2)`
    - 后面的 supplier 会覆盖前面的 supplier 的属性值
- Keep in mind that `Object.assign()` doesn’t create accessor properties on the receiver when a supplier has accessor properties. Since `Object.assign()` uses the assignment operator, an accessor property on a supplier will become a data property on the receiver. For 

    ```js
    var receiver = {};
    var supplier = {
        get name() {
            return 'file.js'
        }
    };
    Object.assign(receiver, supplier);
    var descriptor = Object.getOwnPropertyDescriptor(receiver, 'name');
    console.log(descriptor.value);      // file.js
    console.log(descriptor.get);        // undefined
    ```

    - `receiver.name` exists as a data property with a value of "file.js" because `supplier.name` returned "file.js" when `Object.assign()` was called.

