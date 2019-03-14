## 对象字面量的简写：指以{}形式直接表示的对象
    
    1.属性的简洁表示法
      -----ES5-----
      var listeners = [];

      function listen() {}

      var events = {
          listeners: listeners,
          listen: listen
      }

      -----ES6-----
      var listeners = [];

      function listen() {}

      var events = { listeners, listen }
    
    2.可计算的属性名
      -----ES5-----
      var expertise = 'journalism';

      var person = {
          name: 'Sharon',
          age: 27
      }
      person[expertise] = {
          years: 5,
          interests: ['international', 'politics', 'internet']
      }

      -----ES6-----把任何表达式放在中括号中，表达式的运算结果将会是对应的属性名
      var expertise = 'journalism';

      var person = {
          name: 'Sharon',
          age: 27,
          [expertise]: {
              years: 5,
              interests: ['international', 'politics', 'internet']
          }
      }
      
      
      ★注意：简写属性和计算的属性名不可同时使用，简写属性是一种在编译阶段的就会生效的语法糖，而计算的属性名则在运行时才生效，如果你把二者混用，代码会报错，而且二者混用往往还会降低代码的可读性
      
      3.对象方法定义的简写
        -----ES5-----
        var emitter = {
            events: {},
            on: function (type, fn) {
              // coding...
            },
            emit: function (type, event) {
              // coding...
            }
        }

        -----ES6-----允许省略对象方法的function关键字及之后的冒号
        var emitter = {
            events: {},
            on(type, fn) {
              // coding...
            },
            emit(type, event) {
              // coding...
            }
        }
        
      4.箭头函数
        -----ES5-----
        var example = function (parameters) {
          // function body
        }
        
        -----ES6-----箭头函数不需要使用function关键字，其参数和函数体之间以=>相连接
        var example = (parameters) => {
          // function body
        }
        
      5.箭头函数的简写
      
        (1)当只有一个参数时，可以省略箭头函数参数两侧的括号

          var double = value => {
              return value * 2
          }

        (2)对只有单行表达式且该表达式的值为返回值,函数体的{}可以省略，return 关键字可以省略，会静默返回该单一表达式的值

          var double = (value) => value * 2

        (3)上述两种形式可以合并使用

          var double = value => value * 2
          
        简写箭头函数注意事项：当简写箭头函数返回值为一个对象时，需要用小括号括起返回的对象，否则，浏览器会把对象的{}解析为箭头函数函数体的开始和结束标记
          // 正确的书写方式
          var objectFactory = () => ({ modular: 'es6' })
          
        注意：
          箭头函数不能被直接命名，不过允许它们赋值给一个变量；
          箭头函数不能用做构造函数，你不能对箭头函数使用new关键字；
          箭头函数也没有prototype属性；
          箭头函数绑定了词法作用域，不会修改this的指向

      
      






















