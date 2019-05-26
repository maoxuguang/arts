1. algorithm

2. review

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