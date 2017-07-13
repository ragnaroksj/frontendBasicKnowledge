# frontendBasicKnowledge

HTML:
1. <!DOCTYPE> 作用：indicate which html version should be used to render the page in the browser.
Html 5 : <!DOCTYPE html>
Html 4.01 Transitional <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
Html 4.01 Frameset <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN"  "http://www.w3.org/TR/html4/frameset.dtd">
XHTML 1.0 Strict <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
XHTML 1.0 Transitional <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
XHTML 1.0 Frameset <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
XHTML 1.1 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
如果没有 Doctype:
use quirks mode to render page
the use of a doctype means that you can rely (for the most part) on your page rendering the same in every browser, making development significantly easier

2. What's the difference between an "attribute" and a "property”?
Attributes are defined by HTML. Properties are defined by DOM.
attributes do not change and always carry initial (default) values. However, HTML properties can change,

3. cookie:  session cookies / persistent cookie & localstorage / sessionstorage
cookie:
Session cookies - these are temporary cookie files, which are erased when you close your browser. When you restart your browser and go back to the site that created the cookie, the website will not recognize you. You will have to log back in (if login is required) or select your preferences/themes again if the site uses these features. A new session cookie will be generated, which will store your browsing information and will be active until you leave the site and close your browser. More on session cookies.

Persistent cookies – these files stay in one of your browser's subfolders until you delete them manually or your browser deletes them based on the duration period contained within the persistent cookie's file

Create a Cookie with JavaScript
 document.cookie="username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC";
 document.cookie="username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC; path=/";

 Read a Cookie with JavaScript
 var x = document.cookie;
 Delete a Cookie with JavaScript

Deleting a cookie is very simple. Just set the expires parameter to a passed date:
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC";
http://www.w3schools.com/js/js_cookies.asp


Localstorage & sessionstorage
Local storage is more secure, and large amounts of data can be stored locally, without affecting website performance. 
Unlike cookies, the storage limit is far larger (at least 5MB) and information is never transferred to the server.
The only difference is that, while data stored in localStorage has no expiration time, data stored in sessionStorage gets cleared when the browsing session ends—that is, when the browser is closed
localStorage.setItem("username","John");
localStroage.getItme("username");
removeItem
cookies only allow you to store strings. sessionStorage and localStorage allow you to store JavaScript primitives but not Objects or Arrays (it is possible to JSON serialise them to store them using the APIs)

4. http 原理：从输入URL到页面加载发生了什么
https://segmentfault.com/a/1190000006879700
1. DNS lookup: translate domain name to ip, look up in local server -> root server -> com server, saved in dns cache, dns load balance
2. TCP connection: Http uses TCP for tranform layer protocol. Http is not safe, use https(http+ssl)
3. Http Request:
    3.1 request line: Method(GET, POST, PUT, DELETE...) Request-URL HTTP-version CRLF
        3.1.1 Post and Get:
            Get means get resource, limit by browser or server, sent with URL. example: get data
            Post means update data, unlimited, sent in request content. example: send twitter, send password
    3.2 request headers: allow client send extra information(accept, authorization, cookie) to the server.
    3.3 request content: using post,put to pass data to server and those data is saved in request content.
4.Http Response: Server process the request and return response.
    4.1 status code
        4.1.1 301(Moved Permanently) and 302(move temporarly)
        4.1.2 HTTP cache
    4.2 response header: server, connection
    4.3 response content: html, css, javascript, images
5. Browser render page: analyze html and build DOM tree and then analyze css render tree. 
    Reflow: DOM calculate elemtns size and position first and then Repaint.
    js: single thread, synchrounous and async. runtime: main thread(同步任务) + task queue（异步任务）， 异步任务有了结果放置一个event等待被提取，event loop
6. close TCP connect


CSS:
1. px,em.rem, vh(vw):
PX: pixel, accurate but cannot scale
em: size by parent element
rem: size by root(html) element
vh(vw): viewpoint, 100vw = 100% of width of viewpoint

2. The box model
box-sizing:
border-box: width = border + padding + content width
content-box width = content width

3. inline vs block
Block:
- If no width is set, will expand naturally to fill its parent container
- Can have margins and/or padding
- If no height is set, will expand naturally to fit its child elements (assuming they are not floated or positioned)
- By default, will be placed below previous elements in the markup (assuming no floats or positioning on surrounding elements)
- Ignores the vertical-align property

Inline:
- Flows along with text content, thus
- Will not clear previous content to drop to the next line like block elements
- Is subject to white-space settings in CSS
- Will ignore top and bottom margin settings, but will apply left and right margins, and any padding
- Will ignore the width and height properties
- If floated left or right, will automatically become a block-level element, subject to all block characteristics
- Is subject to the vertical-align property

4. Position:
static(default): it is laid out in its current position in the flow.  The top, right, bottom, left and z-index properties do not apply.
relative: lays out all elements as though the element were not positioned, and then adjust the element's position, without changing layout (and thus leaving a gap for the element where it would have been had it not been positioned). The effect of position:relative on table-*-group, table-row, table-column, table-cell, and table-caption elements is undefined.
absolute: Do not leave space for the element. Instead, position it at a specified position relative to its closest positioned ancestor or to the containing block. Absolutely positioned boxes can have margins, they do not collapse with any other margins.
fixed: Do not leave space for the element. Instead, position it at a specified position relative to the screen's viewport and don't move it when scrolled. When printing, position it at that fixed position on every page. This value always create a new stacking context. 

5. Margin Collapse:
相邻元素（父子或兄弟元素）在普通流（非float,absolute）的 块元素垂直方向上的margin会发生叠加，取相邻margin max的值
何为毗邻：是指没有被非空内容、padding、border 或 clear 分隔开。
何为普通流：除浮动（ float ）、绝对定位（ absolute ）外的代码即为普通流。
https://codepen.io/andrewgrant/post/css-margin-collapsing-explained
http://geekplux.com/2014/03/14/collapsing_margins.html

6. css flex
items will be laid out following either the main axis (from main-start to main-end) or the cross axis (from cross-start to cross-end)

Container:
display: flex/inline-flex;
flex-direction: row | row-reverse | column | column-reverse
flex-wrap: nowrap | wrap | wrap-reverse
flex-flow: shorthand flex-direction and flex-wrap properties,
justify-content: flex-start | flex-end | center | space-between |space-around
align-items: stretch | flex-start | flex-end | center | baseline
align-content: strecth | flex-start | flex-end | center | space-between | space-around 

items:
order: <integer>
flex-grow: <number>
flex-shrink: <number>
flex-basis: <length> | auto
flex: flex-grow flexshrink flex-basis
align-self: auto | flex-atart | flex-end | center | baseline | strentch;
http://www.ruanyifeng.com/blog/2015/07/flex-examples.html

7. css sibling selector
<div>
  <p>Line one</p>
  <p>Line two</p>
  <div>Box</div>
  <p>Line Three</p>
</div>

p + p{
	color: red; // Line two
}

p ~ p{
	color: red; // Line two and Line Three
}

p:nth-of-type(3) {
    color: red; // Line three 
}

p:nth-child(3) {
    color: red; // Nothing selected
}

8. CSS - Resize:
none|both|horizontal|vertical|initial|inherit;
The resize property specifies whether or not an element is resizable by the user.

Javascript:
1. Closue:
必包的概念就是子函数在父函数执行完毕后依旧能调用父函数的变量，其实就是变量不被释放而已，应该是堆的形式分配内存。
A closure is an inner function that has access to the outer (enclosing) function's variables—scope chain. The closure has three scope chains: it has access to its own scope (variables defined between its curly brackets), it has access to the outer function's variables, and it has access to the global variables.

Closures are functions that refer to independent (free) variables (variables that are used locally, but defined in an enclosing scope). In other words, these functions 'remember' the environment in which they were created.

Example:
// f2 is coluse: can read f1 variable.
function f1(){
    var n=999;
    function f2(){
        alert(n); 
　　 }
　　 return f2;
}
　　
var result=f1();
result(); // 999


function addClick(){
    for(var i = 0; i<3 ; i++)
     document.getElementBy(item[i]).click = function(){
          console.log(i); //i always outputs 3
     }
}
click is a closure. And any variable is used in click will use the latest one

function addClick(){
     for(var i = 0; i<3 ; i++)
     document.getElementBy(item[i]).click = clickFunction(i);
}

function clickFunction(i){
     return function(){
          console.log(i);
     }
}

2. immediately-invoked funciton express(iife)
the grouping operator needs to contain an expression.
function foo(){ /* code */ }(); // SyntaxError: Unexpected token )
(function foo(){}());

3. What is the difference between event bubbling and event capture?
from inner Element to outside, from outside to inner Element

4. Explain “hoisting”
Hoisting is the act of moving the declarations to the top of the function.

5. defer and async
<script>: block html downloading and downlad script and run 
<script async>: download js during html downloading and run when it has finished(pause html parser)
<script defer>: download js and execute after html,js -all are downloaded

6. This :
The value of this is determined by how a function is called. It can't be set by assignment during execution, and it may be different each time the function is called.

7. undeclared, undefined, null
var x //x is undefined;
var y = null // y is null but defined;
console.log(z); //z is undeclared

use typeof to check:
typeof undefined // undefined
typeof null //object ,bug should be null
check undeclared:
if( typeof foo !== “undefined”){
}

8. What's the difference between host objects and native objects?
Native objects are defined in this specification in ECMAscript.(Object (constructor), Date, Math, parseInt, eval, string methods like indexOf and replace, array methods, ...)
Host objects are supplied by the host environment to complete the execution environment of ECMAScript.
Assuming browser environment): window, document, location, history, XMLHttpRequest, setTimeout, getElementsByTagName, querySelectorAll, ...

9.Difference between: function Person(){}, var person = function(){}, and var person = new Person()?
The first one and second define a function(or class) and the third one create an instance
The first one is to declare a function and the second one is to create an anonymous function

10. call, apply, bind
The call() method calls a function with a given this value and arguments provided individually.
The bind() method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.
fn.function1.call(thisObj, param1, param2)
fn.function1.apply(this.Obj, paramArray)
Function.prototype.bind = function(ctx) {
    var fn = this;
    return function() {
        fn.apply(ctx, arguments);
    };
};

Call and apply will execute the function immediately, whereas bind returns a function that when later executed will have the correct context set for calling the original function. This way you can maintain context in async callbacks, and events.

11. Ternary: ? : = if else

12. JS primitive:
String, Number, boolean, symbol

13. Explain how JSONP works (and how it's not really AJAX)
JSONP requests insert a <script> tag , whose source is set to the target URL, into to the DOM (normally the <head>).
not use xmlhttprequest
get only

14. ajax:
var xmlhttp = new XMLHttpRequest();
xmlhttp.onreadystatechange = function(){
    if( xmlhttp.readyState == 4 && xmlhttp.status === 200 ){
        // xmlhttp.responseText
    }
}
xmlhttp.open("GET","ajax_info");
xmlhttp.send();

open(method,url,async)
method: the type of request: GET or POST
url: the server (file) location
async: true (asynchronous) or false (synchronous)

15. Explain the same-origin policy with regards to JavaScript
Two pages have the same origin if the protocol, port (if one is specified), and host are the same for both pages.

16. the Deferred object provides a way to register multiple callbacks into self-managed callback queues, invoke callback queues as appropriate, and relay the success or failure state of any synchronous or asynchronous function.

17 JSON obj -> string JSON.stringify(jsonObj);
string -> JSON obj  JSON.parse(jsonObjString);

Performance Improvement:
1. Specify ways to optimize a web page to load faster
1. Optimize Image Size and Format : progressive , different size image for different device
2. optimize dependencies:  plugins/ tracking scripts/ cms software
3. avoid inline js and css files
4. optimize caching: CDN
5. avoid render blocking scripts: Place javascript files at the end of the body or use the 'async' attribute to load them asynchronously.
6. avoid redirects: check broken link
7. set up g-zip encoding
8. reduce http requests: css sprites
9. minify the js and css
10. reduce cookie size

18. What is "use strict";? what are the advantages and disadvantages to using it?
Strict mode helps out in a couple ways:
- It catches some common coding bloopers, throwing exceptions.
- It prevents, or throws errors, when relatively "unsafe" actions are taken (such as gaining access to the global object).
- It disables features that are confusing or poorly thought out.
- Prevents accidental globals. Without strict mode, assigning a value to an undeclared variable automatically creates a global variable with that name. This is one of the most common errors in JavaScript. In strict mode, attempting to do so throws an error.
- Eliminates this coercion. Without strict mode, a reference to a this value of null or undefined is automatically coerced to the global. This can cause many headfakes and pull-out-your-hair kind of bugs. In strict mode, referencing  a 'this' value of null or undefined throws an error.

19. What is the difference between .get(), [], and .eq()?
get() returns the DOM element matched by the selector.
eq() returns the jQuery Object eq().get(0) = get()
[] returns the Dom element = get()

20. What is the difference between $ and $.fn? Or just what is $.fn.
$ = function(){}
$.fn = $.prototype = {};

21. Window.onload和$(document).ready()
window.onload: execute code after all resouces are loaded, 一次只能保存对一个函数的引用，多次绑定函数只会覆盖前面的函数。
$(document).ready(): excute code after DOM is loaded, 多次使用而注册不同的事件处理程序

22. Prototype & inheritance
All objects in JavaScript inherit properties and methods from Object.prototype. These inherited properties and methods are constructor, hasOwnProperty (), isPrototypeOf (), propertyIsEnumerable (), toLocaleString (), toString (), and valueOf (). ECMAScript 5 also adds 4 accessor methods to Object.prototype.
Prototype: Each object has an internal property called prototype, which links to another object
function inherit(o){
function F(){};
F.prototype = o;
return new F(); 
}

function extend(child, parent){
child.prototype = inherit(parent.prototype);
child.prototype.constructor = child;
child.parent = parent.prototype;
}


call superclass constructor and also call a parent method after overriding
superObject.apply(this, arguments);
superObjet.prototype.xyz.apply(this, arguments)

继承lastest Version;
function Base(baseVar){
this.baseVar = baseVar;
}

Base.prototype.say = function(){
alert(this.baseVar);
}

function Child(childVar, childVar2){
Base.call(this,childVar);
this.childVar2 = childVar2;
}

Child.prototype = Object.create(Base.prototype);
Child.prototype.constructor = Child;



Pseudo-classical pattern
// --------- the base object ------------
function Animal(name) {
this.name = name
}

// methods
Animal.prototype.run = function() {
alert(this + " is running!")
}

Animal.prototype.toString = function() {
return this.name
}


// --------- the child object -----------
function Rabbit(name) {
Rabbit.parent.constructor.apply(this, arguments)
}

// inherit
extend(Rabbit, Animal)

// override
Rabbit.prototype.run = function() {
Rabbit.parent.run.apply(this)
alert(this + " bounces high into the sky!")
}

var rabbit = new Rabbit('Jumper')
rabbit.run()


All in one:
function Animal(name) {
this.name = name
this.run = function() {
alert("running "+this.name)
}
}

var animal = new Animal('Foxie')
animal.run()

function Rabbit(name) {
var rabbit = Animal(name)

var parentRun = rabbit.run

rabbit.jump = function() {
alert(name + " jumped!")
}

rabbit.run = function() {
parentRun.call(this)
alert("fast")
}

return rabbit
}

rabbit = Rabbit("rab")

Factory constructor pattern
function Animal(name) {
return {
run: function() {
alert(name + " is running!")
}
}
}

function Rabbit(name) {
Animal.apply(this, arguments)

var parentRun = this.run

this.jump = function() {
alert(name + " jumped!")
}

this.run = function() {
parentRun.call(this)
alert("fast")
}
}

rabbit = new Rabbit("rab")

Extend:
$(...).clone() just copy dom element
/ Shallow copy
var newObject = jQuery.extend({}, oldObject);

// Deep copy
var newObject = jQuery.extend(true, {}, oldObject);

http://geniuscarrier.com/copy-object-in-javascript/

带构造函数的继承
function extend(Child, Parent) {
var F = function () { };
F.prototype = Parent.prototype;
Child.prototype = new F();
Child.prototype.constructor = Child;
Child.uber = Parent.prototype;
}


不待构造函数的继承
function deepCopy(p, c) {
var c = c || {};
for (var i in p) {
if (typeof p[i] === 'object') {
c[i] = (p[i].constructor === Array) ? [] : {};
deepCopy(p[i], c[i]);
} else {
c[i] = p[i];
}
}
return c;
}

23. What is a potential pitfall with using typeof bar === "object" to determine if bar is an object? How can this pitfall be avoided?
if bar is null, it will return true;
if bar is [], it will return true;
if bar is undefined, typeof bar is undefined;

24. What is the significance of, and reason for, wrapping the entire content of a JavaScript source file in a function block?
creates a closure around the entire contents of the file which, perhaps most importantly, creates a private namespace and thereby helps avoid potential name clashes between different JavaScript modules and libraries.

Another feature of this technique is to allow for an easily referenceable (presumably shorter) alias for a global variable.

25.Ajax跨域问题
不同的domian无法通过ajax来传递值
jsonp
——————— http://b.com/index ———————-

<script src="jquery-1.4.2.js" type="text/javascript"]] > </script>
<script type="text/javascript">
function fun1()
{
$.getJSON("http://a.com/c.php?no=10&msg=ok&format=json&jsoncallback=?",
function(data){
alert(data.msg);
});
}
</script>
<button type="button" onclick="fun1()">跨域处理</button>

——————– http://a.com/c.php ———————-

<?php
$no = $_GET['no'];
$msg = $_GET['msg'];
$json = json_encode(array('no'=>$no,'msg'=>$msg));
//必需以下这样输出
echo $_GET['jsoncallback'].'('.$json.')';






Coding Challenge:
1. Make this work:
[1,2,3,4,5].duplicate(); // [1,2,3,4,5,1,2,3,4,5]
Array.prototype.duplicate = function( ){
    return this.concat(this);
}

2. What will the code below output to the console and why?

(function(){
  var a = b = 3;
})();

console.log("a defined? " + (typeof a !== 'undefined')); //false
console.log("b defined? " + (typeof b !== 'undefined')); //true

var a = b = 3 相当于：
var a = b;
b =3;
所以 b是全局变量，a是局部变量

3. Consider the two functions below. Will they both return the same thing? Why or why not?

function foo1()
{
  return {
      bar: "hello"
  };
}
//return object:{ bar: "hello"};

function foo2()
{
  return
  {
      bar: "hello"
  };
}
//return undefined;
foo2 相当于 return; { bar: "hello" };

4. What will the code below output? Explain your answer.

console.log(0.1 + 0.2);
console.log(0.1 + 0.2 == 0.3);

You can’t be sure. it might print out “0.3” and “true”, or it might not. 

5. var arr1 = "john".split(''); // arr1: [j,o,h,n];
var arr2 = arr1.reverse(); // arr2: arr1, arr1: [n,h,o,j];
var arr3 = "jones".split('');
arr2.push(arr3); // arr2: arr1, arr1: [n,h,o,j,[j,o,n,e,s]]
console.log("array 1: length=" + arr1.length + " last=" + arr1.slice(-1));
console.log("array 2: length=" + arr2.length + " last=" + arr2.slice(-1));

6. console.log(1 +  "2" + "2"); //"122"
console.log(1 +  +"2" + "2"); //"32"
console.log(1 +  -"1" + "2"); // "02"
console.log(+"1" +  "1" + "2"); // "112"
console.log( "A" - "B" + "2"); // "NaN2"
console.log( "A" - "B" + 2); // "NaN"

7. What is the output out of the following code? Explain your answer.

var a={},
    b={key:'b'},
    c={key:'c'};

a[b]=123;
a[c]=456;

console.log(a[b]);

The output of this code will be 456 (not 123).

The reason for this is as follows: When setting an object property, JavaScript will implicitly stringify the parameter value. In this case, since b and c are both objects, they will both be converted to "[object Object]". As a result, a[b] anda[c] are both equivalent to a["[object Object]"] and can be used interchangeably. Therefore, setting or referencing a[c] is precisely the same as setting or referencing a[b].

8. iPhone 格式布局
<div class="screen">  
<div class="app-icon">
<span>center</span>
</div>
<div class="app-icon"></div>
<div class="app-icon"></div>
<div class="app-icon"></div>
<div class="app-icon"></div>
<div class="app-icon"></div>
<div class="app-icon"></div>
</div>

.app-icon {
border-radius: 15%;
float: left;
width: 20%;
height: 0px;
padding-top: 20%;
display: block;
background: #000;
margin-left: 4%;
margin-top: 4%;
position: relative;
}

or

.app-icon{
width: 20vw;
height: 20vw;
}

.screen{
width: 100%;
}

span {
position: absolute;
top: 0;
left: 0;
color: red;
}


second way:
html:
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width">
<title>JS Bin</title>
</head>
<body>
<div class="iphone-container">
<div class="item"><div>a</div></div>
<div class="item"><div>a</div></div>
<div class="item"><div>a</div></div>
<div class="item"><div>a</div></div>
<div class="item"><div>a</div></div>
<div class="item"><div>a</div></div>
<div class="item"><div>a</div></div>
<div class="item"><div>a</div></div>
<div class="item"><div>a</div></div>
</div>
</body>
</html>

css:
.iphone-container {
width: 100vw;
height:100vh;
margin: 0 auto;
}

.item {
width: 25vw;
float: left;
border: 1px solid #ccc;
box-sizing: border-box;
text-align: center;
background-image: url('https://lh4.ggpht.com/wKrDLLmmxjfRG2-E-k5L5BUuHWpCOe4lWRF7oVs1Gzdn5e5yvr8fj-ORTlBF43U47yI=w300-rw');
background-size: cover;
margin: 10px;
position: relative;
}

.item div {
position: absolute;
top: 50%;
left: 50%
}

.item:before {
display: block;
content: "";
padding-top: 100%;
}

div:nth-child(1) {
background-color: green;
border-color:#000;
border-width:5px;
border-style: solid;
}

9. 2-column, left sidebar
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width">
<title>JS Bin</title>
</head>
<body>
<div class="container">
<div class="sidebar-left">left sidebar</div>
<div class="content">content</div>
</div>
</body>
</html>

.container {
width: 50%;
border: 1px solid #000;
}

.sidebar-left {
width: 50px;
height: 100vh;
float: left;
background: #fff;
}

.content {
background: #ccc;
height: 100vh;
}

10. 3-column, content responsive
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width">
<title>JS Bin</title>
</head>
<body>
<div class="container">
<div class="sidebar-left">left sidebar</div>
<div class="content">content dskd fejfe fef feffjf ejfjfj</div>
<div class="sidebar-right">right sidebar</div>
</div>
</body>
</html>

.container {
width: 80%;
border: 1px solid #000;
position: relative;
overflow: auto;
}

.sidebar-left {
width: 50px;
height: 100vh;
position: absolute;
background: #fff;
left: 0;
}

.content {
background: #ccc;
height: 100vh;
float: left;
padding-left:60px;
padding-right:60px;
}

.sidebar-right {
position: absolute;
right: 0;
height:100vh;
width: 50px;
background: red;
}

10. css 实现dropdown menu:
<nav>
<ul>
<li>
<a href="#">Main Menu 1</a>
<ul class="sub-menu">
<li>sub menu 1</li>
<li>sub menu 2</li>
</ul>
</li>
<li >
<a href="#">Main Menu 2</a>
<ul class="sub-menu">
<li>sub menu 1</li>
<li>sub menu 2</li>
</ul>
</li>
</ul>
</nav>


li{
display: inline-block;
position: relative;
height: 30px;
width: 100px;
}

.sub-menu{
display: none;
position: absolute;
top: 30px;
left: 0;
padding: 20px;
background:rgba(0,0,0,0.8);
}

li:hover .sub-menu{
display: block;
}

11. stick footer bottom 5 ways:
s1. 
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width">
<title>JS Bin</title>
<style id="jsbin-css">
html, body {
height: 100%;
margin: 0;
}

.wrapper {
min-height: 100%;
width: 100%;
background-color: #ccc;
margin-bottom: -60px;
}

.wrapper:after {
display: block;
content: '';
height: 60px;
}

.footer {
width: 100%;
background: #aaa;
height:60px;
}


</style>
</head>
<body>
<div class="wrapper">
content
</div>
<div class="footer">footer</div>

s2.
body {
margin: 0;
}

.header {
width: 100%;
background: #ccc;
height: 50px;
position: relative;
}

.content {
width: 100%;
background: red;
min-height: 100vh;
margin-bottom: -50px;
padding-top: 50px;
box-sizing: border-box;
margin-top: -50px;
padding-bottom: 50px;
}

.footer {
width: 100%;
background: #aaa;
height:50px;
}


</style>
</head>
<body>
<div class="header">header</div>
<div class="content">
The big problem with the above three techniques is that they require fixed height footers. Fixed heights are generally a bummer in web design. Content can change. Things are flexible. Fixed heights are usually red flag territory. Using flexbox for a sticky footer not only doesn't require any extra elements, but allows for a variable height footer.
<br />
Notice the 70px in the calc() vs. the 50px fixed height of the footer. That's making an assumption. An assumption that the last item in the content has a bottom margin of 20px. It's that bottom margin plus the height of the footer that need to be added together to subtract from the viewport height. And yeah, we're using viewport units here as another little trick to avoid having to set 100% body height before you can set 100% wrapper height.
</div>
<div class="footer">footer</div>
</body>

s3.
<style id="jsbin-css">
html {
height: 100%;
}

.header {
width: 100%;
background: #ccc;
height: 50px;
position: relative;
}

body {
min-height: 100%;
display: flex;
flex-direction: column;
margin: 0;
}

.content {
flex: 1;
}

.footer {
width: 100%;
background: #aaa;
min-height:50px;
}


</style>
</head>
<body>
<div class="header">header</div>
<div class="content">
The big problem with the above three techniques is that they require fixed height footers. Fixed heights are generally a bummer in web design. Content can change. Things are flexible. Fixed heights are usually red flag territory. Using flexbox for a sticky footer not only doesn't require any extra elements, but allows for a variable height footer.
<br />
Notice the 70px in the calc() vs. the 50px fixed height of the footer. That's making an assumption. An assumption that the last item in the content has a bottom margin of 20px. It's that bottom margin plus the height of the footer that need to be added together to subtract from the viewport height. And yeah, we're using viewport units here as another little trick to avoid having to set 100% body height before you can set 100% wrapper height.
</div>
<div class="footer">footer</div>
</body>

s4*. grid


12. Discuss possible ways to write a function isInteger(x) that determines if x is an integer.

Number.prototype.isInteger = function(x){
return (x^0) === x; 
}

Number.prototype.isInteger = function(x){
return Math.round(x) === x;
}

13.Write a sum method which will work properly when invoked using either syntax below.

console.log(sum(2,3));   // Outputs 5
console.log(sum(2)(3));  // Outputs 5

function sum(x){
if( arguments.length === 2 ) return arguments[0] + arguments[1];
else{
return function(y){
return x + y;
}
}
}

14. The following recursive code will cause a stack overflow if the array list is too large. How can you fix this and still retain the recursive pattern?

var list = readHugeList();

var nextListItem = function() {
var item = list.pop();

if (item) {
// process the list item...
nextListItem();

}
};

//solution:
setTimeout( nextListItem, 0);
The stack overflow is eliminated because the event loop handles the recursion, not the call stack. When nextListItem runs, if item is not null, the timeout function (nextListItem) is pushed to the event queue and the function exits, thereby leaving the call stack clear. When the event queue runs its timed-out event, the next item is processed and a timer is set to again invoke nextListItem. Accordingly, the method is processed from start to finish without a direct recursive call, so the call stack remains clear, regardless of the number of iterations.


15. What will be the output of the following code:

for (var i = 0; i < 5; i++) {
setTimeout(function() { console.log(i); }, i * 1000 );
}

Explain your answer. How could the use of closures help here?


for (var i = 0; i < 5; i++) {
(function(i){
setTimeout(function() { console.log(i); }, i * 1000 );
}(i));
}

16. The code will output the following four lines:
1 && 2 //2
评估1 true then 评估2 true, && 返回表达式（2）；

17. What will the following code output to the console and why:

var hero = {
_name: 'John Doe',
getSecretIdentity: function (){
return this._name;
}
};

var stoleSecretIdentity = hero.getSecretIdentity;

console.log(stoleSecretIdentity()); //undefined
console.log(hero.getSecretIdentity()); // John Doe

What is the issue with this code and how can it be fixed.
fix:
var stoleSecretIdentity = stoleSecretIdentity.bind(hero);


18. Create a function that, given a DOM Element on the page, will visit the element itself and all of its descendents (not just its immediate children). For each element visited, the function should pass that element to a provided callback function.

The arguments to the function should be:

a DOM element
a callback function (that takes a DOM element as its argument)


function traverse(element,callback){
callback(element);
var childElement = element.children;
for( var i = 0; i < childElement.lenght; i++ ){
traverse(childElement[i], callback);
}
}



<a href="#">
Checkout
</a>

a {
border-radius: 6px;
box-shadow: 1px 1px 5px -3px #555;
color: rgb(85, 85, 85);
display: block;
font-family: arial;
font-weight: bold;
height: 50px;
line-height: 50px;
margin: 50px;
padding-top: 0;
position: relative;
text-align: center;
text-decoration: none;
text-transform: uppercase;
width: 200px;
}

a:before, a:after {
border-radius: 12px;
bottom: 1px;
content: " ";
display: block;
position: absolute;
z-index: -1;
}

a:before {
background: none repeat scroll 0 0 #fff;
border: 2px solid rgb(85, 85, 85);
box-shadow: 1px 1px 3px 2px #ccc;
height: 64px;
width: 218px;
left: -14px;
top: -7px;
}

a:after {
background: linear-gradient(to bottom, #dddddd 0%, #dddddd 44%, #adadad 69%, #adadad 100%) repeat scroll 0 0 rgba(0, 0, 0, 0);
border: 6px solid #ccc;
color: #666;
content: "\2605 \2605";
font-size: 25px;
height: 47px;
left: -7px;
letter-spacing: 94px;
line-height: 39px;
padding-left: 40px;
text-align: left;
top: -3px;
width: 155px;
text-indent : -3px;
}


请写一个简单的幻灯效果页面


- 如果不使用JS来完成，可以加分。

<DOCTYPE HTML>
<html>
<head></head>
<style>
@keyframes slide{
0%{
opacity : 0;
}
10%{
opacity : 1;
}
50%{
opacity : 1;
}
60%{
opacity : 0;
}
100%{
opacity : 0;
}
}

div{
position : relative;
width:400px;
height:300px;
overflow:  hidden;
}
img{
position: absolute;
left : 0px ;
top : 0px;
opacity : 0;
animation-name : slide;
animation-duration : 10s;
animation-iteration-count : infinite;
}
img:first-child{
animation-delay : 0s;
z-index : 999;
}
img:nth-child(2){
animation-delay : 5s;
z-index : 99;
}

</style>
<body>
<div>
<img width="400" src="1.jpg" />
<img width="400" src="2.jpg" />
</div>
</body>
</html>

<DOCTYPE HTML>
<html>
<head></head>
<style>

div{
width : 400px;
height : 300px;
overflow : hidden;
}
div > div{
width : 1600px;
}
img{
display : inline-block;
animation-name : slideshow;
animation-duration : 10s;
animation-iteration-count : infinite;
}

div >div:hover img{
animation-play-state: paused;
}

@keyframes slideshow{
0% {
transform : translateX(0px);
}
5%{
transform : translateX(0px);
}

45%{
transform : translateX(0px);
}
55%{
transform : translateX(-400px);
}


95%{
transform : translateX(-400px);
}
100%{
transform : translateX(-800px);
}
}

</style>
<body>
<div>
<div>
<img width="400" src="1.jpg" /><!--
                                --><img width="400" src="2.jpg" /><!--
                                                                   --><img width="400" src="1.jpg" />
</div>
</div>
</body>

event delegation:
Event delegation allows us to attach a single event listener, to a parent element, that will fire for all descendants matching a selector, whether those descendants exist now or are added in the future.

document.getElementById("parent-list").addEventListener("click",function(e) {
// e.target is the clicked element!
// If it was a list item
if(e.target && e.target.nodeName == "LI") {
// List item found!  Output the ID!
console.log("List item ",e.target.id.replace("post-")," was clicked!");
}
});


#cloud.animate {
animation-name: cloud;
animation-duration: 12s;
animation-timing-function: ease;
animation-iteration-count: 1; 
animation-direction: normal;
animation-delay: 0;
animation-play-state: running;
animation-fill-mode: forwards;
}

@keyframes cloud {

0% {
opacity: 0;
left: -100px;
}

50% {
opacity: 1;
}

75% {
opacity: 1;
left: 100px;
}

100% {
opacity: 0;
left: 500px;
}

}

18. http://codepen.io/anon/pen/qbJWVy
<div class="progress-bar">
<div class="inner"></div>
</div>

<input type="button" value="add" id="add" />

.progress-bar{
width: 100%;
height: 30px;
border: 1px solid red;
border-radius: 15px;
overflow: hidden;
}

.inner{
height: 100%;
background: red;
animation: 2s progressing;
}

@keyframes progressing{
from{ width: 0}
to{ width: 100%}
}


(function(){
var runningFlag = 0;

$("#add").on("click",function(){
$("body").append("<div class='progress-bar'></div>");
if( !runningFlag ){
check();
}
});

$("body").on("animationstart",".inner",function(){
runningFlag = 1;             
});

$("body").on("animationend",".inner",function(){
$(this).parent().addClass("end");
runningFlag = 0;
check();
});

function check(){
var elmCache = $(".end").eq(-1).nextAll(".progress-bar");
if( elmCache.length ){
elmCache.eq(0).append('<div class="inner"></div>');
}
}

}());

19. 中间自适应
css left-center-right

<div class="left">left</div>
<div class="center">center</div>
<div class="right">right</div>
div{
background: #ccc;
border: 2px solid #000;
float:left;
box-sizing: border-box;
}

.left{
width: 100px;
}

.right{
width: 100px;
float: right;
}

.center{
width: calc(100% - 200px); 
}



<div class="left">left</div>
<div class="right">right</div>
<div class="center">center</div>

div{
background: #ccc;
border: 2px solid #000;
float:left;
box-sizing: border-box;
}

.left{
width: 100px;
}

.right{
width: 100px;
float: right;
}

.center{
width: 100%;
margin: 0 -100px;
padding: 0 100px;
position: relative;
z-index: -1;
}

20. requestAnimationFrame and cancelAnimationFrame 例子

var run = true, a, mWidth = window.innerWidth, i = 1, ltr = true;
var div = document.createElement("div");
div.style.width = "100px";
div.style.height = "100px";
div.style.background = "red";
document.body.appendChild(div);
div.id = "d";
div.style.position= "absolute";
div.style.left = "0px";
div.style.top = "0px";
div.style.zIndex = "999999999";
div.style.borderRadius="50%";
div.style.cursor="pointer";
div.innerHTML = "<div style='position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);'>----------------</div>"

document.getElementById("d").addEventListener("click",function(){
if(run){
window.requestAnimationFrame(render);
}else{
window.cancelAnimationFrame(a);
}  
run = !run;
});


function render(){
if(ltr) {
div.style.left = parseInt(div.style.left)+i + "px";
div.style.transform="rotate("+parseInt(div.style.left)+"deg)";
}else{
div.style.left = parseInt(div.style.left)-i + "px";
div.style.transform="rotate("+parseInt(div.style.left)+"deg)";
}
if( parseInt(div.style.left) === 0|| parseInt(div.style.left) === mWidth - 100 ) ltr = !ltr;
a = window.requestAnimationFrame(render);
}

21. Amazon
var a = {
"name" : "div",
"children": [
{
"name": "div",
"children" : [
{
"name":"span"
}
]
},{
"name": "span"
}
]
}

function calculateElement(elementObj){
var hash = {};
return fetchData(elementObj, hash);

}

function fetchData(elementObj,hash){

if( hash[elementObj["name"]] === undefined ) hash[elementObj["name"]] = 1;
else hash[elementObj["name"]]++;

if( elementObj["children"] !== undefined ){
elementObj["children"].map(function(item){

fetchData(item,hash);

});
}

return hash;

}


22.
var a = [{
"id": 1,
"name": {
"first_name" : "Craig",
"last_name": "Phillips",
},
"email": "cphillips0@disqus.com",
"country": "China",
"ip_address": "91.71.153.92"
}, {
"id": 2,
"name": {
"first_name" : "Lori",
"last_name": "Gray",
},
"email": "lgray1@berkeley.edu",
"country": "Tanzania",
"ip_address": "225.194.188.254"
}, {
"id": 3,
"name": {
"first_name" : "John",
"last_name": "Sullivan",
},
"email": "jsullivan2@si.edu",
"country": "Argentina",
"ip_address": "156.37.164.164"
}, {
"id": 4,
"name": {
"first_name" : "Gloria",
"last_name": "Ramirez",
},
"email": "gramirez3@ftc.gov",
"country": "Russia",
"ip_address": "21.19.199.1"
}, {
"id": 5,
"name": {
"first_name" : "Edward",
"last_name": "Mendoza",
},
"email": "emendoza4@house.gov",
"country": "Russia",
"ip_address": "134.131.221.72"
}];

//var b = a[0];
//readJson(a);
//fetchData("first_name",a);
fetchItem(2,a);

function fetchItem(id,jsonData){
var getData = 0;
for(var i in jsonData){
if( typeof jsonData[i] =="object"){
fetchItem(id, jsonData[i]);
}else{
if( i == "id" && jsonData["id"] == id ) getData = 1;
else if( i == "id" && jsonData["id" != id]) getData = 0;

if( getData == 1){
document.getElementById("fetch-item").innerHTML = document.getElementById("fetch-item").innerHTML+ "<li>"+ i + ":" + jsonData[i]+"</li>" ;
}
}
}
}

function readJson(jsonData){
for(var i in jsonData){
if( typeof jsonData[i] == "object" ){
readJson(jsonData[i]);
}else{
document.getElementById("abccedf").innerHTML = document.getElementById("abccedf").innerHTML+ "<li>"+ i + ":" + jsonData[i]+"</li>" ;
}
}
}

function fetchData(dataName, jsonData){
for(var i in jsonData){
if( typeof jsonData[i] == "object" ){
fetchData(dataName, jsonData[i]);
}else{
if( i == dataName ){
document.getElementById("fetch-data").innerHTML += "<li>" + i + ":" + jsonData[i] + "</li>";
}
}
}
}

<ul id="abccedf"><li>go-through</li></ul>
<ul id="fetch-data"><li>fetch-data</li></ul>
<ul id="fetch-item"><li>fetch-item</li></ul>



Reference:
Json question: https://modernpathshala.com/Learn/JSON/Interview
http://javascript-puzzlers.herokuapp.com/
https://github.com/darcyclarke/Front-end-Developer-Interview-Questions
http://www.smashingmagazine.com/2013/07/08/choosing-a-responsive-image-solution/
http://css-tricks.com/interview-questions-css/
http://darcyclarke.me/development/front-end-job-interview-questions/



