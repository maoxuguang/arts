1. algorithm

2. review

3. tips groovy split()和tokenize()的区别

   split()返回的是String[], tokenize()返回的是List，所以tokenize后可以再跟init()取得除最后一个的所有值。

   ```groovy
   env.yaml_file = JOB_NAME.tokenize("-").init().join("-")+".yaml"
   ```

4. share search for how to generate dynamic parallel step in jenkins pipeline

   我看我最开始搜的是Expected a block for parallel，我忘了为什么会搜这个关键字了，可能是从jenkins pipeline parallel stage搜出来的。我想起来了，是报错的信息。

   搜Expected a block for parallel搜到一个帖子的题目是：

   How to define parallel stages of a Jenkinsfile in an external function?

   我觉得这个题目描述的更准确。然后搜这个题目，又搜到了下面这个帖子：

   Dynamic Parallel stages in Jenkins Pipeline outside 'script' block

   在这个帖子里搜到了答案。感觉这两个帖子的题目准确表达了我的想法，我想要的功能，就是在declared pipeline里用一个函数动态生成并行的stage。（我自己为啥表达不出来？）。虽然我最后也没用这种方案，用了worker。另起一个job.这个也源于grooming的时候我说纠结要不要另起一个job，好处是cosole load会快，分析问题也更清楚，坏处是多了一个job可能会显得更复杂，而且每次build会多用一个slave，我们现在资源比较紧张。PO说那哪个因素影响更严重，我好像立马就知道了答案，那肯定是前者啊，如果我们资源充足，我肯定毫不犹豫的直接用worker了。竟然纠结了这么久。。。。
