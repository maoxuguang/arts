1. algorithm

2. review

   https://stackoverflow.com/questions/42295921/what-is-the-effect-of-noncps-in-a-jenkins-pipeline-script

   https://en.wikipedia.org/wiki/Continuation-passing_style

   jenkins pipeline里用到@NonCPS然后搜了下，看不懂....

3. tips how to create methods in jenkins declarative pipeline?

   just outside pipeline {}

4. share how to get downstream job build number without waiting?

   我最开始用的搜素关键词是：

   ```
   jenkins pipeline schedule another job show build number
   ```

   没找到答案，试着搜 jenkins pipeline get build number然后自动联想里面有下面一条：

   ```
   jenkins pipeline get build number of downstream job
   ```

   这不正是我想表达的意思嘛，我已经陷进用build job:, schedule job的思路里来搜索了。搜到的结果是：

   ```
   def triggeredBuild = build job: 'draco/test-pipeline', parameters: [string(name: 'Slave_Label', value: "10.101.34.162")], wait: true
   buildNumber = triggeredBuild.getNumber()
   ```

   然后发现triggeredBuild是null，后来在其他答案里发现wait要设为true。然后搜索：

   ```
   jenkins pipeline how to get downstream build number when wait false
   ```

   在下面这篇文章里发现wait false是不可能得到build number呢，因为那时候job可能还没触发起来，还没分配到build number.

   https://issues.jenkins.io/browse/JENKINS-31392



   今天早上在淘宝搜香港苹果id充值，找到的都是100，150起充，换了个关键词礼品卡，终于找到一个20起充的。就换关键词，换思路尝试很重要。
