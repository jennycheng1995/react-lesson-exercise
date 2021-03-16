# React

## Chapter 1. 簡介

### Unit 1. 特色
* **非作為 MVC (Model-View-Controll) 框架**
專注在==View==上面，以==組件化==方式，讓開發者建構使用者介面，可重複使用，呈現資料與反應資料改變。

* **不使用 Templates**
使用==javascript==語法來建構render函式，增加可維護性。
![](https://i.imgur.com/DbqMlVp.png)



* **不做資料綁定**
React使用==單向資料流==，資料變動時會將組件重新render一次，render成Virtual DOM後，在與真實的DOM做比對，只更新最少最必要的元素。
![](https://i.imgur.com/ryuzgmO.png)
與Browser脫鉤，成為可用在前後端、App等的開發框架。
![](https://i.imgur.com/vynIwp9.png)

* **以組件為單位**
組件為一個有狀態(props)、屬性(state)、生命週期跟自訂方法的一個單位。
透過組件的組合及重複使用，建構更可維護的應用程式。


### Unit 2. 思維
####  2-1. jQuery 與 React 比較
* **jQuery**
思維：對元素直接操作
缺點：程式與元素結構嚴重互相綁定:-1: 

* **React**
思維：==聲明式==(Declarative)，==單向資料流==(One-way data flow)
特點：
1.在修改資料時，不直接修改DOM元素，而是由React為我們更新視覺元素。
2.封裝原則，其他組件無法存取該組件內容，不會因改動造成其他地方發生問題。


### Unit 3. 三大框架比較

![](https://i.imgur.com/y98bWkU.png)

![](https://i.imgur.com/sU3vTPr.png)


### Unit 4. 虛擬組件樹 Virtual DOM
#### 4-1. render function
使用model，透過組件結構render成實際DOM結構。
![](https://i.imgur.com/8fpFwIB.png)
資料變更流程：
![](https://i.imgur.com/juHxD7w.png)
Virtual DOM(memory)會全部重建在與Real DOM去比對，在Real DOM只更新變動元素。
更新畫面最耗效能就是Real DOM的更新。

#### 4-2. Virtual DOM與MVVM比較

* **Virtual DOM**
初始render快
大量更新快
容易時做DOM以外的render

* **MVVM**
小量更新快
要做若干優化，大量更新才快

---

## Chapter 2. ES6與npm

### Unit 1. 取代 var 的 let 與 const
```javascript=1
//can re-assign
let age = 24
age += 1
age = 28

//cannot re-assign
const fingers = 10
fingers *= 2
fingers = 9 

const point ={ x: 1, y: 2 }
point.x = 3             //can change object
point = { x: 2, y: 3 }  //cannot re-assign
```

#### 1-1. var, let, const 的區別

var 作用範圍： block
let/const 作用範圍： scope

* **scope(作用域)**：
1.function scope/ global scope
2.由外而內繼承進去
```javascript=1
var x = 1;
function f(){
    console.log(x);
}
f();
```
:::warning
**result：**
1
:::

```javascript=1
var x = 1;
function f(){
    var x = 2;
    console.log(x);
}
f();
console.log(x);
```
:::warning
**result：**
2
1
:::
* **block：**
1.由外而內繼承進去
```javascript=1
var x = 1;
{
   var x = 2;
   console.log(x);
}
console.log(x);
```
:::warning
**result：**
2
2
:::
```javascript=1
let x = 1;
{
   let x = 2;
   console.log(x);
}
console.log(x);
```
:::warning
**result：**
2
1
:::

### Unit 2. 箭頭函式 arrow functions

#### 2-1. Javascript ES6 函式寫法
```javascript=1
const double = (x) => {
    return x * 2
}
```
```javascript=1
const double = x => return x * 2
```
#### 2-2. this

1. 一般函式

* 直接執行： Window
```javascript=1
function jump(){
    console.log(this);
}
jump();
```
:::warning
**result：**
Window
:::
* 做為物件執行： 該物件
```javascript=1
function jump(){
    console.log(this);
}

const a = {};
a.jump = jump;
a.jump();
```
:::warning
**result：**
{jump: f}
:::
* 做為DOM偵聽函式執行： 該DOM
```htmlembedded=1
<button id="btn">btn</button>
```
```javascript=1
function jump(){
    console.log(this);
}
btn.addEventListener('click', jump);
```
:::warning
**result：**
<button id="btn">btn</button>
:::

2. 箭頭函式
沒有自己的context，內部的this就是外部this。

* 直接執行： Window
```javascript=1
const jump = () => {
    console.log(this);
}
jump();
```
:::warning
**result：**
Window
:::
* 做為物件執行： Window
```javascript=1
const jump = () => {
    console.log(this);
}

const a = {};
a.jump = jump;
a.jump();
```
:::warning
**result：**
Window
:::
* 做為DOM偵聽函式執行： Window
```htmlembedded=1
<button id="btn">btn</button>
```
```javascript=1
const jump = () => {
    console.log(this);
}
btn.addEventListener('click', jump);
```
:::warning
**result：**
Window
:::


### Unit 3. import 與 export

==模組化==方式管理程式碼，方便維護協作與測試。

ES6 import與export可做模組化匯入匯出，如下範例：

{%gist 696dba62f818000d02ba159f10d83140%}
{%gist df624f0b18b03264bb956e1b7f597c1b%}

:::info
**ES6基礎環境建置：** https://hackmd.io/@HHmu66jCTFKTFu4dRnPpVw/r1oZzwqm_
:::

### Unit 4. 窺探物件導向：class

#### 4-1. 建立class

如模板一樣，可製作出行為和屬性相似的物件。

{%gist 12f621fef26fe0f47ac3bc081e42d007%}

age: 屬性

bark: 方法

Animal: 父類別

Dog: 子類別

extends代表該==子類別要繼承的父類別的屬性與方法==。

ES6版本的class只能定義方法，必須在建構函式(Constructor)定義屬性。
:::info
**Remarks：** 若使用babel class-properties plugin可使用上方簡寫方式。
:::

### Unit 5. Node.js, npm 與 webpack

#### 5-1. 使用npm安裝package：

**STEP 1. 安裝node.js (若已安裝略過此步驟)**

**STEP 2. 在終端機輸入 ==npm install -s 套件名稱==**

:::info
**Remarks：** 

可使用npm安裝的程式可稱為package。

npm會將package安裝至node_modules的資料夾內，並在package.json記錄安裝的package。
:::

#### 5-2. webpack：

開源的前端打包工具，是在node.js環境底下運行的程式，可將各模組組合起來轉換成瀏覽器可執行的語法。

:::info
**Remarks：** 

安裝webpack

==npm install -s webpack==
:::

### Unit 6. Create React App

**STEP 1. 安裝create-react-app package**

輸入 ==npm install --global create-react-app==

![](https://i.imgur.com/kIrBfVA.png)

**STEP 2. 建立react開發模板**

輸入 ==create-react-app 專案名稱==

![](https://i.imgur.com/18LU5zs.png)

**STEP 3. 執行app**

輸入 ==npm start==

![](https://i.imgur.com/fX8uFpS.png)


**補充：程式碼打包**

輸入 ==npm run build==

程式碼會打包好至build目錄底下，此目錄即可發佈。

![](https://i.imgur.com/2SLYaIo.png)

