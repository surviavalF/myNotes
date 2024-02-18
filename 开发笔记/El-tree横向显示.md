```
//
```

_树节点的内容区的渲染_

```
 Function
```

```
const
 
renderContent
 
=
 (
h
, { 
node
, 
data
, 
store
 }) 
=>
 {
```

```
  
let
 
classname
 
=
 
""
;
```

```
  
// 
```

_由于项目中有三级菜单也有四级级菜单，就要在此做出判断_

```
  
if
 (
node
.
level
 
===
 
4
) {
```

```
    
classname
 
=
 
"foo"
;
```

```
  }
```

```
  
if
 (
node
.
level
 
===
 
3
 
&&
 
node
.
childNodes
.
length
 
===
 
0
) {
```

```
    
classname
 
=
 
"foo"
;
```

```
  }
```

```
  
if
 (
node
.
level
 
===
 
2
 
&&
 
node
.
childNodes
.
length
 
===
 
0
) {
```

```
    
classname
 
=
 
"foo"
;
```

```
  }
```

```
  
return
 
h
(
```

```
    
"p"
,
```

```
    {
```

```
      
class
: 
classname
,
```

```
    },
```

```
    
node
.
label
```

```
  );
```

```
};
```

```
//
```

_节点被展开时触发的事件_

```
const
 
handleExpand
 
=
 () 
=>
 {
```

```
  
//
```

_因为该函数执行在_

```
renderContent
```

_函数之前，所以得加_

```
this.$nextTick()
```

```
  
proxy
.
$nextTick
(() 
=>
 {
```

```
    
changeCss
();
```

```
  });
```

```
};
```

```
//
```

_更改_

```
css
```

```
const
 
changeCss
 
=
 () 
=>
 {
```

```
  
let
 
levelName
 
=
 
document
.
getElementsByClassName
(
"foo"
); 
// levelname
```

_是上面的最底层节点的名字_

```
  
for
 (
let
 
i
 
=
 
0
; 
i
 
<
 
levelName
.
length
; 
i
++
) {
```

```
    
// cssFloat 
```

_兼容_

```
 ie6-8  styleFloat 
```

_兼容_

```
ie9
```

_及标准浏览器_

```
    
levelName
[
i
].
parentNode
.
style
.
cssFloat
 
=
 
"left"
; 
// 
```

_最底层的节点，包括多选框和名字都让他左浮动_

```
    
levelName
[
i
].
parentNode
.
style
.
styleFloat
 
=
 
"left"
;
```

```
    
levelName
[
i
].
parentNode
.
onmouseover
 
=
 
function
 () {
```

```
      
this
.
style
.
backgroundColor
 
=
 
"#fff"
;
```

```
    };
```

```
  }
```

```
};
```

```
<
el-tree
```

```
class
=
"el-tree"
```

```
ref
=
"refElTree"
```

```
:
data
=
"
routeList
"
```

```
show-checkbox
```

```
node-key
=
"value"
```

```
:
props
=
"
defaultProps
"
```

```
@
node-expand
=
"
handleExpand
"
```

```
:
render-content
=
"
renderContent
"
```

```
></
el-tree
>
```

```
let
 
routeList
 
=
 
ref
([]); 
//
```

_树节点_

```
￼
let
 
defaultProps
 
=
 
ref
({
```

```
  
children
: 
"children"
,
```

```
  
label
: 
"label"
,
```

```
}); 
//
```

_树节点_