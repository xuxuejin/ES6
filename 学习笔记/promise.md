## Promise创建的时候是立即执行的（同步）

    let p = new Promise(function(resolve, reject){
        console.log("new promise"); //同步执行
        resolve("success");
    });

    console.log("after new Promise");

    p.then(function(value){ //异步
        console.log(value);
    });

    输出
    "new promise"
    "after new Promise"
    "success"

## Promise接收的函数参数是同步执行的，但then方法中的回调函数执行则是异步的

    let p = new Promise(function(resolve, reject){
        resolve("success");
    });

    p.then(function(value){
        console.log(value);
    });

    console.log("which one is called first ?");

    输出
    "which one is called first ?"
    "success"

## 当Promise和定时器同时存在
    let p1 = new Promise(function(resolve, reject){
        console.log('p1');
        resolve(1);
    });

    setTimeout(function(){
      console.log('setTimeout');
    },0)

    p1.then(function(value){
      console.log(value);
    })

    输出
    p1
    1
    setTimeout

##### 为什么then会优先于定时器先执行？
    因为等待队列（或者说是任务队列）其实是分为两个： macrotask（宏任务） 和 microtask（微任务）
    promise是存放在microtasks中，而定时器是存放在macrotasks中
    每次"事件循环"后会先执行microtask中的任务，直到整个microtask队列执行结束，才会执行macrotask中的任务

    macrotask主要包含：
    script（整体代码）、setTimeout、setInterval、I/O、UI交互事件、postMessage、MessageChannel、setImmediate（node环境）
    
    micro-task主要包含：
    Promise.then、MutaionObserver、MessageChannel、process.nextTick（node环境）
    
## Promise.resolve() 和 Promise.reject()都是 new Promise（）的快捷方式

    Promise.resolve('Success');
    
    这段代码会让这个Promise对象立即进入resolved状态，并将结果success传递给then指定的onFulfilled回调函数
    由于Promise.resolve()也是返回Promise对象，因此可以用.then()处理其返回值
    
    /*******等同于*******/
    new Promise(function (resolve) {
        resolve('Success');
    });
    

    Promise.reject(new Error('error'));
    
    这段代码会让这个Promise对象立即进入rejected状态，并将错误对象传递给then指定的onRejected回调函数
    
    /*******等同于*******/
    new Promise(function (resolve, reject) {
        reject(new Error('error'));
    });
    
    
参考：http://liubin.org/promises-book/

  
