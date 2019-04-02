1. algorithm

2. review

   <https://www.cloudbees.com/blog/taming-jenkins-json-api-depth-and-tree>

   这篇文章主要是讲怎么通过depth和tree参数，从jenkins api 返回指定的数据。可以通过tree这个参数指定你想要的element和field. subelement可以嵌套。

   ```
   tree=keyname[field1,field2,subkeyname[subfield1]] 
   ```

   在网上查到的结果好像是还可以指定返回的条目。但没查到怎样指定field的值来查询。后来是用xpath实现的。

   ```python
   jenkins_api_url = jenkins_url+"api/xml?&tree=jobs[builds[*]]&xpath=/hudson/job/build[building='true' and fullDisplayName[contains(text(),'" + job_name + "')]]&wrapper=builds"
   ```

3. tip

   通过jquery的addClass()更新circle class失败。通过下面方法更新成功。可能和我们现在用的jquery版本有关

   ```javascript
   $("#status_circle").attr("class",status);
   ```

4. share