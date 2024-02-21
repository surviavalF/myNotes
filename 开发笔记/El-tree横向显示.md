```html
<el-tree

class="el-tree"

ref="refElTree"

:data="routeList"

show-checkbox

node-key="value"

:props="defaultProps"

@node-expand="handleExpand"

:render-content="renderContent"

></el-tree>
```

```js
let routeList = ref([]); //树节点  
let defaultProps = ref({

  children: "children",

  label: "label",

}); //树节点
```

```js
//树节点的内容区的渲染 Function

const renderContent = (h, { node, data, store }) => {

  let classname = "";

  // 由于项目中有三级菜单也有四级级菜单，就要在此做出判断

  if (node.level === 4) {

    classname = "foo";

  }

  if (node.level === 3 && node.childNodes.length === 0) {

    classname = "foo";

  }

  if (node.level === 2 && node.childNodes.length === 0) {

    classname = "foo";

  }

  return h(

    "p",

    {

      class: classname,

    },

    node.label

  );

};

//节点被展开时触发的事件

const handleExpand = () => {

  //因为该函数执行在renderContent函数之前，所以得加this.$nextTick()

  proxy.$nextTick(() => {

    changeCss();

  });

};

//更改css

const changeCss = () => {

  let levelName = document.getElementsByClassName("foo"); // levelname是上面的最底层节点的名字

  for (let i = 0; i < levelName.length; i++) {

    // cssFloat 兼容 ie6-8  styleFloat 兼容ie9及标准浏览器

    levelName[i].parentNode.style.cssFloat = "left"; // 最底层的节点，包括多选框和名字都让他左浮动

    levelName[i].parentNode.style.styleFloat = "left";

    levelName[i].parentNode.onmouseover = function () {

      this.style.backgroundColor = "#fff";

    };

  }

};
```