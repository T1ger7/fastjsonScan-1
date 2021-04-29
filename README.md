#### 更新v3.8
 支持<=1.2.47的不出网检测方案！！！！其中有SpringEcho方案，有DelayTest方案。不出网利用链有3条:dbcp,ibatis和TemplatesImpl，其中TemplatesImpl几乎遇不到，但是也加着。TomcatEcho依然没有，我太菜了，没构造成功，不过暂时DelayTest够用了。

## fastjsonScan
fastjson漏洞burp插件，检测fastjson&lt;=1.2.47基于dnslog和fastjson 1.2.24 的不出网2种TomcatEcho回显方案，使用ysoserial的tomcatEcho回显方案

附带fastjson1.2.47.tar.gz的web，解压到tomcat 的webapps，和fastjson 1.2.24的jar包，替换1.2.47的jar就能测试1.2.24。



### 自己编写的burp插件
 1.fastjson =< 1.2.47 反序列化漏洞检测
   无法检测没有外网的主机，默认使用rmi协议。
   
#### FastjsonScan 更新
 1.在原来的被动扫描上支持主动扫描，由于主动扫描发送数据包较多，故会多次扫描。
 2. 在原来的rmi协议上支持ldap协议。
 3. 支持fastjson 1.2.47 SpringEcho ,检测后，发送到Repeater 中，便可以利用。
 4. 支持fastjson<= 1.2.47 的延时检测。
  ##### 4. 存在攻击行为，非法使用后果自负！！！！
 5. 为防止被动检测多次扫描，同一url被动检测一次，如果重新检测，需要重新加载插件或重启burp，主动扫描可以检测多次，目前主动扫描不会tomcatEcho。
 ##### 6. 加入1.2.24-1.2.68 dnslog检测方案。
 
#### 用法：
  加到burp插件就行了，流量经过burp就检测。结果在ISSUES中看到，如果是fastjson 1.2.24的话，自动发送结果到Repeater如下图。
#### FastjsonExploit.jar
  打包大佬的代码，大佬地址：https://github.com/c0ny1/FastjsonExploit
  
#### 注意：
   只检测post，且类型是application/json
 
##### 如下图：
检测结果ISSUES中看到：

![](%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20210119112911.png)

fastjson1.2.24自动发到Repeater 回显结果，添加Testcmd头执行命令：

![](%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20210118170804.png)

一键反弹shell：
![](%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20210118174907.png)

加入第二种回显方案：
也是自动检测，存在的话会发送到repeater中，如图，修改echo:test和Testcmd:命令：
![](微信截图_20210402211015.png)
