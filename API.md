##Ajax请求HTTP api参考

服务端提供 <a href="http://www.ruanyifeng.com/blog/2014/05/restful_api.html">RESTful API</a> 接口，前端在页面上使用 Ajax 或者在服务器端使用 PHP 来调用这些接口。
请求 API 时，通过指定的 GET 或 POST 方法把参数发送过去，API 返回的 HTTP Header 带上 Content-Type:application/json，返回内容为合法的 JSON 字符串。

###请求 API(Request)
* 原则上获取数据的接口使用 HTTP GET 方法请求，保存数据的接口使用 HTTP POST 方法请求。
* HTTP GET 请求的参数以 Query String 的形式传参。

如： 
> http://domain/uri?key1=value1&key2=value2&...&keyN=valueN

特别的，数组参数的传递方式是：
> http://domain/uri?key[]=value1&key[]=value2&...&key[]=valueN

部分采用 [jsonp](http://www.cnblogs.com/yuzhongwusan/archive/2012/12/11/2812849.html)：
> http://domain/uri?key[]=value1&key[]=value2&...&key[]=valueN....&callback=?

更复杂的参数可以使用 JSON 格式传参，但不推荐这样的形式。
*　HTTP POST 请求的参数格式与 GET 请求一样，只不过把参数放到 HTTP Body 中发送给服务器。
* 所有请求参数的编码为 UTF-8

### API 返回(Response)
返回的 JSON 基本格式为：

```html
{
  "errcode":0,
  "errmsg":"",
  "data":[]
}
or
{
  "errcode":100,
  "errstr":"数据出错",
  "data":[]
}
```
* errcode：整型，用于表示操作是否成功，0 表示成功，大于 0 表示失败，具体失败代码 API 提供方自己定义。
* errstr：字符串，用于在失败的时候显示给用户的错误信息，errno 为 0 时，errmsg 为空字符串。
* data：任意类型，所有 API 返回数据都放在 data 中。data 是可选内容。

原则上 JSON 第一级不要出现其他字段，也就是只能出现 errcode、errstr 和 data。
JSON 字符串要放在一行中，不允许出现换行符。（特殊字符都要转义，具体请参考上文中的 JSON 格式规范）
所有返回值编码为 UTF-8



### 常见功能型接口数据格式参考

```js

// ../api/paginarion?param1=xxx&param2=xxx&p=12  pageno 第几页 pagesize 每页多少条数据
{ 
  "errcode":0,
  "errstr":"",
  "data":{
    count: 10000,
    page:'',
    list:[
        {....},
        {...}
        ...
    ]
  }
}
// 简单的列表
// ../api/search?param1=xxx&param2=xxx
{
  "errcode":0,
  "errmstr":"",
  "data":[
    {...},
    {...},
    ....
  ]
}

// 获取详情(根据某个id取得某个对象的字段)
// ../api/details?id=xxx
{
  "errcode":0,
  "errstr":"",
  "data":[
    id: xxx
    'key':'',
    'key1': '',
    ...
    
  ]
}

```












