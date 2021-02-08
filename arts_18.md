1. algorithm

2. review

3. tips wireshark通过端口过滤:

   udp.port==13001

4. share route和traceroute

   最近收不到MRA，debug的时候常用到route和traceroute这个命令。似懂非懂，下面是通和不通的命令结果对比。第一个是ping 192.168.254.225不通的。所以收不到MRA。我刚开始还用wireshark抓包了，发现过滤不到13001这个端口的数据。就是说MRI已经发出，但是server并没有收到MRI。说明server和rru之间不通。192.168.254.225是BBU分给RRU的IP。那其实不用抓包，直接traceroute和ping这个IP都能发现通路不通，所以收不到MRA。

   ```shell
   [root@Server-PreSmoke-01 ~]# traceroute 192.168.254.225
   traceroute to 192.168.254.225 (192.168.254.225), 30 hops max, 60 byte packets
    1  192.168.255.1 (192.168.255.1)  0.391 ms  0.277 ms  0.191 ms
    2  192.168.253.30 (192.168.253.30)  0.764 ms  0.663 ms *
    3  192.168.253.30 (192.168.253.30)  3079.133 ms !H  3079.083 ms !H  3078.993 ms !H
    
    [root@Server-PreSmoke-01 ~]# traceroute 192.168.254.225
   traceroute to 192.168.254.225 (192.168.254.225), 30 hops max, 60 byte packets
    1  192.168.255.1 (192.168.255.1)  0.483 ms  0.246 ms  0.282 ms
    2  192.168.253.30 (192.168.253.30)  0.811 ms  0.665 ms  0.566 ms
    3  192.168.254.225 (192.168.254.225)  1.351 ms  1.228 ms  1.039 ms
   ```
