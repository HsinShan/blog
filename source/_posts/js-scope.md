---
title: 作用域
date: 2018-07-22 10:36:59
tags:
  - scope
categories:
  - Javascript
---

### 作用域(scope)

即變數(variable)的作用範圍

1. 全局變數: 任何頁面中的地方皆可以使用

```html
<script>
  var a = 10;
</script>
```

2. 局部變數

```html
<script>
  function test() {
    var b = 20; // 僅存在此函數中
  }
</script>
```

---

### 作用域分析

1. 預解析: 所有變數在 code 真正 run 之前，都非賦值為定義的值; 所有函數在 code 真正 run 之前，都是整個函數區塊
   ※遇到重複命名: 若 2 個皆為變數，僅留下一個; 若為變數和函數重複命名，則**留下函數** => 一般情況不會發生
2. 逐行解析: 解析表達式 + - x / =
   ※函數也是一個作用預，若全局變數和局部變數同時存在此函數中，**局部變數優先**

#### 範例一:一般情況

```javascript
var a = 1;
function fn1() {
  alert(a);
  a = 2;
}
fn1(); // alert 1
alert(a); // 2
```

**預解析**
1 `var a;`
2 `fn1 = function(){...};`

**逐行解析**
1 `a=1`
2 等調用此函數才會進行解析
6 **函數調用**(因為也是一個作用域，所以會再預解析)

- 預解析 => 無(因無定義變量或函數)
- 逐行解析
  - 3 `alert(1)`
  - 4 `a = 2`

7 `alert(2);`

#### 範例二:全局和局部變數重名

```javascript
var a = 1;
function fn2() {
  alert(a);
  var a = 2;
}
fn2(); // a = undefined
alert(a); // 1
```

**預解析**
1 `var a;`
2 `fn2 = function(){...};`

**逐行解析**
1 `a=1`
2 等調用此函數才會進行解析
6 **函數調用**(因為也是一個作用域，所以會再預解析)

- 預解析
  - 4 `var _a;` // **局部變數**
- 逐行解析
  - 3 `alert(a)`
    ※ 因變數重名，所以局部優先。但在此函數作用域中，因為是由上往下看，所以 a 變數尚未被定義，因此為 undefined
  - 4 `_a = 2`

7 `alert(1);` // alert 原先全局的變數 a，所以會 alert 1

#### 範例三:全局和局部變數(函數參數)重名

```javascript
var a = 1;
function fn3(a) {
  alert(a);
  a = 2;
}
fn1(); // a = undefined
alert(a); // 1
```

**預解析**
1 `var a;`
2 `fn3 = function(a){...};`

**逐行解析**
1 `a=1`
2 等調用此函數才會進行解析
6 **函數調用**(因為也是一個作用域，所以會再預解析)

- 預解析
  - 2 `var _a;` // **局部變數(函數的參數)**
- 逐行解析
  - 3 `alert(a)`
    ※ 因變數重名，所以局部優先。但調用此函數未給參數值，所以 a 變數未被賦值，因此為 undefined
  - 4 `_a = 2`

7 `alert(1);` // alert 原先全局的變數 a，所以會 alert 1

#### 範例四:函數和變數重名

```javascript
alert(a); // alert function a(){alert("222");}
var a = 1;
function a() {
  alert("...");
}
alert(a); // 1
var a = 3;
alert(a); // 3
function a() {
  alert("222");
}
alert(a); // 3
```

**預解析**
2 `var a;`
3 `a = function(){ alert("...")};`
7 `var a;`
9 `a = function(){ alert("222")};`

**逐行解析**
1 `alert function a(){alert("222");}` // 因為預解析過後，只留函數，所以會是預解析最後第 9 行 a 函數的結果
2 `a = 1`
6 `alert(1)`
7 `a = 3`
8 `alert(3)`
12 `alert(3)`

- 預解析
  - 2 `var _a;` // **局部變數(函數的參數)**
- 逐行解析
  - 3 `alert(a)`
    ※ 因變數重名，所以局部優先。但調用此函數未給參數值，所以 a 變數未被賦值，因此為 undefined
  - 4 `_a = 2`

7 `alert(1);` // alert 原先全局的變數 a，所以會 alert 1
