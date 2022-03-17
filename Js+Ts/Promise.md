#### Promise 认知流程

1. **关于 promise**
   - promise 是一种异步编程的解决方案,一个 promise 实例可以看做是一个容器,里面保存了异步操作的结果状态(等待,完成或者失败),同时提供了处理异步操作结果的方法(then ,catch 等等)
   - 注意点:1. promise 实例化时, resolve 或者 reject 调用后,后续的代码依旧执行. 2. promise 实例如果 resolve 一个实例后,该实例的 promise 状态将会被新 promise 重置
2. **promise实例和Promise的常见方法**
   - then
   1. then 方法将会在 promise 实例变为 resolve 状态后调用,并且会把 resolve 传入的值作为 then 方法中回调函数的实参.
   2. then 方法的回调函数返回的是一个 promise 实例,依次 then 方法后续也可以继续链式调用 then 方法.
   - catch
   1. catch 方法会捕获 promise 实例化时 reject 状态或错误抛出,也会不会 catch 前面所有 then 方法的错误抛出(只能捕捉前面不能捕捉后面的);下面的例子中,catch将会捕获三种错误.

    ```
    const p1 = () => Promise.reject("p1");
    const p2 = Promise.resolve("p2");
    p2.then(() => p1())
    .then((res) => console.log(res))
    .catch((error) => console.log(error));
    ```
   * Promise.resolve
   1. Promise.resolve 方法返回一个resolve状态的promise实例
   2. 如果传入的是resolve实例则完整返回这个实例,否则通常传入的参数作为resolve状态的值
   * Promise.reject
   1. Promise.reject 方法返回一个reject的promise实例
   2. reject方法传入的参数会作为返回promise实例的catch方法的回调函数实参

3. **promise应用**
* 如何让多个异步操作顺序执行
    ```
    const asyncList =  new Array(4).fill(() => new Promise((resolve,reject) => {
        setTimeout(() => {
            console.log(1234)
            resolve(100)
        }, 1000);
    }))
    
    let promiseStart = Promise.resolve()
    
    asyncList.forEach(p => {
        promiseStart = promiseStart.then(() => p())
    })
    
    
    ```
* 声明一个类,它的实例具有一个可以定时打印字符的能力并且可以链式调用

