1. algorithm

2. review

   <https://jenkins.io/doc/book/pipeline/>

   jenkins pipeline的简单介绍。pipeline的优势，什么是declarative pipeline和scripted pipeline. 现在应该主要用declarative pipeline吧，scripted pipeline好像是最外层是node,又看了下，最外层的这个node不是必需的. declarative pipeline最外层是pipeline.

   但是这个文章对scripted pipeline的介绍好像很不全面，在其他的文档里看到的解释是一种以groovy为基础的DSL语言:

   ```
   Scripted Pipeline is a domain-specific language based on Groovy, most Groovy syntax can be used in Scripted Pipeline without modification.
   ```

   而pipeline中的script step是加进declarative pipeline的一小段scripted pipeline:

   ```
   The script step takes a block of Scripted Pipeline and executes that in the Declarative Pipeline. For most use-cases, the script step should be unnecessary in Declarative Pipelines, but it can provide a useful "escape hatch." script blocks of non-trivial size and/or complexity should be moved into Shared Libraries instead.
   ```

   script step好像是由各个jenkins plugin提供的:

   ```
   The following plugins offer Pipeline-compatible steps.
   ```

3. tips

   jenkins 获取在folder中的job的方法是

   ```
   def buildNumber = Jenkins.instance.getItemByFullName('job_name').lastSuccessfulBuild.number
   ```

   获取不在folder中的job的方法是

   ```
   def buildNumber = Jenkins.instance.getItem('jobName').lastSuccessfulBuild.number
   ```

4. share google搜索

   tips里的问题，我的搜索过程是：

   ```
   Jenkins.instance.getItem contains / in job name
   Jenkins.instance.getItem contains slash in job name
   jenkins getItem  slash in job name
   jenkins getitem job in folder
   ```

   在搜“jenkins getItem  slash in job name”的时候看到有个问题是关于$JOB_NAME inside a folder. 于是搜了"jenkins getitem job in folder"就找到正确答案了。slash in name是问题的呈现，我感觉是因为名字里forward slash所以getItem拿不到，job in folder是问题产生的原因，正因为job是在folder里面的，才导致job的名字中有slash.

   总结：

   ```
   尝试不同的角度，不同的表述方式搜索，除了搜索问题的表现，也搜索问题产生的根源
   扩大或者缩小搜索范围，扩大搜索范围可以发现其他人搜索时不同的表述方式，缩小范围搜到的答案更准确。
   ```


