```
            
let
 
timer
 
=
 
setTimeout
(()
=>
 {
```

```
                
clearTimeout
(
timer
)
```

```
                
let
 
drawerDom
 
=
 
document
.
querySelector
(
'.u-drawer'
)
```

```
                
let
 
copyone
 
=
 
drawerDom
```

```
                
drawerDom
.
parentNode
.
removeChild
(
drawerDom
)
```

```
                
document
.
body
.
appendChild
(
copyone
)
```

```
            }, 
20
)
```