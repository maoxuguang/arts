1. algorithm

2. review

3. tips robot的Run Keyword If    ELSE

   ```rob
   Run Keyword If    '${BRANCH}' == 'cci_Branch'    Power Reset With PSU    ELSE    Power Reset
   ```

4. share jenkins pipeline sh 的变量解析

   这个地方坑好多。最近的一次是我在sh里的变量名和外面groovy脚本里的变量名一样，本来就是同样的变量，在groovy里组装成map，在sh里再解析出来，我想着反正局部变量同名也不影响。结果发现devtool明明运行了两次却只有一次生效了。后来发现是我没有在sh的变量名前面加\转义，jenkins会在sh执行前先解析变量，我没有加转义符，它就把变量解析成了外层groovy里同名变量的值。所以for循环并没有用，因为里面的变量的值已经提前解析固定了。

   ```shell
   for component in \${component_array[@]}
   do
       component_info=`echo \$component|sed 's#^\\[##'|sed 's#^ ##'|sed 's#\\]\$##'`
       echo \$component_info
       component_name_devtool=`echo \$component_info|cut -d ":" -f1`
       cherry_pick_cmd_devtool=`echo \$component_info|cut -d ":" -f 2-`
       devtool modify \${component_name_devtool} \${component_name_devtool}_local
   done
   ```

   如果sh里有``，有些特殊符号还要转义不止一次。比如我想用sed去掉变量开头的"["，应该是因为"["是正则表达式里的元字符，要转义一次，命令符要转义一次，所以转义两次。

   ```shell
   component_info=`echo \$component|sed 's#^\\[##'|sed 's#^ ##'|sed 's#\\]\$##'`
   ```

   再补充一点，在shell里，单引号会剥夺所有字符的特殊含义，双引号中会保留参数替换$和命令替换`这两个特殊字符。

