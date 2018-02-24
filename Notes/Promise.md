```js
'use strict';

const PENDING = Symbol();
const FULFILLED = Symbol();
const REJECTED = Symbol();

function Promisee(fn) {
    if (typeof fn != 'function') {
        throw new Error('resolver should be a function!');
    }

    let state = PENDING;
    let value = null;
    let handler = [];

    function fulfill(result) {
        state = FULFILLED;
        // 用value保存 fulfilled时候的值
        value = result;
        // next里面根据state 执行fulfilled或者rejected
        handler.forEach(next);
        handler = null;
    }

    function reject(err) {
        state = REJECTED;
        value = err;
        handler.forEach(next);
        handler = null;
    }

    function resolve(result) {
        // 处理 resolve时候 返回的可能还是一个Promise
        try {
            let then = typeof result.then == 'function' ? result.then : null;
            if (then) {
                then.bind(result)(resolve, reject);
                return;
            }
            // 非Promise fulfill里设置全局value
            fulfill(result);
        } catch (err) {
            reject(err);
        }
    }

    function next({ onFulfill, onReject }) {
        switch (state) {
            case FULFILLED:
                // 传入value
                onFulfill && onFulfill(value);
                break;
            case REJECTED:
                onReject && onReject(value);
                break;
            case PENDING:
                handler.push({ onFulfill, onReject });
        }
    }

    this.then = function (onFulfill, onReject) {
        return new Promisee((resolve, reject) => {
            console.log('resolve, reject', resolve, reject);
            next({
                onFulfill: (val) => {
                    // val from next methods
                    try {
                        // then方法onFulfill 第一个回调函数的参数接收到value
                        // resolve 接受 onFulfill的返回值
                        resolve(onFulfill(val));
                    } catch (err) {

                    }
                },
                onReject: (err) => {
                    reject(onReject(val));
                }
            });
        });
    }
    // new的时候 赋值resolve reject回调参数
    fn(resolve, reject);
}
var p1 = new Promisee((resolve, reject) => {
    setTimeout(() => {
        resolve(3000);
    }, 3000)
})
p1
    .then(res => {
        console.log(res);
    }, rej => {
        console.log(rej);
    })
 ```
