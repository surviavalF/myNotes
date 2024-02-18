```
    
// 
```

_假设你有一个对象数组_

```
var 
array
 
=
 [
```

```
  { 
id
: 
1
, 
name
: 
'Object 1'
 },
```

```
  { 
id
: 
2
, 
name
: 
'Object 2'
 },
```

```
  { 
id
: 
3
, 
name
: 
'Object 3'
 }
```

```
];
```

```
// 
```

_要查找的_

```
ID
```

```
var 
searchId
 
=
 
2
;
```

```
// 
```

_使用数组的_

```
find
```

_方法查找对象_

```
var 
resultObject
 
=
 
array
.
find
(
function
(
obj
) {
```

```
  
return
 
obj
.
id
 
===
 
searchId
;
```

```
});
```

```
// 
```

_输出结果对象_

```
console.log(resultObject);
```