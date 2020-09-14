# Key Note
## require
+ require 函数是同步顺序寻找的.（核心模块-->当前目录-->node_modules）
+ require 是Node中少数的几个同步I/O操作之一，不可再I/O密集的地方调用require，否则会有性能问题。比如 每个请求都用了require这类情况。
+ require(./demo.js)表示在当前目录寻找。并且js后缀可以省略。

## exports
+ 正确用法是：
` module.exports = function/object`,不能省略“module.” 或者这样写：
`exports.function = function`
+ 如果module中既有module.exports 又有exports，那么exports 会被忽略。