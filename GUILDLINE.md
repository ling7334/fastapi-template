# 开发规范

## Python 开发规范

Python 风格规范 本项目包含了部分 Google 风格规范和 PEP8 规范，仅用作内部培训学习
https://www.jianshu.com/p/d414e90dc953

### 命名规范

#### Python 之父推荐的规范

| Type                       | Public             | Internal                                                             |
| -------------------------- | ------------------ | -------------------------------------------------------------------- |
| Modules                    | lower_with_under   | \_lower_with_under                                                   |
| Packages                   | lower_with_under   |
| Classes                    | CapWords           | \_CapWords                                                           |
| Exceptions                 | CapWords           |
| Functions                  | lower_with_under() | \_lower_with_under()                                                 |
| Global/Class Constants     | CAPS_WITH_UNDER    | \_CAPS_WITH_UNDER                                                    |
| Global/Class Variables     | lower_with_under   | lower_with_under                                                     |
| Instance Variables         | lower_with_under   | \_lower_with_under (protected) or \_\_lower_with_under (private)     |
| Method Names               | lower_with_under() | \_lower_with_under() (protected) or \_\_lower_with_under() (private) |
| Function/Method Parameters | lower_with_under   |
| Local Variables            | lower_with_under   |

#### 应该避免的名称

1. 单字符名称
2. 包/模块名中使用连字符(-)而不使用下划线(\_)
3. 双下划线开头并结尾的名称（如**init**）

#### 命名约定

1. 所谓“内部(Internal)”表示仅模块内可用, 或者, 在类内是保护或私有的.
2. 用单下划线(\_)开头表示模块变量或函数是 protected 的(使用 import \* from 时不会包含).
3. 用双下划线(\_\_)开头的实例变量或方法表示类内私有.
4. 将相关的类和顶级函数放在同一个模块里. 不像 Java, 没必要限制一个类一个模块.
5. 对类名使用大写字母开头的单词(如 CapWords, 即 Pascal 风格), 但是模块名应该用小写加下划线的方式(如 lower_with_under.py).

#### 注释规范

##### 文档字符串

Python 使用文档字符串作为注释方式: 文档字符串是包, 模块, 类或函数里的第一个语句. 这些字符串可以通过对象的 doc 成员被自动提取, 并且被 pydoc 所用. 我们对文档字符串的惯例是使用三重双引号"""( PEP-257 ).

一个文档字符串应该这样组织:

1. 首先是一行以句号, 问号或惊叹号结尾的概述(或者该文档字符串单纯只有一行). 接着是一个空行.
2. 接着是文档字符串剩下的部分, 它应该与文档字符串的第一行的第一个引号对齐.

```python
"""A user-created :class:`Response <Response>` object.

Used to xxx a :class: `JsonResponse <JsonResponse>`, which is xxx

:param data: response data
:param file: response files

Usage::

    >>> import api
    >>> rep = api.Response(url="http://www.baidu.com")
"""
```

#### 行内注释(PEP8)

行内注释是与代码语句同行的注释

1. 行内注释和代码至少要有两个空格分隔
2. 注释由#和一个空格开始

```python
x = x + 1                 # Compensate for border
```

#### 模块

每个文件应该包含一个许可样板. 根据项目使用的许可(例如, Apache 2.0, BSD, LGPL, GPL), 选择合适的样板.

```python
# -*- coding: utf-8 -*-
# (C) JiaaoCap, Inc. 2017-2018
# All rights reserved
# Licensed under Simplified BSD License (see LICENSE)
```

#### 函数和方法

一个函数必须要有文档字符串, 除非它满足以下条件:

1. 外部不可见
2. 非常短小
3. 简单明了
   文档字符串应该包含函数做什么, 以及输入和输出的详细描述
   文档字符串应该提供足够的信息, 当别人编写代码调用该函数时, 他不需要看一行代码, 只要看文档字符串就可以了
   对于复杂的代码, 在代码旁边加注释会比使用文档字符串更有意义.

```python
def simple_func(method, timeout)
    """Constructs and sends a :class:`Request <Request>`.

    :param method: method for the new :class:`Request` object.
    :param timeout: (optional) How many seconds to wait for the server to send data
        before giving up, as a float, or a :ref:`(connect timeout, read
        timeout) <timeouts>` tuple.
    :type timeout: float or tuple
    :return: :class:`Response <Response>` object
    :rtype: requests.Response

    Usage::

      >>> import requests
      >>> req = requests.request('GET', 'http://httpbin.org/get')
      <Response [200]>
    """
```

#### 类

类应该在其定义下有一个用于描述该类的文档字符串. 如果你的类有公共属性(Attributes), 那么文档中应该有一个属性(Attributes)段. 并且应该遵守和函数参数相同的格式.

```python
class HTTPAdapter(BaseAdapter):
    """The built-in HTTP Adapter for urllib3.

    Provides a general-case interface for Requests sessions to contact HTTP and
    HTTPS urls by implementing the Transport Adapter interface.

    :param pool_connections: The number of urllib3 connection pools to cache.
    :param max_retries: The maximum number of retries each connection
        should attempt.

    Usage::

      >>> import requests
      >>> s = requests.Session()
      >>> a = requests.adapters.HTTPAdapter(max_retries=3)
      >>> s.mount('http://', a)
    """

    def __init__(self, pool_connections, max_retries):
        self.pool_connections = pool_connections
        self.max_retries = max_retries
```

#### 块注释和行注释

对于复杂的操作, 应该在其操作开始前写上若干行注释. 对于不是一目了然的代码, 应在其行尾添加注释.

```python
# We use a weighted dictionary search to find out where i is in
# the array.  We extrapolate position based on the largest num
# in the array and the array size and then do binary search to
# get the exact number.

if i & (i-1) == 0:        # true iff i is a power of 2
```

#### 行长度

1. 每行不超过 80 个字符
2. 不要使用反斜杠连接行
3. Python 会将 圆括号, 中括号和花括号中的行隐式的连接起来 , 你可以利用这个特点. 如果需要, 你可以在表达式外围增加一对额外的圆括号.
   NO:

```python
query_sql = "SELECT image_id, image_o, image_width, image_height "\
            "FROM active_image_tbl "\
            "WHERE auction_id=:auction_id AND status=1 " \
            "ORDER BY image_id DESC"
```

YES:

```python
agent_sql = ("CREATE TABLE IF NOT EXISTS db_agent ("
             "id INTEGER PRIMARY KEY AUTOINCREMENT, "
             "device_id VARCHAR(128) DEFAULT '', "
             "status INTEGER DEFAULT 1, "
             "updated_time TIMESTAMP  DEFAULT CURRENT_TIMESTAMP, "
             "created_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP)")
```

在注释中，如果必要，将长的 URL 放在一行上。

Yes:

```python
# See details at
# http://www.example.com/us/developer/documentation/api/content/v2.0/fication.html
```

#### 换行

1. 使用 4 个空格来缩进代码
2. 对于行连接的情况, 你应该要么垂直对齐换行的元素, 或者使用 4 空格的悬挂式缩进(这时第一行不应该有参数):

```python
# 垂直对齐换行的元素
foo = long_function_name(var_one, var_two,
                         var_three, var_four)
```

```python
# 4空格的悬挂式缩进(这时第一行不应该有参数)
foo = long_function_name(
    var_one, var_two, var_three,
    var_four)
```

#### 空格

- 括号内不要有空格

YES:

```python
spam(ham[1], {eggs: 2}, [])                 # 注意标点两边的空格
```

NO:

```python
spam( ham[ 1 ], { eggs: 2 }, [ ] )
```

- 不要在逗号，分号，冒号前面加空格，而应该在它们的后面加

YES:

```python
if x == 4:
    print x, y
x, y = y, x
```

NO:

```python
if x == 4 :
   print x , y
x , y = y , x
```

- 二元操作符两边都要加上一个空格（=， ==，<, >, !=, in, not ...）
- 当’=’用于指示关键字参数或默认参数值时

```python
def complex(real, imag=0.0):
    return magic(r=real, i=imag)
```

- 不要用空格来垂直对齐多行间的标记, 因为这会成为维护的负担(适用于:, #, =等)

YES:

```python
foo = 1000  # comment
long_name = 2  # comment that should not be aligned
```

NO:

```python
foo       = 1000  # comment
long_name = 2     # comment that should not be aligned
```

#### 模块导入

- 每个导入应该独占一行

YES:

```python
import os
import sys
from subprocess import Popen, PIPE      # PEP8
```

NO:

```python
import sys, os
```

- 模块导入顺序
  a. 标注库导入
  b. 第三方库导入
  c. 应用程序指定导入

- 每种分组中, 应该根据每个模块的完整包路径按字典序排序, 忽略大小写.

```python
import foo
from foo import bar
from foo.bar import baz
from foo.bar import Quux
from Foob import ar
```

#### TODO 注释

1. TODO 注释应该在所有开头处包含”TODO”字符串, 紧跟着是用括号括起来的你的名字, email 地址或其它标识符. 然后是一个可选的冒号. 接着必须有一行注释, 解释要做什么
2. 如果你的 TODO 是”将来做某事”的形式, 那么请确保你包含了一个指定的日期(“2009 年 11 月解决”)或者一个特定的事件

```python
# TODO(kl@gmail.com): Use a "*" here for string repetition.
# TODO(Zeke) Change this to use relations.
```

#### 二元运算符换行(PEP8)

```python
# 不推荐: 操作符离操作数太远
income = (gross_wages +
          taxable_interest +
          (dividends - qualified_dividends) -
          ira_deduction -
          student_loan_interest)
```

```python
# 推荐：运算符和操作数很容易进行匹配
income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction
          - student_loan_interest)
```

### 其它规范

1. 不要在行尾加分号, 也不要用分号将两条命令放在同一行.
2. 除非是用于实现行连接, 否则不要在返回语句或条件语句中使用括号. 不过在元组两边使用括号是可以的.
3. 顶级定义之间空两行, 方法定义之间空一行

#### Pandas 使用规范

1. pandas 数据结构命名 df*、se*
2. df 取一列，禁止使用 df.列名，可以使用 df['列名'], 建议使用 df.loc[:, '列名']
3. 禁止使用 df.ix

#### 目录结构示例

```
|--docs
|--requests
|    |--__init__.py
|    |--_internal_utils.py
|    |--utils.py
|    |--api.py
|--tests
|--setup.py
|--README.rst
|--LICENSE
```

#### Class 结构示例

```python
# -*- coding: utf-8 -*-
# (C) JiaaoCap, Inc. 2017-2018
# All rights reserved
# Licensed under Simplified BSD License (see LICENSE)

"""
requests.api

This module contains xxx.
This module is designed to xxx.
"""

# stdlib
import os
import time

from base64 import b64encode

# 3p
try:
    import psutil
exception ImportError:
    psutil = None
import simplejson as json

# project
from .utils import current_time
from ._internal_utils import internal_func


class Response(object):
    """A user-created :class:`Response <Response>` object.

    Used to xxx a :class: `JsonResponse <JsonResponse>`, which is xxx

    :param data: response data
    :param file: response files

    Usage::

        >>> import api
        >>> rep = api.Response(url="http://www.baidu.com")
    """

    def __init__(self, data, files, json, url)
        self.data = data

    @staticmethod
    def _sort_params(params):
        """This is a private static method"""
        return params

    def to_json():
        """The fully method blala bian shen,
        xxx sent to the server.

        Usage::

            >>> import api
            >>> rep = api.Response(url="http://www.baidu.com")
            >>> rep.to_json()
        """

        if self.url == "www":
            return True
        return False
```

### 相关链接

- Google 开源项目风格指南: https://zh-google-styleguide.readthedocs.io/en/latest/
- PEP 8 -- Style Guide for Python Code: https://www.python.org/dev/peps/pep-0008/
- Python PEP8 编码规范中文版: https://blog.csdn.net/ratsniper/article/details/78954852
