# JavaScript 编码风格指南

软件生命周期中80%的成本消耗在了维护上，因此编码风格指南对一个长期维护的软件而言是非常重要的。



### 一、ESLint

在基于vue-cli+webpack构建的项目中，引入了ESLint，一个JavaScript QA 工具，用来避免低级错误和统一的代码风格



#### 1、缩进

每一行层级由2个空格组成，可以通过配置编辑器，将tab键转换为2个空格`{"tab_size":2},    {"translate_tabs_to_spaces":true}`

```javascript
// 好的写法
if (true) {
  doSomething()
}
```



#### 2、省略分号

分析器有自动分号插入（ASI）机制，JavaScript代码省略分号也可以正常工作，结合ESLint的风格检查机制，可以有效规避意外换行导致的分号插入错误



#### 3、空格

二元运算符前后必须使用一个空格来保持表达式的整洁、操作符包括赋值运算符和逻辑运算符，比如：

```javascript
let found = (values[i] === item)
for (let i = 0; i < count.length; i++) {
  ...
}
```

当使用括号时，紧接着左括号之后和紧接着右括号之前不应该有空格，比如：

```javascript
if (null === undefined) {}
doSomething(name, title, cb)
```

函数声明需要在函数名和（）前后各一个空格，而调用函数则省略（）前的空格，比如：

```javascript
function getName (name) {
  // doSomething
}
this.getName('ross')
```



#### 4、注释

频繁的使用注释有助于他人理解你的代码，如下情况应当使用注释：

组件开头，在组件最顶部的位置，写一个多行注释，包含：组件位置、组件名、props、emit及其他需要解释的信息，如：

```javascript
/*
  客户模块-详情页
  props
  	id: 客户ID
  	form: 用来提交的表单数据
  emit
  	@close 当窗口关闭时，通知到父组件
  	@editItem 点击编辑按钮时触发，携带一个参数，为row对象
  
*/
```

函数注释：包含描述、指定所有参数和返回值的类型和值。

```javascript
/**
 * make() returns a new element
 * based on the passed in tag name
 *
 * @param {String} tag
 * @return {Element} element
 */
```



在data中声明的变量，如果和业务相关，也应当给予一个单行注释

```javascript
data () {
  return {
    commomRuleId: 1, // 审批通用设置id
    ruleList: [], // 审批列表
    currentRule: 0, // 当前选中的审批
    currentType: 0 // 当前审批类型
  }
}
```



在computed、methods、filters中的函数和方法，均要有注释(建议两个方法之间留一个空行)

```javascript
  methods: {
    
    // 审批启用状态修改
    toggleStatus (val) {
      .....
    },

    // 打开审批通用设置
    openSet () {
      .....
    },

    // 获取审批规则列表
    getRuleList () {
      let url = '/approvalApi/getRuleList.html'
      api.post(url, {}, (data) => {
        this.ruleList = data.result.ruleList
        this.commomRuleId = data.result.commomRuleId

        // 默认选中第一个
        if (this.ruleList.length) {
          let id = this.ruleList[0].id
          let type = this.ruleList[0].type
          this.openDetail(id, type)
        }
      })
    }
  }
```



#### 5、命名

命名主要遵循三种方式：

1. 驼峰式命名 (camelCase)，即首字母小写，后续单词首字母大写；
2. 帕斯卡命名 (PascalCase)，即首字母大写，后续单词首字母大写；
3. 横线分隔命名 (kebab-case)，即所有字母全部小写，单词之间用'-'隔开，主要应用在dom中。

```javascript
function Person () {}
import CommonConfig from './common-config'
let count = 10
const myName = 'Nicolas'
<common-config></common-config>
```

##### 变量和函数

变量名前缀应该是名字，而函数名前缀应该是动词，并且均应遵循驼峰式命名法，如：

```javascript
let count = 10
const myName = 'Nicolas'

function getName () {}
```

通常来讲，命名尽可能短，并抓住要点。尽量在变量中体现出值的数据类型。比如，命名count、length和size表明数据类型是数字，而name、title和message则表明数据类型是字符串。

常用的函数动词前缀有 is, has, get, set 等

##### 单文件组件文件

单文件组件命名使用横线分隔 (kebab-case)，在script中引入时，按照大驼峰式命名(PascalCase)，如下：

```javascript
import CommonConfig from './common-config'
<common-config></common-config>
```

基础组件命名 (也就是展示类的、无逻辑的或无状态的组件) 全部使用v作为特定的前缀开头：

```javascript
<v-switch></v-switch>
import VSwitch from './v-switch'
```

##### 配置文件、枚举类等全部以大写的方式命名

```javascript
/* url config */
const URL = {
    .....
}
export URL
```



#### 其他

##### 引号

统一用单引号 ' 替换双引号 "



##### 模板字符串

```javascript
let name = 'Nicolas'

// bad
let message = 'How are you, ' + name + '?'

// good
let message = `How are you, ${name}?`
```



##### 函数默认值

```javascript
// really bad
function handleThings(opts) {
  // 不！我们不应该改变函数参数。
  // 更加糟糕: 如果参数 opts 是 false 的话，它就会被设定为一个对象。
  // 但这样的写法会造成一些 Bugs。
  //（译注：例如当 opts 被赋值为空字符串，opts 仍然会被下一行代码设定为一个空对象。）
  opts = opts || {}
  // ...
}

// still bad
function handleThings(opts) {
  if (opts === void 0) {
    opts = {}
  }
  // ...
}

// good
function handleThings(opts = {}) {
  // ...
}
```



