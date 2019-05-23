1. algorithm

2. review

   <https://gerrit-review.googlesource.com/Documentation/rest-api-changes.html#get-change>

   编译的bb文件里用到commit id，jenkins的gerrit插件里好像没有这个变量，搞不懂gerrit里面change-id和commit id的关系。看了下文档，change-id主要是把一次review的commit收集在一起，一个change-id可以对应几个通过amend添加的commit. 一次commit就是一个patch set.其实gerrit里面也是有这个变量的:

   ```
   GERRIT_PATCHSET_REVISION
   ```

3. tips

   Mysql 数据库表的字段设置了NOT NULL, 但是插入和更新的时候却可以让该字段为空，查了下是因为Mysql里面的sql_mode设置non-strict的原因，可以通过下面的命令查询sql_mode:

   ```sql
   SELECT @@GLOBAL.sql_mode;
   ```

4. shares python unhashable

   是极客时间python课程的课后题，题目是是否可以用列表作为字典的键值，在Jupyter上试了试，报的错试unhashable type. 为什么列表，可变的数据就是unhashable的呢，查了下, 在生命周期内不可变的对象才有个哈希值，才是可哈希的。我还理解错题目了，键值是key，有个值我脑子里给想成了value，试了下value是可以是列表的，key不行，因为要对key哈希存储。

   <https://stackoverflow.com/questions/14535730/what-does-hashable-mean-in-python>

   ```
   An object is hashable if it has a hash value which never changes during its lifetime (it needs a __hash__() method), and can be compared to other objects (it needs an __eq__() or __cmp__() method). Hashable objects which compare equal must have the same hash value.
   
   Hashability makes an object usable as a dictionary key and a set member, because these data structures use the hash value internally.
   
   All of Python’s immutable built-in objects are hashable, while no mutable containers (such as lists or dictionaries) are. Objects which are instances of user-defined classes are hashable by default; they all compare unequal, and their hash value is their id().
   ```


