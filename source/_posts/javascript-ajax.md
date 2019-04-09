---
title: AJAX异步请求
date: 2017-09-26 16:33:26
tags: [javascript, ajax]
toc: true
categories: [Javascript, util]
---

AJAX： Asyncchronous Javascript + XMLL
Ajax的技术核心是XMLHttpRequest对象，简称XHR。

`XMLHttpRequest`对象（XHR）

以异步的方式从服务器获取数据，获取新数据后，通过DOM的方式将新数据插入到页面中。

<!-- more -->

### 1. 新建XHR对象
* IE7+、现代浏览器都支持原生的XHR对象

```JavaScript
var xhr = new XMLHttpRequest();
```

### 2. open(method, url, boolean)

> open() 方法并不会真正发送请求，而是启动一个请求以备发送。
> 同域、同端口、同协议

* `method`: 发送请求的类型（get、post、delete、put等）
* `url`： 请求URL（相对路径是相对于当前页面或者绝对路径）
* `boolean`： 是否异步发送请求

### 3. send()

> 一个参数，作为请求主体发送的数据，或者为null（body中的数据）
> 默认情况下，服务器对POST请求和表单提交的请求不会一视同仁。因此服务器端必须有程序来读取发送过来的原始数据，并从中解析出有用的部分。
> 可以使用XHR来模仿表单提交：
        1、将content-Type头部信息设置成application/x-www-form-urlencoded
        2、serialize()函数序列化表单内容。

收到相应请求后，响应数据会自动填充XHR对象的属性。
* `responseText` 作为响应主体被返回的文本。
* `responseXML` 如果响应类型是`text/xml`或者`application/xml`，这个属性中保存着包含响应数据的`XML DOM`文档。
* `status` HTTP响应状态
* `statusText` HTTP响应状态说明

> 异步请求，检测XHR对象的<code>readyState</code>属性，该属性表示请求/响应过程中的当前活动阶段。

* *0* ： 未初始化。尚未调用`open()`方法。
* *1* ： 启动。已经调用`open()`方法， 但未调用`send()`方法。
* *2* ： 发送。已经调用`send()`方法， 但未接收到响应。
* *3* ： 接收。已经接收到部分响应数据。
* *4* ： 完成。已经接收到全部响应数据，已经可以在客户端使用。

>`readyState`值变化都会触发`readystatechange`事件。

#### 同步方式请求
``` javascript
var xhr = new XMLHttpRequest();
xhr.open('get', 'example.json', false);
xhr.send(null);

if((xhr.status > 200 && xhr.status < 300) || xhr.status == 304){
        //xhr.responseText;
        //通过检测xhr.status来检测请求返回状态，不要依赖statusText，因为跨浏览器时statusText不可靠
}else{
        //请求错误, 输出错误log：xhr.status
}
```
#### 异步方式请求
```javascript
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = function(){
  if(xhr.readyState == 4){
    if(xhr.status > 200 && xhr.status < 300 || xhr.status == 304){
      alert(xhr.reponseText);
    }else{
      alert("Request was unsuccessful: " + xhr.status);
  }
}
xhr.open('get', 'example.json', true);
xhr.send(null);
```

### 4. 取消异步请求
` xhr.abort() `

### 5.HTTP头部信息

* `Accept` 浏览器处理的内容类型
* `Accept-Charset` 显示的字符集
* ` Accept-Econding` 处理的压缩编码
* `Connection` 与服务器之间的连接类型  
* `Cookie` Cookie设置
* `Host` 发出请求所在的域
* `Referer` 发出请求坐在的URI

` xhr.setRequestHeader('HeaderName', 'HeaderVal');` 使用自定义的头部字段名称，有些浏览器禁止修改默认的头部字段 。
` xhr.getResponseHeader('HeaderName'); `
` xhr.getAllResponseHeaders(); `

---
```javascript
function create_connect_obj(){
	if(window.ActiveXObject!='undefined' && window.ActiveXObject!=undefined){
        // 兼容IE7以下，可以忽略
		return new ActiveXObject('Microsoft.XMLHTTP');
	}else if(window.XMLHttpRequest!='undefined' && window.XMLHttpRequest!=undefined){
		return new XMLHttpRequest();
	}
}

var doget=function(url,data,success,fail){
	var conn=create_connect_obj();
	if(typeof(data)=='object'){
		var str='';
		for(var i in data){
			str+='&'+i+'='+data[i];
		}
		str=str.substr(1);
		if(url.indexOf('?')!=-1){
			url+=str;
		}else{
			url+='?'+str;
		}
	}else if(typeof(data)=='string'){
		if(url.indexOf('?')!=-1){
			url+=data;
		}else{
			url+='?'+data;
		}
	}
	conn.open('GET',url);
	conn.send(null);
	conn.onreadystatechange=function(){
		if(conn.readyState==4 && conn.status==200){
			if(typeof(data)=='function'){
				data(conn.response);
			}else if(typeof(success)=='function'){
				success(conn.response);	//success
			}
		}else{
			if(typeof(fail)=='function'){	//fail
				fail();	
			}
		}
	}
}

var dopost=function(url,data,success,fail){
	var conn=create_connect_obj();
	conn.open('POST',url);
	conn.setRequestHeader('Content-type','application/x-www-form-urlencoded');

	if(typeof(data)=='object'){
		var str='';
		for(var i in data){
			str+='&'+i+'='+data[i];
		}
		str=str.substr(1);
		conn.send(data);
	}else if(typeof(data)=='string'){
		conn.send(data);
	}else{
		conn.send(null);
	}
	conn.onreadystatechange=function(){
		if(conn.readyState==4 && conn.status==200){
			if(typeof(data)=='function'){
				data(conn.response);
			}else if(typeof(success)=='function'){
				success(conn.response);	//success
			}
		}else{
			if(typeof(fail)=='function'){	//fail
				fail();	
			}
		}
	}
}
```
