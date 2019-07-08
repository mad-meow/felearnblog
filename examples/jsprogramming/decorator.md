# ES7新特性 -- 装饰器(decorator)

>参考链接：
- [ES7 Decorator 装饰器 | 淘宝前端团队](https://segmentfault.com/p/1210000009968000/read)
- [Decorators in ES7](http://www.liuhaihua.cn/archives/115548.html)
- [设计模式——装饰模式（Decorator）](https://blog.csdn.net/zhshulin/article/details/38665187)
- [装饰器模式 | 菜鸟教程](https://www.runoob.com/design-pattern/decorator-pattern.html)

## 1. 装饰器模式
装饰器模式又称为包装（wrapper）模式，是继承关系的一个替代方案。这种设计模式用来在不改变原有类的基础上，向其动态的添加额外的功能，而生成的示例将有和原来一样的接口（但一些接口的功能进行了扩展）。

使用场景：日志记录，安全检查，缓存等

## 2. ES7中使用示例方法
以钢铁侠为例，通过装备提升其基础能力。示例代码（装饰器代码需要[Babel转译](https://babeljs.io/repl/)才能使用)：  
```js
// 原始类
class Man {
    constructor(def = 2, atk = 3, hp = 3) {
        this.init(def, atk, hp);
    }

    init(def, atk, hp) {
        this.def = def;
        this.atk = atk;
        this.hp = hp;
    }

    toString() {
        return `Def: ${this.def}, Atk: ${this.atk}, HP: ${this.hp}`;
    }
}

var tony = new Man();
console.log(`Tony的能力：${tony}`); // 2, 3, 3
```
向原始类加上修饰器：
```js
// 对类中某个方法的装饰器函数，返回一个属性描述符
function decorateArmour(target, key, descriptor) {
    const method = descriptor.value;
    let addDef = 100;
    let newVal;
    descriptor.value = (...args) => {
        args[0] += addDef;
        newVal = method.apply(target, args);
        return newVal; 
    }
    return descriptor;
}

// 对类作用的装饰器函数，返回类
function addFly(target) {
    let extra = '-(获得飞行能力)';
    let method = target.prototype.toString;
    target.prototype.toString = (...args) => {
        return method.apply(target.prototype, args) + extra;
    }
    return target;
}

// 在原始类上添加装饰器
@addFly
class Man {
     constructor(def = 2, atk = 3, hp = 3) {
        this.init(def, atk, hp);
    }

    @decorateArmour
    init(def, atk, hp) {
        this.def = def;
        this.atk = atk;
        this.hp = hp;
    }

    toString() {
        return `Def: ${this.def}, Atk: ${this.atk}, HP: ${this.hp}`;
    }
}
var tony = new Man();
console.log(`Tony的能力：${tony}`); // 102, 3, 3-(获得飞行能力)
```

## 3. ES7中装饰器(decorator)相关说明
ES7中的`@decorator`的实现是基于ES5的`Object.defineProperty`方法的语法糖。

## 4. 参考Babel转译后的代码
```js
var _class, _class2;

function _applyDecoratedDescriptor(
  target,
  property,
  decorators,
  descriptor,
  context
) {
  var desc = {};
  Object.keys(descriptor).forEach(function(key) {
    desc[key] = descriptor[key];
  });
  desc.enumerable = !!desc.enumerable;
  desc.configurable = !!desc.configurable;
  if ("value" in desc || desc.initializer) {
    desc.writable = true;
  }
  desc = decorators
    .slice()
    .reverse()
    .reduce(function(desc, decorator) {
      return decorator(target, property, desc) || desc;
    }, desc);
  if (context && desc.initializer !== void 0) {
    desc.value = desc.initializer ? desc.initializer.call(context) : void 0;
    desc.initializer = undefined;
  }
  if (desc.initializer === void 0) {
    Object.defineProperty(target, property, desc);
    desc = null;
  }
  return desc;
}

// 对类中某个方法的装饰器函数，返回一个属性描述符
function decorateArmour(target, key, descriptor) {
  const method = descriptor.value;
  let addDef = 100;
  let newVal;

  descriptor.value = (...args) => {
    args[0] += addDef;
    newVal = method.apply(target, args);
    return newVal;
  };

  return descriptor;
} // 对类作用的装饰器函数，返回类

function addFly(target) {
  let extra = "-(获得飞行能力)";
  let method = target.prototype.toString;

  target.prototype.toString = (...args) => {
    return method.apply(target.prototype, args) + extra;
  };

  return target;
} // 在原始类上添加装饰器

let Man =
  addFly(
    (_class = ((_class2 = class Man {
      constructor(def = 2, atk = 3, hp = 3) {
        this.init(def, atk, hp);
      }

      init(def, atk, hp) {
        this.def = def;
        this.atk = atk;
        this.hp = hp;
      }

      toString() {
        return `Def: ${this.def}, Atk: ${this.atk}, HP: ${this.hp}`;
      }
    }),
    _applyDecoratedDescriptor(
      _class2.prototype,
      "init",
      [decorateArmour],
      Object.getOwnPropertyDescriptor(_class2.prototype, "init"),
      _class2.prototype
    ),
    _class2))
  ) || _class;

var tony = new Man();
console.log(`Tony的能力：${tony}`); // 102, 3, 3-(获得飞行能力)
```