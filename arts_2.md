1. leetcode

   ```java
   /**
    * Definition for singly-linked list.
    * public class ListNode {
    *     int val;
    *     ListNode next;
    *     ListNode(int x) { val = x; }
    * }
    */
   class Solution {
       public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
           ListNode index1 = l1;
           ListNode index2 = l2;
           ListNode result = new ListNode((l1.val+l2.val)%10);
           ListNode result_index = result;
           int carry = (l1.val+l2.val)/10;
           while (index1.next != null || index2.next != null){
               if(index1.next == null){
                   result.next = new ListNode((index2.next.val+carry)%10);
                   carry = (index2.next.val+carry)/10;
                   index2 = index2.next;
               }else if(index2.next == null){
                   result.next = new ListNode((index1.next.val+carry)%10);
                   carry = (index1.next.val+carry)/10;
                   index1 = index1.next;
               }else{
                   result.next = new ListNode((index1.next.val+index2.next.val+carry)%10);
                   carry = (index1.next.val+index2.next.val+carry)/10;
                   index1 = index1.next;
                   index2 = index2.next;
               }
               result = result.next;
           }
           
           if(index1.next == null && index2.next == null && carry != 0){
                   ListNode carry_over = new ListNode(carry);
                   result.next = carry_over;
               }
           return result_index;
       }
   }
   ```

   2. review

      https://martinfowler.com/eaaDev/EventSourcing.html

      写event sourcing.

      主要的应用场景包括需要事件回放，或者异步通信时收到的信息和发送的顺序不一致。

      后半部分关于实现的细节没有看。好像我们想引入事件回溯的原因和他说的场景不一致。还在迷惑中。

   3. tips curl 重试

      curl -f --retry 3 -s $link

      -f 参数是为了不输出http失败的信息，免得如果后面有管道符需要对curl的结果进一步处理的时候有影响。

      --retry 后面跟的是需要重试的次数。

      -s silent 不输出那些下载过程等信息

   4. share 

      怎样在应用间传递复杂的数据

      因为jenkins只有基本的数据类型，我们从Django触发的时候需要传复杂的参数过去，原来采用的是在jenkins的shell脚本里调用Django的api, 但因为之前出现过api调用失败，拿不到数据，这周要求把api去掉，直接把参数传给shell，其实我不太喜欢这种做法，我觉得就用api传就很好，拿不到如果是网络问题，可以重试，如果是负载问题，可以解决负载的问题，但同事又说有时候是调用api的时候访问数据库的连接也有问题，这个没有办法通过重试解决。最终还是决定了从Django直接传给jenkins.

      但有个麻烦是数据比较复杂，嵌套好几层，jenkins又接收不了这种复杂的数据，现在的做法是把复杂的数据通过base64封装，传给jenkins, shell里再解码，感觉也很奇怪啊。

      你们有更好的解决办法吗？