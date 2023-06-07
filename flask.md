# Python Flask API

## MVC web model
M：Model        ==>    与数据库相关的模型层

V：Views         ==>    网页的地址，以及渲染网页等

C：Controller  ==>    访问网页地址后，读取页面数据，调用业务逻辑

## Python Web Frameworks
Django    **市场**占有率极高的框架，适合大项目，官方文档齐全

Tornado  **异步**高性能框架，包含许多底层细节，少而精

Web.py   作者过于nb，很早被上帝请去喝茶，**停止维护**了

Flask    微框架，**轻量级**，扩展插件较多

[2]: https://mp.weixin.qq.com/s?__biz=MzAxMTM3MDk2Ng==&mid=2451660085&idx=1&sn=30f869f5b856568064312c2f486fabfd&chksm=8c97d58cbbe05c9a65d44181b1a7f7555f396b0a838d7e321a49a72d10bffa38263f3b85fd80&scene=21#wechat_redirect

## Static
pages existed on the web that don't need to be compiled, like HTML

`static_folder`: where you store the static content. When it's undefined, it will assume it's stored in a `static` folder
- same as `template_folder` (assuming `templates`)

`static_url_path`: when you type it in the url to find the static content, it will point to the content stored in `static_folder`

```Python
import flask
app=flask.Flask(__name__,static_url_path='/pp/2/4556565656',static_folder='1245487878awda')
@app.route('/')
def test_01():
    return 'hello'
if __name__ == '__main__':
    app.run()
```
[1]: https://www.cnblogs.com/lhTest/p/15242591.html

## Dynamic (render template)
Automatically render HTML when return
```
@app.route('/')
def hello_world():
    return '<h1>Hello World！</h1>\
        <img src="img1.jpg"> \
        
```
