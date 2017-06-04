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




