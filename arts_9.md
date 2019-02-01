1. algorithm

2. review

3. tips

   Mysql 数据库表的字段设置了NOT NULL, 但是插入和更新的时候却可以让该字段为空，查了下是因为Mysql里面的sql_mode设置non-strict的原因，可以通过下面的命令查询sql_mode:

   ```sql
   SELECT @@GLOBAL.sql_mode;
   ```

4. shares