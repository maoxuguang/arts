1. algorithm

2. review

3. tips 

   **mount相关命令**

   查看mount info的命令：

   ```shell
   cat /proc/mounts
   mount
   mount -l
   df -h
   ```

   mount:

   ```shell
   mount //10.109.3.56/storage-1 /mnt/x
   ```

   un mount

   ```
   umount /mnt/x
   ```

   **生成ssh key直接用这个命令就行：**

   ```shell
   ssh-keygen
   ```

4. share jenkins pipeline sh中的变量赋值

   我之前想在pipeline的sh里通过ls命令把tar的文件名赋值给变量，但是没成功。后面引用的时候总是报错。我记得加了escape符号\也不行。这次又碰到要在sh里给变量赋值，试了试又可以了。

   ```
   pipeline {
       agent any
   
      stages {
          stage('Stage1') {
              steps {
                   sh """
                       cd ${WORKSPACE}
                       mkdir -p test
                       cd test
                       echo "aaaaa">a.txt
                       file_name=`ls *.txt`
                       echo "file_name is \$file_name"
                       mv \$file_name b.txt
                       ls
                   """
               }
           }
       }
   }
   ```

   这是stackoverflow上的解释，就是jenkins pipeline会在执行前解析变量，动态赋值的变量就会报错。在environment里提前定义好的就不会。

   ```
   Another restriction that this poses is that you truly cannot use dynamic variables in the sh portion of the Jenkins declarative pipeline script since Jenkins will first attempt to resolve all variables before execution.
   ```


