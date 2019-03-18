#bloom filter 过滤器

很多业务量比较大,如果直接调用接口可能导致性能问题. 所以使用bloom filter 挡住无效的请求.
高效的挡住无效的请求和流量，可用于数据库不存在，是否在集合中判断。

##安装
```shell
git clone https://github.com/luw2007/bloomfilter.git && \
    cd bloomfilter && \
    pip install -r requirements.txt && \
    python setup.py install
```
###通过源代码安装项目依赖：
pyreBloom, hiredis(非必须)
```shell
git clone https://github.com/redis/hiredis.git /root/src/hiredis && \
    cd /root/src/hiredis && \
    make && make PREFIX=/usr install &&\
    ldconfig
git clone https://github.com/seomoz/pyreBloom /root/src/pyreBloom && \
    cd /root/src/pyreBloom && \
    python setup.py install
```

##使用方法:
>>> from bloomfilter.base import BaseModel
>>> class TestModel(BaseModel):
...    PREFIX = "bf:test"
>>> t = TestModel()
>>> t.add('hello')
1
>>> t.extend(['hi', 'world'])
2
>>> t.contains('hi')
True
>>> t.delete()

##可用方法:
extend, keys, contains, add, put, hashes, bits, delete

##例子

请查看[example](tree/master/examples)目录


##Q&A
1. 运行报错, 缺少pyreBloom?
```
In [1]: from bloomfilter.base import BaseModel
---------------------------------------------------------------------------
ModuleNotFoundError                       Traceback (most recent call last)
<ipython-input-1-3172e213138d> in <module>
----> 1 from bloomfilter.base import BaseModel

~/github/bloomfilter/bloomfilter/base.py in <module>
     52 import logging
     53 from six import PY3 as IS_PY3
---> 54 from pyreBloom import pyreBloom, pyreBloomException
     55
     56 from bloomfilter.utils import force_utf8

ModuleNotFoundError: No module named 'pyreBloom'
```
安装`pyreBloom`，pip install -r requirements.txt
