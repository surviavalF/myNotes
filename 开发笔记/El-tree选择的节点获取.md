
当父节点中的子节点未完全选择，父组件是半选择状态时，想要获取全部节点（包括半选择的父节点）使用此方法

```js
let Nodes = [

    ...refElTree.value.getHalfCheckedKeys(),

    ...refElTree.value.getCheckedKeys(),

  ];

```

el-tree组件在获取选择的节点时，默认的逻辑是，选中父节点时所有的子节点会被选中（checked），但是当该节点下不是选中所有子节点的时候，主节点不会被选中，而是处于一种半选中状态，提交时通过 getCheckedKeys() 方法也不会提交父节点，因为半选中状态下 checked 属性是 false 的。

解决办法

通常如果只是为了提交数据，我们可以使用getHalfCheckedKeys()+getCheckedKeys()来获取需要的数据

const data=[  
...this.$refs.tree.getHalfCheckedKeys(),  
...this.$refs.tree.getCheckedKeys()  
]

但是如果需要保存数据且需要编辑，那在编辑初始设置选中项的时候将遇到问题，所以我们只能使用el-tree现有的api来自己实现需要的功能，el-tree中有一个属性check-strictly（在显示复选框的情况下，是否严格的遵循父子不互相关联的做法，默认为 false）意思就是勾选父节点和勾选子节点，没有任何的关系。这是为了解决默认选中节点加载时，选中父节点会同时选中所以子节点，显然这不是我们想要的。

<el-tree  
    show-checkbox  
    node-key="id"  
    check-strictly  
    @check-change="checkChange"  
    ref="tree">  
</el-tree>

然后使用 check-change 事件（节点选中状态发生变化时的回调）

共三个参数，依次为：传递给 data 属性的数组中该节点所对应的对象、节点本身是否被选中、节点的子树中是否有被选中的节点

```js
checkChange(data, check) {  
      // 父节点操作  
      if (data.parentId !== null) {  
        if (check === true) {  
          // 如果选中，设置父节点为选中  
          this.$refs.tree.setChecked(data.parentId, true);  
        } else {  
          // 如果取消选中，检查父节点是否该取消选中（可能仍有子节点为选中状态）  
          var parentNode = this.$refs.tree.getNode(data.parentId);  
          var parentHasCheckedChild = false;  
          for (  
            var i = 0, parentChildLen = parentNode.childNodes.length;  
            i < parentChildLen;  
            i++  
          ) {  
            if (parentNode.childNodes[i].checked === true) {  
              parentHasCheckedChild = true;  
              break;  
            }  
          }  
          if (!parentHasCheckedChild)  
            this.$refs.tree.setChecked(data.parentId, false);  
        }  
      }  
      // 子节点操作，如果取消选中，取消子节点选中  
      if (data.children != null && check === false) {  
        for (var j = 0, len = data.children.length; j < len; j++) {  
          var childNode = this.$refs.tree.getNode(data.children[j].id);  
          if (childNode.checked === true) {  
            this.$refs.tree.setChecked(childNode.data.id, false);  
          }  
        }  
      }  
    }
```
