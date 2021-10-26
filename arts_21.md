1. algorithm

2. review

   https://sematext.com/blog/log-analysis-tools/

   介绍log analysis tool，但好像大部分都是收费的。

3. tips git rename file

   ```
   git mv original_file_name new_file_name
   ```

4. share how to get string list from json file

   因为ecpri-64的环境有多个，我想配置在json文件中，然后再从Jenkinsfile里去取，我最开始写的是:

   ```json
   "ecpri-64":"10.101.34.162, 10.101.34.163"
   ```

   这样得到的是字符串，我看网上可以直接得到一个list，但我用下面的代码打印出来的每个list的元素是一个数字：

   ```groovy
   def slave_list = data[ "ecpri-64" ]
   slave_list.each { single_slave ->
   println "single_slave is "+single_slave
   }
   ```

   后来我看有个示例里的json是这样的：

   ```json
   tags: [ "person", "employee"],
   ```

   stackoverflow上有个帖子也说在json里[]里是array,{}里是对象。我就改成了下面这个样子：

   ```json
   "ecpri-64":["10.101.34.162, 10.101.34.163"]
   ```

   但还是不行，得到的结果还是字符串，我还怀疑是JsonSlurperClassic的问题，是不是它解析出来就解析成字符串了，还在想这个类也太不负责任了吧...后来发现是格式没写对，对比了一下示例里的，改成这样就可以了，我还怀疑人家类有问题，是不是太搞笑了。

   ```json
   "ecpri-64": ["10.101.34.162", "10.101.34.163"],
   ```


