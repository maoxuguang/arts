

algorithm

1. review re-throw exception in python

   <https://nedbatchelder.com/blog/200711/rethrowing_exceptions_in_python.html>

   我想把捕捉到的异常再原封不动的抛出去，查到了这个，很简单，直接用raise就是"throw the exception last caught"

   ```python
   try:
       do_something_dangerous()
   except:
       do_something_to_apologize()
       raise
   ```

2. tips  用wireshark抓包分析

   ![1574233426844](.\wireshark1.png)

   ![1574233606169](.\wireshark2.png)

   ![1574233780094](.\wireshark3.png)

3. share python的try except

   最近在代码中要用socket接收两条消息，又没办法判断什么时候结束，就用了timeout，于是用到了except。我原来以为except后面跟的是exception的type，还特意打印了exception的type：

   ```python
   try:
       someFunction()
   except Exception as ex:
       template = "An exception of type {0} occurred. Arguments:\n{1!r}"
       message = template.format(type(ex).__name__, ex.args)
       print message
   ```

   然后发现type是timeout,更新代码后发现不行:

   ```python
   try:
       someFunction()
   except 'timeout':
       ...
   ```

   查了下，更新成这个样子就可以了:

   ```python
   try:
       someFunction()
   except socket.timeout:
       ...
   ```

   所以这里跟的可能是Class吧。文档里是这样写的：

   ```
    A class in an except clause is compatible with an exception if it is the same class or a base class thereof (but not the other way around — an except clause listing a derived class is not compatible with a base class). 
   ```

​       另外还想在除了timeout异常之外的其他异常发生的时候把异常抛出去，我是这样写的:

        ```python
try:
​    someFunction()
except socket.timeout:
​    somecode
else:
​    raise Exception("some unexpected errors occurred")
​        ```

发现执行结果不对，else并不是处理其他的异常的，而是处理没有异常发生的情况。文档中是这么写的:

```
The try … except statement has an optional else clause, which, when present, must follow all except clauses. It is useful for code that must be executed if the try clause does not raise an exception.
```

最后的代码是这个样子的

```python
try:
    someFunction()
except socket.timeout:
    somecode
except:
    raise Exception("some unexpected errors occurred")
```

