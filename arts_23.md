1. algorithm

2. review

   https://sematext.com/guides/elk-stack/

   https://sematext.com/guides/elasticsearch/

   介绍elk和elasticsearch，elasticserach通过倒排索引提供了强大的全文检索功能。

3. tips 

   **yum command**

   ```shell
   yum search LINSEE_gcc
   yum remove LINSEE_gcc_v490a
   ```

   **ls file size in readable** 

   ```shell
   ls -lh
   ```

   **create new user in linux**

   ```shell
   sudo adduser jenkins
   sudo passwd jenkins
   ```

   **select by columns**

   ```
   Alt+Shift+A
   ```

4. share elk config

   filebeat config file path:

   ```
   /etc/filebeat/filebeat.yml
   
   check log:
   journalctl -u filebeat
   
   /var/lib/filebeat/registry/filebeat
   
   ```

**filebeat配置**

1) 在filebeat的配置文件filebeat.yml里配置log path

```yaml
- type: log

  # Change to true to enable this input configuration.
  enabled: true

  # Paths that should be crawled and fetched. Glob based paths.
  paths:
    - /var/log/jenkins/jenkins.log
    - /var/lib/jenkins/jobs/*/builds/*/log
    #- c:\programdata\elasticsearch\logs\*
```



 2)配置kibana, 用内网IP

```yaml
setup.kibana:
host: "192.168.0.86:5601"
```

 3）配置elasticsearch,用内网IP

```yaml
# ---------------------------- Elasticsearch Output ----------------------------
output.elasticsearch:
  # Array of hosts to connect to.
  hosts: ["192.168.0.86:9200"]
```



**elasticsearch配置，同样用内网IP**

```yaml
network.host: 192.168.0.86
```

配完报了个错说什么discovery.seed_hosts: ["host1", "host2"]配置不对，不能用默认的，google下，增加了下面的字段解决了

```yaml
discovery.type: single-node
```



**kibana配置**，同样用内网IP配置，但要用外网IP访问。还要在openstack把elk用到的端口都配上。

```yaml
server.port: 5601
server.host: "192.168.0.86"
elasticsearch.hosts: ["http://192.168.0.86:9200"]
```



**怎样查看filebeat有没有把log发到elasticsearch?**

在浏览器输入下面的命令就会把index列出来，不知道这个是api还是啥啊

```
http://10.183.227.6:9200/_cat/indices?
```

![1632901532250](C:\Users\xumao\AppData\Roaming\Typora\typora-user-images\1632901532250.png)

还有一个问题是在kibana的discover里没有看到filebeat生成的index，为这个index再create a index pattern就可以了。

