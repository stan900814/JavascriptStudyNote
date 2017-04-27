#Javascript高程学习笔记#

##第五章##
###5.2###
创建数组的方法两种：1、 利用数组构造函数`var a=new Array()`;可省略new关键字。2、使用数组字面量表示法，`var a=[1,2,3,.....]`;
数组的length属性是可读可写的，所以用此属性对数组进行项的增加和删除.
`Array.isArray()`检测某个值是否是数组。调用数组`toString()``valueOf()`方法返回的值都是数组中每一个值的字符串拼接而成的以逗号分隔的字符串。使用`join()`方法可以使用不同的分隔符来构建字符串。`var a=['red','blue','green']; `
`alert(a.join(“_”)）；//red_blue_green`
**如果数组中的某一项的值是null或者undefined那么该值在join()、toString()、valueOf()方法中返回的结果以空字符表示**.  
数组的push()与pop（）方法：push接收任意数量的参数把它们逐个添加到数组末尾，**并返回修改后数组的长度**(**直接修改数组**)；pop则从数组末尾移除最后一项（**直接修改数组**），**并返回移除的项**。   
shift()与unshift()方法：shift能移除数组中的第一项，**并返回该项**，同事数组长度减1.unshift能够在数组前端添加任意数量的项**并返回新数组的长度**。    
reverse()与sort()方法：reverse方法会反转数组项目的顺序，sort方法按升序排列数组项，**sort方法会调用toString()方法将所有数组项转化成字符串，即使数组中的每个项都是数值，sort()方法也是比较的字符串**，sort方法可以接受一个比较函数作为参考以便指定哪个位于哪个值得前面：
> function compare(value1, value2) {  
> 
if (value1 < value2) {  
>
return -1;  
>
} else if (value1 > value2) {  
>
return 1;  
>
} else {  
>
return 0;  
>
}}  
>var values=[0,1,5,10,15];  
>  
>  values.sort(compare);
>
>alert(values);   //0,1,5,10,15    
  
当然也可以改变比较函数使sort（）方法产生降序排序的结果，只要交换比较函数返回的值即可。  

concat()方法与slice()方法：concat方法会基于当前数组创建一个新的数组，这个方法先创建一个当前数组的副本，然后将接收的参数添加到这个副本的末尾，最后返回**新**数组。如果没有传递参数，就只是复制当前数组并返回副本。  
>var colors = ["red", "green", "blue"];    
>
>var colors2 = colors.concat("yellow", ["black", "brown"]);  
>
alert(colors); //red,green,blue  
>
>alert(colors2); //red,green,blue,yellow,black,brown
  
slice()方法能够基于当前数组中的一或多个项创建一个新数组，它能接收一或两个参数，即要返回项的起始和结束为止。在只有一个参数的情况下， slice()方法返回从该
参数指定位置开始到当前数组末尾的所有项。如果有两个参数，该方法返回起始和结束位置之间的项
**但不包括结束位置的项**。注意， slice()方法**不会影响原始数组**。  
>var colors = ["red", "green", "blue", "yellow", "purple"];  
>
>var colors2 = colors.slice(1);  

>var colors3 = colors.slice(1,4);  

>alert(colors2); //green,blue,yellow,purple  

>alert(colors3); //green,blue,yellow  

如果 slice()方法的参数中有一个负数，则用数组长度加上该数来确定相应的位置。例如，在一个包含 5 项的数组上调用 slice(-2,-1)与调用 slice(3,4)得到的结果相同。如果结束位置小于起始位置，则返回空数组。  
**splice()方法**： splice()方法最多接受三个参数，分别是起始位置、要删的项数、要插入的项目，例如：`splice(2,1,"red","green")`会从当前数组的位置2开始删除1个项，然后将“red”与“green”从位置2插入到数组中。  **splice()数组始终会返回一个数组，该数组是从原始数组中删除的项（如果没有删除项，则返回空数组）**。  
>var colors = ["red", "green", "blue"];  
>
>var removed = colors.splice(0,1); // 删除第一项  
>
>alert(colors); // green,blue  

>alert(removed); // red，返回的数组中只包含一项  

>removed = colors.splice(1, 0, "yellow", "orange"); // 从位置 1 开始插入两项  

>alert(colors); // green,yellow,orange,blue  

>alert(removed); // 返回的是一个空数组  

>removed = colors.splice(1, 1, "red", "purple"); // 插入两项，删除一项  

>alert(colors); // green,red,purple,orange,blue  

>alert(removed); // yellow，返回的数组中只包含一项
###5.3###
创建日期对象， `var now=new Date();`Date.parse()方法能创建一个指定日期的对象例如：`var someDate=new Date(Date.parse("May 25,2004"));`该例子等价于：`var someDate=new Date("May 25,2004");`  
在对两个日期进行比较的时候可以直接用比较符进行比较；
###5.5###
定义函数的三种方法：
- `function sum(num1,num2){return num1 + num2;}`
- `var sum=function(num1,num2){return num1 + num2};`
- `var sum=new Function("num1","num2","return num1 + num2");`  //不推荐（解析两次，影响性能）  
>function sum(num1, num2){  
>
>return num1 + num2;  
>
>}  
>
>alert(sum(10,10)); //20  

>var anotherSum = sum;  

>alert(anotherSum(10,10)); //20  

>sum = null;  

>alert(anotherSum(10,10)); //20  
**使用不带圆括号的函数名是访问函数指针，而非调用函数**，所以上面即使sum=null,anothoersum()也能正常调用。  
**对于函数声明与函数表达式，解析器会在执行任何代码前率先读取函数声明，而函数表达式则需要等到解析器执行到他所在代码行才会真正被执行。**  
关于arguments的callee属性，该属性是一个指针，指向拥有这个arguments对象的函数。  
>function factorial(num){  
>
>if (num <=1) {  
>
>return 1;  
>
>} else {  
>
>return num * factorial(num-1)  
>
>}
>}

----------
>function factorial(num){  
>
>if (num <=1) {  
>
>return 1;  
>
>} else {  
>
>return num * arguments.callee(num-1)  
>
>}
>}
上面两个定义的阶乘函数效果是一样的。但是当函数名字改变时第一种情况就会出现问题。比如：  
>var trueFactorial = factorial;  
>
>factorial = function(){  
>
>return 0;  
>
>};  
>
>alert(trueFactorial(5)); //120  
>
>alert(factorial(5)); //0  
**关于this**,**this引用的是函数据以执行的环境对象————或者也可以说是this值**当在网页的全局作用于中调用函数时，this对象引用就是window  
函数的length属性表示函数希望接收到的命名参数的个数  
**call()、apply()与bind()**

##第六章##  
###6.1###
对象的属性类型：1、数据属性，包含：

- `[[Configurable]]`表示能否通过 delete 删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性，这个特性默认值为 true

- `[[Enumerable]]`表示能否通过for-in循环遍历，默认值为true

- `[[Writable]]`表示属性值是否可修改，默认值为true

- `[[Value]]`包含属性的数据值，读和写都是这里，默认值为undefined
修改这些属性的默认值得使用Object.defineProperty()方法，该方法接收三个参数：属性所在对象，属性名，属性描述符（configurable、enumerable、writable、value),例如：
>var person = {};  
>
>Object.defineProperty(person, "name", {  
>
>writable: false,  
>
>value: "Nicholas"  
>
>});  
>
>alert(person.name); //"Nicholas"  
>
>person.name = "Greg";  
>
>alert(person.name); //"Nicholas"
2、访问器属性：  
###6.2###
创建对象的模式：1、工厂模式；2、构造函数模式；  
工厂模式实例：  
>function createPerson(name,age,job){  
>var o =new Object();   
> 
>o.name=name;  
>o.age=age;  
>o.job=job;  
>o.sayName=function(){  
>alert(this.name);  
>}  
>return o;  
>var person1=createPerson("a",21,"xxx")  
>var person2=createPerson("b",22,"xxx")  

构造函数实例：
>function Person(name,age,job){  
>this.name=name;
>this.age=age;
>this.job=job;  
>this.sayName=function(){  
>alert(this.name);  
>}  
>}  
>var person1=new Person("a",21,"xxx")  
>var person2=new Person("b",20,"xxx")      

**构造函数与其他函数的区别就在于，构造函数只能通过new操作符来调用**    
3、**原型模式**：   
每个函数都有一个**prototype**（原型）属性，这个属性是一个指针，指向一个对象，该对象包含可以由所有由该函数创造的实例共享的属性和方法。  
>function Person(){  
>}  
>person.prototype.name='a';  
>person.prototype.age=20;  
>person.prototype.job="xxx";  
>person.prototype.sayName=function(){  
>alert(this.name);  
>}  
>var person1=new Person();  
>person.sayName();  //"a"  
>var person2=new Person();  
>person.sayName();  //"a"  
>alert(person1.sayName==person2.sayName);  //true  
##第4章##
###4.1###
变量包含的值：基本类型（undefined、null、boolean、number、string）、引用类型（对象）。  
基本类型值的复制是值的直接复制，从一个变量向另外一个变量复制基本类型值之后，两变量上的这个值互不影响。  
引用类型值的复制是对引用对象的复制，从一个变量向另外一个变量复制引用类型值之后，两变量同时引用同一个对象，所以两变量会互相影响。  
关于参数的传递，理解下面的例子：  
>funtion setName(obj){  
>obj.name="Nicholas";  
>obj =new Object();  
>obj.name="Greg";  
>}  
>var person =new Object();
>setName(person);  
>alert(person.name);   //""Nicholas""   

----------
typeof:检测变量值的**基本类型**，如果是对象或者**null**，返回“object”  
instanceof:检测变量值的**引用类型**，根据原型链来识别  
###4.2###
**执行环境（execution context）**:   
 
**作用域链（scope chain）**:

----------
**回调函数（callback）**：将一个函数作为另外一个函数的参数，并且在另外一个函数中调用了这个函数，这个函数就叫做回调函数。example：setTimeout/setInterval。  

**JavaScript中的同步与异步**：  
**异步编程的几种实现方法**：








  



  




