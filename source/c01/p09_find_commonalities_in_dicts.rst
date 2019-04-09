=============================
1.9 查找两字典的相同点 Finding Commonalities in Two Dictionaries
=============================

----------
问题
----------
怎样在两个字典中寻寻找相同点（比如相同的键、相同的值等等）？
You have two dictionaries and want to find out what they might have in common (same
keys, same values, etc.).

----------
解决方案
----------
考虑下面两个字典：
Consider two dictionaries

.. code-block:: python

    a = {
        'x' : 1,
        'y' : 2,
        'z' : 3
    }

    b = {
        'w' : 10,
        'x' : 11,
        'y' : 2
    }

为了寻找两个字典的相同点，可以简单的在两字典的 ``keys()`` 或者 ``items()`` 方法返回结果上执行集合操作。比如：

.. code-block:: python

    # Find keys in common
    a.keys() & b.keys() # { 'x', 'y' }
    # Find keys in a that are not in b
    a.keys() - b.keys() # { 'z' }
    # Find (key,value) pairs in common
    a.items() & b.items() # { ('y', 2) }

这些操作也可以用于修改或者过滤字典元素。
比如，假如你想以现有字典构造一个排除几个指定键的新字典。
下面利用字典推导来实现这样的需求：

.. code-block:: python

    # Make a new dictionary with certain keys removed
    c = {key:a[key] for key in a.keys() - {'z', 'w'}}
    # c is {'x': 1, 'y': 2}

----------
讨论
----------
一个字典就是一个键集合与值集合的映射关系。
字典的 ``keys()`` 方法返回一个展现键集合的键视图对象。
键视图的一个很少被了解的特性就是它们也支持集合操作，比如集合并、交、差运算。
所以，如果你想对集合的键执行一些普通的集合操作，可以直接使用键视图对象而不用先将它们转换成一个 set。

字典的 ``items()`` 方法返回一个包含 (键，值) 对的元素视图对象。
这个对象同样也支持集合操作，并且可以被用来查找两个字典有哪些相同的键值对。

尽管字典的 ``values()`` 方法也是类似，但是它并不支持这里介绍的集合操作。
某种程度上是因为值视图不能保证所有的值互不相同，这样会导致某些集合操作会出现问题。
不过，如果你硬要在值上面执行这些集合操作的话，你可以先将值集合转换成 set，然后再执行集合运算就行了。
A dictionary is a mapping between a set of keys and values. The keys() method of a
dictionary returns a keys-view object that exposes the keys. A little-known feature of
keys views is that they also support common set operations such as unions, intersections,
and differences. Thus, if you need to perform common set operations with dictionary
keys, you can often just use the keys-view objects directly without first converting them
into a set.
The items() method of a dictionary returns an items-view object consisting of (key,
value) pairs. This object supports similar set operations and can be used to perform
operations such as finding out which key-value pairs two dictionaries have in common.
Although similar, the values() method of a dictionary does not support the set oper‐
ations described in this recipe. In part, this is due to the fact that unlike keys, the items
contained in a values view aren’t guaranteed to be unique. This alone makes certain set
operations of questionable utility. However, if you must perform such calculations, they
can be accomplished by simply converting the values to a set first
