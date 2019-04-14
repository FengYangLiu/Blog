# HTML语义：div和span不是够用了吗？

语义类标签是什么，使用它有什么好处？

## 本节概述
- 语义类标签是什么
- 为什么要用语义类标签
- 语义标签怎么用与实例

## 语义标签是什么
语义标签：特点是视觉表现上互相都差不多，主要的区别在于它们表示了不同的语义

winter认为在实际工作中html用于描述软件界面比富文本多，div与span标签能解决大部分的问题。但老师本人并未一杆子打死，也抛出了某些工作使用语义化带来很多好处如：
1. 语义标签对开发着更友好，无CSS时，网页结构明显可维护性高，也有利于 团队
2. 对人类友好。如屏幕阅读器、爬虫、文章目录生成、SEO、搜索量等

winter对语义化标签的建议：
- 用对比不用好
- 不用比用错好
- 有理想的工程师追求用对

## 语义标签实例
实例

-  作为自然语言的延伸
    - ruby -- 文字顶上出现标注
    -  em 表示强调语气
- 作为标题摘要的语义标签
    - h1~h6平铺 与配合hgroup添加副标题
    - html5中在嵌套的session中添加h1 浏览器会自动降级如sesion中还session 并且存在h1 呢么这里就是h2
    ```
    <h1></h1> //h1
    <session>
        <h1>111</h1> // h2
        <session>
            <h1>2222</h1> // h3
        </session>
    </session>
    ```
- 作为整体结构的语义类标签
    - 语义化对机器阅读模式变得越来越重要具体如：session、header、footer、aside、nav、article等等

```
<!--作为整体结构的语义类标签-->
<body>
    <header>……</header>
    <article>
        <header>……</header>
        <section>……</section>
        <section>……</section>
        <section>……</section>
        <footer>……</footer>
    </article>
    <article>
        ……
    </article>
    <article>
        ……
    </article>
    <footer>
        <address></address>
    </footer>
</body>

```
## 小结
本节作者主要阐述了他本人对语义化标签的看法，并且向我们提供了建设性的意见，用好用对语义化标签否则就尽量不用。还从以下方向解析
- 作为自然语言的延伸
- 作为标题摘要的语义标签
- 作为整体结构化的语义标签

### 自我思考小结
本人赞成老师的观点，首先是要熟悉了解语义使用更佳，如果只是含糊不清的使用div+span其实更好。



