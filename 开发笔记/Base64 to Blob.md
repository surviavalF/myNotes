```
function
 
base64ConvertToBlob
() {
```

```
  
function
 
base64ToBlob
({
```

```
    
b64data
 
=
 
""
,
```

```
    
contentType
 
=
 
""
,
```

```
    
sliceSize
 
=
 
512
```

```
  } 
=
 {}) {
```

```
    
return
 
new
 
Promise
((
resolve
, 
reject
) 
=>
 {
```

```
      
// 
```

_使用_

```
 atob() 
```

_方法将数据解码_

```
      
let
 
byteCharacters
 
=
 
atob
(
b64data
);
```

```
      
let
 
byteArrays
 
=
 [];
```

```
      
for
 (
```

```
        
let
 
offset
 
=
 
0
;
```

```
        
offset
 
<
 
byteCharacters
.
length
;
```

```
        
offset
 
+=
 
sliceSize
```

```
      ) {
```

```
        
let
 
slice
 
=
 
byteCharacters
.
slice
(
offset
, 
offset
 
+
 
sliceSize
);
```

```
        
let
 
byteNumbers
 
=
 [];
```

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
 
slice
.
length
; 
i
++
) {
```

```
          
byteNumbers
.
push
(
slice
.
charCodeAt
(
i
));
```

```
        }
```

```
        
// 8 
```

_位无符号整数值的类型化数组。内容将初始化为_

```
 0
```

_。_

```
        
// 
```

_如果无法分配请求数目的字节，则将引发异常。_

```
        
byteArrays
.
push
(
new
 
Uint8Array
(
byteNumbers
));
```

```
      }
```

```
      
let
 
result
 
=
 
new
 
Blob
(
byteArrays
, {
```

```
        
type
: 
contentType
```

```
      });
```

```
      
result
 
=
 
Object
.
assign
(
result
, {
```

```
        
// 
```

_这里一定要处理一下_

```
 URL.createObjectURL
```

```
        
preview
: 
URL
.
createObjectURL
(
result
),
```

```
        
name
: 
`XXX.png`
```

```
      });
```

```
      
resolve
(
result
);
```

```
    });
```

```
  }
```

```
  
return
 
new
 
Promise
((
resolve
) 
=>
 {
```

```
    
Promise
.
all
(
```

```
      
formData
.
value
.
imgLists
.
map
(
async
 (
item
, 
index
) 
=>
 {
```

```
        
if
 (
item
.
indexOf
(
"base64"
) 
>
 
-
1
) {
```

```
          
let
 
base64
 
=
 
item
.
split
(
","
)[
1
];
```

```
          
return
 (
index
 
=
 {
```

```
            
imgList
: 
await
 
base64ToBlob
({
```

```
              
b64data
: 
base64
,
```

```
              
contentType
: 
"image/png"
```

```
            })
```

```
          });
```

```
        } 
else
 {
```

```
          
return
 (
index
 
=
 { 
oldList
: 
item
 });
```

```
        }
```

```
      })
```

```
    )
```

```
      .
then
(
resolve
)
```

```
      .
catch
((
err
) 
=>
 {
```

```
        
console
.
log
(
err
);
```

```
      });
```

```
  });
```

```
}
```