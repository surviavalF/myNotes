```js
    // 假设你有一个对象数组

var array = [

  { id: 1, name: 'Object 1' },

  { id: 2, name: 'Object 2' },

  { id: 3, name: 'Object 3' }

];

// 要查找的ID

var searchId = 2;

// 使用数组的find方法查找对象

var resultObject = array.find(function(obj) {

  return obj.id === searchId;

});

// 输出结果对象

console.log(resultObject);
```