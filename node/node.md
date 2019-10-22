# node 多进程与多线程

### node中多进程

node中进行进程的创建有多种方式，包括使用process模块 ， child_process模块 ， 还有cluster 模块 。

一般node中进程的创建主要是依赖与对于主进程的fork  ， 而主进程只负责子进程的管理和调度 ， 不负责任务的执行。fork进程的数量应当与自己的CPU核心数相关 ， 不应超过CPU核心数 。

```javascript
//在node 中可以查询到CPU的相关信息
var cups = require('os').cpus()
var Muncpus = cups.length                  //通过length可以得知CPU的总数量
```



fork子进程的demo

child_process 模块:

```javascript
const childProcess = require('child_process')

 const option = {
    maxBuffer:100*1024            //在exec中默认值为200*1024 , 超出范围会导致程序的崩溃。
    encoding: 'utf8',
    timeout:5000
}
 //在另一个进程上执行系统命令
 var child = childProcess.exec("mkdir a" , option , function(error , stdout , stderr){//stdout , stderr 都是包含执行命令的输出的Buffer对象
    if(error){
        console.log(error.stack)
        console.log('Error Code:'+error.code)
        console.log('Error Signal:'+error.signal)
    }
    console.log('Results:\n'+stdout)
    if(stderr.length){
        console.log('Error :'+stderr)
    }
})

child.on('exit' , function(code){
    console.log('Completed with code: '+code)
})


const  fork = require('child_process').fork

const compute = fork('./md.js')

compute.on('message'  ,  message =>{
    console.log('serve'  + message)
})

compute.on('close' , (code ,  singal) =>{
    console.log(`收到信号 ${singal} , 退出码${code}`)
    compute.kill()
})
```

cluster 模块 ：

```javascript
const cluster = require('cluster')
const http = require('http')
const cups = require('os').cpus()
const Muncpus = cups.length

if(cluster.isMaster){
    cups.forEach(() => {
        cluster.fork()
    })
    cluster.on('fork' , function(worker){
        console.log('serve create:'+worker.id)
    })
    cluster.on('listening' , function(worker , address){
        console.log('serve:'+worker.id+"is listening on"+address.address)
    })
    cluster.on('exit' , function(worker, code ,signal){
        console.log('serve'+worker.id+'die')
    })
}else{
    http.createServer(function(req , res){
        res.writeHeader(200)
        res.end('hell world')
        console.log('serve: '+process.pid+'make a respose')

    }).listen(8000)
}
```

child_process 和 cluster 都是解决node单线程 ， 而无法利用多核CPU而出现的。核心就是父进程负责监听端口，接到请求后将其发给下面的子进程进行执行。

child_process 和cluster 不同的地方就是child_process 可以控制多个进程集群 ， 而cluster只能控制一个。

cluster中的进程之间的主进程和子进程可以通过`cluster.isMaster`来进行判断 ，而每一个worker都有自己的id表示。



![](./img/node/child)

![](./img/node/cluter)

### node中多线程

node真正提供多线程的能力 ：`worker_threads`

直到 Node 10.5.0 的发布，官方才给出了一个实验性质的模块 worker_threads 给 Node 提供真正的多线程能力。

- isMainThread: 是否是主线程，源码中是通过 threadId === 0 进行判断的。
- MessagePort: 用于线程之间的通信，继承自 EventEmitter。
- MessageChannel: 用于创建异步、双向通信的通道实例。
- threadId: 线程 ID。
- Worker: 用于在主线程中创建子线程。第一个参数为 filename，表示子线程执行的入口。
- parentPort: 在 worker 线程里是表示父进程的 MessagePort 类型的对象，在主线程里为 null
- workerData: 用于在主进程中向子进程传递数据（data 副本）

```javascript
const { Worker, isMainThread, parentPort } = require('worker_threads');

if (isMainThread) {
  const worker = new Worker(isMainThread: 是否是主线程，源码中是通过 threadId === 0 进行判断的。
MessagePort: 用于线程之间的通信，继承自 EventEmitter。
MessageChannel: 用于创建异步、双向通信的通道实例。
threadId: 线程 ID。
Worker: 用于在主线程中创建子线程。第一个参数为 filename，表示子线程执行的入口。
parentPort: 在 worker 线程里是表示父进程的 MessagePort 类型的对象，在主线程里为 null
workerData: 用于在主进程中向子进程传递数据（data 副本）__filename);
  worker.once('message', (message) => {
    console.log(message);  // Prints 'Hello, world!'.
  });
  worker.postMessage('Hello, world!');
} else {
  // When a message from the parent thread is received, send it back:
  parentPort.once('message', (message) => {
    parentPort.postMessage(message);
  });
}
```



