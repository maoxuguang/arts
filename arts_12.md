1. algorithm

2. review

   <https://sourcemaking.com/refactoring/introduce-parameter-object>

   这是代码里pipeline调用pybot.bat的时候，传参太多，我搜索搜到的。虽然和我的情况还不太一样，这个文章主要讲的是函数参数太多的时候怎么重构。最后我的解决方法是从环境变量里去取JOB_NAME, 这个是jenkins的环境变量里本来就有的，好歹减少了一个参数。

3. tips

   ```java
   def made_url = artifactory_root+compile_job+"/"+build_number+"/"+"${env.tarFile}"
   ```

   这是pipeline的script step遇到的问题，引用环境变量用${env.tarFile}不行，要加上双引号，好像单引号也不行...