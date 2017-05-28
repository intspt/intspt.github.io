---
layout: base
permalink: /note/2015-02-05-00
---

原来是MySQL连接超时的问题

据sae官方的说明（附链接：[常见问题-SAE文档中心](http://www.sinacloud.com/doc/sae/python/faq.html)）

> MySQL连接超时时间为30s，不是默认的8小时，所以你需要在代码中检查是否超时，是否需要重连。对于使用sqlalchemy的用户，需要在请求处理结束时调用 db.session.close() ，关闭当前session，将mysql连接还给连接池，并且将连接池的连接recyle时间设的小一点（推荐为10s）.

于是在app config里添加了超时自动重连的参数

    SQLALCHEMY_POOL_RECYCLE = 10

并且在请求结束后调用了db.session.close()

目前为止没有再发生这种状况哈哈哈

至于这个神奇的参数是我google到的（MD他们是怎么知道的。。。文档里似乎没有啊。。。我回去在仔细看看）

【好吧还真有。。。附链接：[Flask-SQLAlchemy Configuration Keys](http://pythonhosted.org/Flask-SQLAlchemy/config.html)】

总之问题解决了

可喜可贺，可口可乐

（恭喜恭喜 (((o(*ﾟ▽ﾟ*)o))) by wendy）