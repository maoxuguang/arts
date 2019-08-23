1. algorithm

2. review

   <https://sourcemaking.com/refactoring/introduce-parameter-object>

   这是代码里pipeline调用pybot.bat的时候，传参太多，我搜索搜到的。虽然和我的情况还不太一样，这个文章主要讲的是函数参数太多的时候怎么重构。最后我的解决方法是从环境变量里去取JOB_NAME, 这个是jenkins的环境变量里本来就有的，好歹减少了一个参数。

3. tips

   ```java
   def made_url = artifactory_root+compile_job+"/"+build_number+"/"+"${env.tarFile}"
   ```

   这是pipeline的script step遇到的问题，引用环境变量用${env.tarFile}不行，要加上双引号，好像单引号也不行...

4. share python: SyntaxError: EOL while scanning string literal

   EOL: end of line. a special character or sequence of characters signifying the end of a line of text in computing

   遇到这个问题的时候查了下以为是字符串中有特殊符号/，但是后来发现只有一个字符没有特殊字符的时候也报这个错误，后来发现是后面有个回车，因为回车不显示所以比较难发现。而且后来查了下EOL本来就是结束符的意思。