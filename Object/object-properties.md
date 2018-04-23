- `Object()` 实例有如下属性
    - `hasOwnProperty(propertyName)`
    - `obj1.isPrototypeOf(obj2)`
    - `propertyIsEnumerable(propertyName)`
        - 决定属性是否可以用 `for in` 枚举到
    - `toLocaleString()`
    - `toString()`
    - `valueOf()`
        - 通常结果和调用 `toString()` 相同
- 对象属性的内部特性由规范定义，用来实现 JS 引擎，不能直接访问到
    - `[[]]`
- ECMAScript 属性分两类
    1. 数据属性
    2. 访问器属性
# 数据属性
- 4 个特性
    1. `[[Configurable]]`
        - 决定一个属性是否可以删除了再重新定义；是否可以更改属性的特性；是否可以将一个属性的类型改为访问器属性
        - 对于直接定义在对象上的数据属性，值默认为 `true`
    2. `[[Enumeralbe]]`
        - 决定一个属性是否能够被 `for in` 枚举到
        - 对于直接定义在对象上的数据属性，值默认为 `true`
    3. `[[Writable]]`
        - 决定属性值可否更改
        - 对于直接定义在对象上的数据属性，值默认为 `true`
    4. `[[Value]]`
        - 读值、保存属性值的地方
        - 默认值是 `undefined`
- 一个属性被显式加到一个对象上时，该属性的前三个特性的值为 `true`，`[[Value]]` 值是被赋予的值
- 可以通过 `Object.defineProperty()` 方法更改属性的特性值
    - 使用 `Object.defineProperty()` 方法后，若没有显式指定，前三个特性的值均为 `false`
    - 接受 3 个参数
        1. 属性所在的对象
        2. 属性名
        3. 描述器对象
        
        ```javascript
        var person = {};
        Object.defineProperty(person, "job", {
            configurable: false,
            writable: false,
            value: "software engineer"
        });
        ```

        - `configurable` 设为 `false` 表示该属性不可从对象中移除，调用 `detele` 在严格模式下会报错，非严格模式则删除删除操作无效
        - 一旦 `configuable` 设为 `false`，就不能再设回 `true`，就只能更改 `writable` 特性的值，更改其它特性的值回抛错
# 访问器属性
- 读取访问器属性的值时，属性的 `getter` 方法被调用
- 写访问器属性的值时，属性的 `setter` 方法被调用，新值被写入
- 4 个特性
    1. `[[Configurable]]`    
        - 决定一个属性是否可以删除了再重新定义；是否可以更改属性的特性；是否可以将属性类型改为数据属性
    2. `[[Enumerable]]`
        - 决定一个属性是否能够被 `for in` 枚举到
        - 对于直接定义在对象上的属性，值默认为 `true`
    3. `[[Get]]`
        - 读取属性的值时调用的函数
        - 默认值为 `undefined`
    4. `[[Set]]`
        - 写入属性的值时调用的函数
        - 默认值为 `undefined`
- 访问器属性不能直接在对象上定义，必须通过 `Object.defineProperty()`