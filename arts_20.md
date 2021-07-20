1. algorithm

2. review

3. tips get type of groovy var

   ```
   println obj.getClass()
   ```

4. share how to read config from json file in jenkins pipeline

   本来想用Pipeline Utility Steps这个插件，但是tt不在，就想试着直接用groovy读。最开始的代码是这样的：

   ```groovy
   def jsonSlurper = new JsonSlurper()
   data = jsonSlurper.parse(new File(filename))
    
   println(data)
   ```

   但报的错是找不到文件，文件是在的。查了下好像没有权限访问node上的文件，要用readFile这个step。就改成了这样:

   ```groovy
   def jsonSlurper = new JsonSlurper()
   data = jsonSlurper.parse(readFile(filename))
    
   println(data)
   ```

   又报java.io.NotSerializableException的错误。最后改成了另外一个解析类，并且加了@NonCPS，下面这个样子的:

   ```groovy
   data = jsonParse(readFile("${env.WORKSPACE}/jenkins-pipeline-build/component-compile/env.json"))
   
   @NonCPS
   def jsonParse(def json) {
       new groovy.json.JsonSlurperClassic().parseText(json)
   }
   ```
