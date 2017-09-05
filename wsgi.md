 wsgi 是一个 web 组件的接口规范.，wsgi将 web 组件分为三类： web服务器,web中间件,web应用程序，下图来自ibm developerworks ，很好的说明了三者之间的关系

从上图可以看出来，wsgi基本处理模式为 ： WSGI Server -> (WSGI Middleware)* -> WSGI Application 。

wsgi server可以理解为一个符合wsgi规范的web server，接收request请求，封装一系列环境变量，按照wsgi规范调用注册的wsgi app，最后将response返回给客户端。

wsgi server 基本工作流程
服务器创建socket，监听端口，等待客户端连接。
当有请求来时，服务器解析客户端信息放到环境变量environ中，并调用绑定的handler来处理请求。
handler解析这个http请求，将请求信息例如method，path等放到environ中。
wsgi handler再将一些服务器端信息也放到environ中，最后服务器信息，客户端信息，本次请求信息全部都保存到了环境变量environ中。
wsgi handler 调用注册的wsgi app，并将environ和回调函数传给wsgi app
wsgi app 将reponse header/status/body 回传给wsgi handler
最终handler还是通过socket将response信息塞回给客户端。

WSGI Application
         wsgi application就是一个普通的callable对象，当有请求到来时，wsgi server会调用这个wsgi app。这个对象接收两个参数，通常为environ,start_response。environ就像前面介绍的，可以理解为环境变量，跟一次请求相关的所有信息都保存在了这个环境变量中，包括服务器信息，客户端信息，请求信息。start_response是一个callback函数，wsgi application通过调用start_response，将response headers/status 返回给wsgi server。此外这个wsgi app会return 一个iterator对象 ，这个iterator就是response body。

```python
from wsgiref.simple_server import make_server

def simple_app(environ, start_response):
    status = '200 OK'
    response_headers = [('Content-type', 'text/plain')]
    start_response(status, response_headers)
    return [u"This is hello wsgi app".encode('utf8')]

httpd = make_server('', 8000, simple_app)
print "Serving on port 8000..."
httpd.serve_forever()
```
访问http://127.0.0.1:8000 就能看到效果了。

上面讲到了wsgi app只要是一个callable对象就可以了，因此不一定要是函数，一个实现了__call__方法的实例也可以，示例代码如下：

```python
from wsgiref.simple_server import make_server

class AppClass:

    def __call__(self,environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type', 'text/plain')]
        start_response(status, response_headers)
        return ["hello world!"]

app = AppClass()
httpd = make_server('', 8000, app)
print "Serving on port 8000..."
httpd.serve_forever()
```

middleware包装
middleware是wsgi里的概念，用来包装你的app，包装之后就可以在被包装的部分被调用前后做点其他处理：

[Middleware处理一下输入] -> [APP] -> [Middleware处理一下APP的输出]
具体到SharedDataMiddleware，其实是处理静态内容（例如js、图片……）的，在APP被调用前，检测一下是不是在可以直接返回静态文件，可以就直接返回，不调用APP了，不可以就继续调用APP。