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

