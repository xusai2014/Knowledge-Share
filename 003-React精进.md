## React 知识分享

### 组件渲染列表

当创建一个元素时，需要添加key属性，否则会提示警告，Why？

keys时帮助识别哪些元素需要改变，比如添加、删除、更新，需要给确定一个标识。

一般呢采用数据的id标志来做key的值，对于顺序发生变化的列表不建议使用索引作为key。
　

经常看到，开发者使用索引作为渲染列表元素的key，例如：
```
{todos.map((todo, index) =>
  <Todo
    {...todo}
    key={index}
  />
)}

```
看上去代码整洁，还能消除警告，但是事实上这是有风险的！It may break your application and display wrong data!

key是用来标识列表元素，假如添加或者删除一个元素，ReactDOM会以为此时key标识的新元素和之前标识的元素是同一个，实际上不是这样的。
[示例](https://jsbin.com/wohima/edit?js,output)

解决方案
```
var shortid = require('shortid');
function createNewTodo(text) {
  return {
    completed: false,
    id: shortid.generate(),
    text
  }
}
```

参考
[Index as a key is an anti-pattern](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318)