# HTML与web相关知识汇总



## 一、关于<! DOCTYPE> 标签 

​          **DTD**（document type definition，文档类型定义）是一系列的语法规则， 用来定义XML或(X)HTML的文件类型。浏览器会使用它来判断文档类型， 决定使用何种协议来解析，以及切换浏览器模式。

​         **<!DOCTYPE>**用于指示 web 浏览器关于页面使用哪个 HTML 版本进行编写的指令，它不是html标签，声明必须是 HTML 文档的第一行，位于 `<html>` 标签之前。

​        **<!DOCTYPE>**声明包括标准版本和一个DTD文件的URI。常用的DOCTYPE声明有以下几种：

  **HTML 5**

```html
<!DOCTYPE html>
```

  **HTML 4.01 Stric（标准）**

​          该 DTD 包含所有 HTML 元素和属性，但**不包括**展示性的和弃用的元素（比如 font）。不允许使用框架集（Framesets）。

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```

**HTML 4.01 Transitional（过渡）**

​         该 DTD 包含所有 HTML 元素和属性，**包括**展示性的和弃用的元素（比如 font）。不允许使用框架集（Framesets）。

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
"http://www.w3.org/TR/html4/loose.dtd">
```

**HTML 4.01 Frameset**

​        该 DTD 等同于 HTML 4.01 Transitional，但允许框架集内容

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" 
"http://www.w3.org/TR/html4/frameset.dtd">
```

## 二、关于 `<meta>` 标签

​          `<meta>` 位于 head 元素中 **提供关于 HTML 文档的元数据**。元数据不会显示在页面上，但是对于机器是可读的。

​          典型的情况是，meta 元素被用于**规定页面的描述、关键词、文档的作者、最后修改时间以及其他元数据**。元数据可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他 web 服务。

   **组成**

   1.name属性

​           name属性主要用于描述网页，比如网页的关键词，叙述等。与之对应的属性值为content，content中的内容是对name填入类型的具体描述，便于搜索引擎抓取。
​      name属性语法格式是：

```
<meta name="参数" content="具体的描述">。
```

​      常用属性参数：

 A. keywords(关键字)

说明：用于告诉搜索引擎，你网页的关键字。
举例：

```
<meta name="keywords" content="Liaeor,博客">
```

B. description(网站内容的描述)

说明：用于告诉搜索引擎，你网站的主要内容。
举例：

```
<meta name="description" content="学习笔记，闲谈">
```

C. viewport(移动端的窗口)

说明：这个概念较为复杂，具体的会在下篇博文中讲述。
这个属性常用于设计移动端网页。在用bootstrap,AmazeUI等框架时候都有用过viewport。

举例（常用范例）：

```
<meta name="viewport" content="width=device-width, initial-scale=1">
```

​      2.http-equiv属性

​         相当于HTTP的作用，比如说定义些HTTP参数啥的。至少要有一个参数content-type:text/html。这将告诉浏览器准备接受一个 HTML 文档。

 http-equiv属性语法格式是：

```
<meta http-equiv="参数" content="具体的描述">
```

​    常用属性参数：

​        content-Type(设定网页字符集)

说明：用于设定网页字符集，便于浏览器解析与渲染页面
举例：

```
<meta http-equiv="content-Type" content="text/html;charset=utf-8">  //旧的HTML，不推荐

<meta charset="utf-8"> //HTML5设定网页字符集的方式，推荐使用UTF-8
```

 详细查阅：[ <meta> 标签总结](https://segmentfault.com/a/1190000004279791)



##三、HTML全局属性(global attributes)

 参考资料：[MDN: html global attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes)或者[W3C HTML global-attributes](http://www.w3.org/TR/html-markup/global-attributes.html#common.attrs.core)

- `accesskey`:设置快捷键，提供快速访问元素如[aaa](https://github.com/qiu-deqing/FE-interview#)在windows下的firefox中按`alt + shift + a`可激活元素
- `class`:为元素设置类标识，多个类名用空格分开，CSS和javascript可通过class属性获取元素
- `contenteditable`: 指定元素内容是否可编辑
- `contextmenu`: 自定义鼠标右键弹出菜单内容
- `data-*`: 为元素增加自定义属性
- `dir`: 设置元素文本方向
- `draggable`: 设置元素是否可拖拽
- `dropzone`: 设置元素拖放类型： copy, move, link
- `hidden`: 表示一个元素是否与文档。样式上会导致元素不显示，但是不能用这个属性实现样式效果
- `id`: 元素id，文档内唯一
- `lang`: 元素内容的的语言
- `spellcheck`: 是否启动拼写和语法检查
- `style`: 行内css样式
- `tabindex`: 设置元素可以获得焦点，通过tab可以导航
- `title`: 元素相关的建议信息
- `translate`: 元素和子孙节点内容是否需要本地化



## 四、 < img > 的 title 和 alt 属性的区别

1. `title`是global attributes之一，用于为元素提供附加的advisory information。通常当鼠标**滑动到元素上的时候显示**。
2. `alt`是`<img>`的特有属性，是**图片内容的等价描述，用于图片无法加载时显示**、读屏器阅读图片。可提高图片可访问性，除了纯装饰图片外都必须设置有意义的值，搜索引擎会重点分析。



## 五、什么是web语义化,有什么好处

​           web语义化是**指通过HTML标记表示页面包含的信息，包含了HTML标签的语义化和css命名的语义化**。 

​          HTML标签的语义化是指：通过使用包含语义的标签（如h1-h6）恰当地表示文档结构

​          css命名的语义化是指：为html标签添加有意义的class，id补充未表达的语义

 为什么需要语义化：

- 搜索引擎更好地理解页面，有利于收录
- 便团队项目的可持续运作及维护
- 去掉样式后页面呈现清晰的结构
- 盲人使用读屏器更好地阅读



## 六、前端需要注意哪些SEO（搜索引擎优化）

1. 合理的title、description、keywords：搜索对这三项的权重逐个减小，title值强调重点即可，重要关键词出现不要超过2次，而且要靠前，不同页面title要有所不同；description把页面内容高度概括，长度合适，不可过分堆砌关键词，不同页面description有所不同；keywords列举出重要关键词即可
2. 语义化的HTML代码，符合W3C规范：语义化代码让搜索引擎容易理解网页
3. 重要内容HTML代码放在最前：搜索引擎抓取HTML顺序是从上到下，有的搜索引擎对抓取长度有限制，保证重要内容一定会被抓取
4. 重要内容不要用js输出：爬虫不会执行js获取内容
5. 少用iframe：搜索引擎不会抓取iframe中的内容
6. 非装饰性图片必须加alt
7. 提高网站速度：网站速度是搜索引擎排序的一个重要指标



## 七、如何进行网站性能优化

​          网站性能会受诸多方面的影响，我们可以针对各方面做出合理的优化：

- content方面
  1. 减少HTTP请求：合并文件、CSS精灵（css sprite）、inline Image
  2. 减少DNS查询：DNS查询完成之前浏览器不能从这个主机下载任何任何文件。方法：DNS缓存、将资源分布到恰当数量的主机名，平衡并行下载和DNS查询
  3. 避免重定向：多余的中间访问
  4. 使Ajax可缓存
  5. 非必须组件延迟加载
  6. 未来所需组件预加载
  7. 减少DOM元素数量
  8. 将资源放到不同的域下：浏览器同时从一个域下载资源的数目有限，增加域可以提高并行下载量
  9. 减少iframe数量
  10. 不要404
- Server方面
  1. 使用CDN
  2. 添加Expires或者Cache-Control响应头
  3. 对组件使用Gzip压缩
  4. 配置ETag
  5. Flush Buffer Early
  6. Ajax使用GET进行请求
  7. 避免空src的img标签
- Cookie方面
  1. 减小cookie大小
  2. 引入资源的域名不要包含cookie
- css方面
  1. 将样式表放到页面顶部
  2. 不使用CSS表达式
  3. 使用不使用@import
  4. 不使用IE的Filter
- Javascript方面
  1. 将脚本放到页面底部
  2. 将javascript和css从外部引入
  3. 压缩javascript和css
  4. 删除不需要的脚本
  5. 减少DOM访问
  6. 合理设计事件监听器
- 图片方面
  1. 优化图片：根据实际颜色需要选择色深、压缩
  2. 优化css精灵
  3. 不要在HTML中拉伸图片
  4. 保证favicon.ico小并且可缓存
- 移动方面
  1. 保证组件小于25k
  2. Pack Components into a Multipart Document



## 八、渐进增强与优雅降级

​    **渐进增强（Progressive Enhancement）**：*一开始就针对低版本浏览器进行构建页面，完成基本的功能*，然后再针对高级浏览器进行效果、交互、追加功能达到更好的体验。

​    **优雅降级（Graceful Degradation）**：*一开始就构建站点的完整功能*，然后针对浏览器测试和修复。比如一开始使用 CSS3 的特性构建了一个应用，然后逐步针对各大浏览器进行 hack 使其可以在低版本浏览器上正常浏览。

​    **二者区别**

​        关键的区别则在于它们各自关注同一事物的不同的点，定义里给出的解释很清晰。

​        **优雅降级**观点认为应该针对那些最高级、最完善的浏览器来设计网站

​        **渐进增强**观点则认为应关注于内容本身

例：

>  .transition { /*渐进增强写法*/
>   -webkit-transition: all .5s;
>  ​     -moz-transition: all .5s;
>  ​       -o-transition: all .5s;
>  ​          transition: all .5s;
>  }
>  .transition { /*优雅降级写法*/
>  ​          transition: all .5s;
>  ​       -o-transition: all .5s;
>  ​     -moz-transition: all .5s;
>   -webkit-transition: all .5s;
>  }

[具体参考](http://www.jianshu.com/p/d313f1108862)



## 九、从浏览器地址栏输入url到显示页面的步骤(以HTTP为例)

1. 在浏览器地址栏输入URL

2. 浏览器查看缓存，如果请求资源在缓存中并且新鲜，跳转到转码步骤

   1. 如果资源未缓存，发起新请求
   2. 如果已缓存，检验是否足够新鲜，足够新鲜直接提供给客户端，否则与服务器进行验证。
   3. 检验新鲜通常有两个HTTP头进行控制Expires和Cache-Control：
      - HTTP1.0提供Expires，值为一个绝对时间表示缓存新鲜日期
      - HTTP1.1增加了Cache-Control: max-age=,值为以秒为单位的最大新鲜时间

3. 浏览器**解析URL**获取协议，主机，端口，path

4. 浏览器**组装一个HTTP（GET）请求报文**

5. 浏览器获取主机ip地址，过程如下：

   1. 浏览器缓存
   2. 本机缓存
   3. hosts文件
   4. 路由器缓存
   5. ISP DNS缓存
   6. DNS递归查询（可能存在负载均衡导致每次IP不一样）

6. 打开一个socket与目标IP地址**，端口建立TCP链接，三次握手**如下：

   1. 客户端发送一个TCP的**SYN=1，Seq=X**的包到服务器端口
   2. 服务器发回**SYN=1， ACK=X+1， Seq=Y**的响应包
   3. 客户端发送**ACK=Y+1， Seq=Z**

7. TCP链接建立后**发送HTTP请求**

8. 服务器接受请求并解析，将请求转发到服务程序，如虚拟主机使用HTTP Host头部判断请求的服务程序

9. 服务器检查**HTTP请求头是否包含缓存验证信息**如果验证缓存新鲜，返回**304**等对应状态码

10. 处理程序读取完整请求并准备HTTP响应，可能需要查询数据库等操作

11. 服务器将**响应报文通过TCP连接发送回浏览器**

12. 浏览器接收HTTP响应，然后根据情况选择关闭TCP连接或者保留重用，**关闭TCP连接的四次握手**如下：

    1. 主动方发送**Fin=1， Ack=Z， Seq= X**报文
    2. 被动方发送**ACK=X+1， Seq=Z**报文
    3. 被动方发送**Fin=1， ACK=X， Seq=Y**报文
    4. 主动方发送**ACK=Y， Seq=X**报文

13. 浏览器检查响应状态吗：是否为1XX，3XX， 4XX， 5XX，这些情况处理与2XX不同

14. 如果资源可缓存，**进行缓存**

15. 对响应进行**解码**（例如gzip压缩）

16. 根据资源类型决定如何处理（假设资源为HTML文档）

    ​

    **解析HTML文档，构建DOM树，下载资源，构造CSSOM树，执行js脚本**，这些操作没有严格的先后顺序，以下分别解释：

17. 构建DOM树：

    1. **Tokenizing**：根据HTML规范将字符流解析为标记
    2. **Lexing**：词法分析将标记转换为对象并定义属性和规则
    3. **DOM construction**：根据HTML标记关系将对象组成DOM树

18. 解析过程中遇到图片、样式表、js文件，**启动下载**

19. 构建CSSOM树：

    1. **Tokenizing**：字符流转换为标记流
    2. **Node**：根据标记创建节点
    3. **CSSOM**：节点创建CSSOM树

20. 根据DOM树和CSSOM树构建渲染树:

    1. 从DOM树的根节点遍历所有**可见节点**，不可见节点包括：1）`script`,`meta`这样本身不可见的标签。2)被css隐藏的节点，如`display: none`
    2. 对每一个可见节点，找到恰当的CSSOM规则并应用
    3. 发布可视节点的内容和计算样式

21. js解析如下：

    1. 浏览器创建Document对象并解析HTML，将解析到的元素和文本节点添加到文档中，此时**document.readystate为loading**
    2. HTML解析器遇到**没有async和defer的script时**，将他们添加到文档中，然后执行行内或外部脚本。这些脚本会同步执行，并且在脚本下载和执行时解析器会暂停。这样就可以用document.write()把文本插入到输入流中。**同步脚本经常简单定义函数和注册事件处理程序，他们可以遍历和操作script和他们之前的文档内容**
    3. 当解析器遇到设置了**async**属性的script时，开始下载脚本并继续解析文档。脚本会在它**下载完成后尽快执行**，但是**解析器不会停下来等它下载**。异步脚本**禁止使用document.write()**，它们可以访问自己script和之前的文档元素
    4. 当文档完成解析，document.readState变成interactive
    5. 所有**defer**脚本会**按照在文档出现的顺序执行**，延迟脚本**能访问完整文档树**，禁止使用document.write()
    6. 浏览器**在Document对象上触发DOMContentLoaded事件**
    7. 此时文档完全解析完成，浏览器可能还在等待如图片等内容加载，等这些**内容完成载入并且所有异步脚本完成载入和执行**，document.readState变为complete,window触发load事件

22. **显示页面**（HTML解析过程中会逐步显示页面）



## 十、HTTP 请求 method

1. **GET**是最常用的方法，通常用于**请求服务器发送某个资源**。
2. **POST**起初是用来向服务器输入数据的。实际上，通常会用它来支持HTML的表单。表单中填好的数据通常会被送给服务器，然后由服务器将其发送到要去的地方。
3. **HEAD**与GET类似，但**服务器在响应中值返回首部，不返回实体的主体部分**
4. **PUT**让服务器**用请求的主体部分来创建一个由所请求的URL命名的新文档，或者，如果那个URL已经存在的话，就用干这个主体替代它**
5. **TRACE**会在目的服务器端发起一个环回诊断，最后一站的服务器会弹回一个TRACE响应并在响应主体中携带它收到的原始请求报文。TRACE方法主要用于诊断，用于验证请求是否如愿穿过了请求/响应链。
6. **OPTIONS**方法请求web服务器告知其支持的各种功能。可以查询服务器支持哪些方法或者对某些特殊资源支持哪些方法。
7. **DELETE**请求服务器删除请求URL指定的资源
8. **CONNECT**方法建立一个到由目标资源标识的服务器的隧道
9. **PATCH**方法用于对资源应用部分修改



##十一、常见 http 状态码

- 1XX: 信息状态码
  - **100  Continue(继续)** ： 客户端应当继续发送请求。
- 2XX: 成功状态码
  - **200 OK(成功)** ：请求成功，请求所希望的响应头或数据体将随此响应返回
- 3XX: 重定向
  - **301 Moved Permanently(永久移动)**：所请求的URI资源路径已经改变,新的URL会在响应的`Location`:头字段里找到
  - **302 Found(临时移动)**：所请求的URI资源路径临时改变,并且还可能继续改变.因此客户端在以后访问时还得继续使用该URI.新的URL会在响应的`Location:`头字段里找到.


- 4XX: 客户端错误
  - **404 Not Found(未找到)**：服务器找不到所请求的资源.由于经常发生此种情况,所以该状态码在上网时是非常常见的.


- 5XX: 服务器错误
  - **Internal Server Error(内部服务器错误)**：服务器遇到未知的无法解决的问题. 



