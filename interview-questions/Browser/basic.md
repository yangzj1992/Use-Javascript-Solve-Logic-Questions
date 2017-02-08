Q : 浏览器事件模型和回调机制

A : JavaScript作为单线程运行于浏览器之中

同时出于对UI线程操作的安全性考虑，JavaScript和UI线程也处于同一个线程中。因此对于长时间的耗时操作，将会阻塞UI的响应。为了更好的UI体验，应该尽量的避免JavaScript中执行较长耗时的操作（如大量for循环的对象diff等）或者是长时间I/O阻塞的任务。所以在浏览器中的大多数任务都是异步（无阻塞）执行的，例如：鼠标点击事件、窗口大小拖拉事件、定时器触发事件、Ajax完成回调事件等。当每一个异步事件完成时，它都将被放入一个叫做”浏览器事件队列“中的事件池中去。而这些被放在事件池中的任务，将会被javascript引擎单线程处理的一个一个的处理，当在此次处理中再次遇见的异步任务，它们也会被放到事件池中去，等待下一次的tick被处理。另外在HTML5中引入了新的组件-Web Worker，它可以在JavaScript线程以外执行这些任务，而不阻塞当前UI线程。

由于浏览器的这种内部事件循环机制，所以JavaScript一直主以callback回调的方式来处理事件任务。