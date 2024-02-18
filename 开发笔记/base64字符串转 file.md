```
      
// base64
```

_字符串_

```
      
const
 
base64String
 
=
 
"your_base64_string_here"
;
```

```
      
// 
```

_将_

```
base64
```

_字符串转换为_

```
Blob
```

```
      
const
 
byteCharacters
 
=
 
atob
(
base64String
);
```

```
      
const
 
byteNumbers
 
=
 
new
 
Array
(
byteCharacters
.
length
);
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
 
byteCharacters
.
length
; 
i
++
) {
```

```
        
byteNumbers
[
i
] 
=
 
byteCharacters
.
charCodeAt
(
i
);
```

```
      }
```

```
      
const
 
byteArray
 
=
 
new
 
Uint8Array
(
byteNumbers
);
```

```
      
const
 
blob
 
=
 
new
 
Blob
([
byteArray
], { 
type
: 
"application/octet-stream"
 }); 
// Blob
```

_转为_

```
File
```

_对象_

```
 
```

```
      
const
 
file
 
=
 
new
 
File
([
blob
], 
"filename.jpg"
, { 
type
: 
'image/jpeg'
 });
```