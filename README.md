# Jmeter
Jmeter安装与测试


一、Jmeter


jmeter是apache公司基于java开发的一款开源压力测试工具，体积小，功能全，使用方便，是一个比较轻量级的测试工具，使用起来非常简单。因为jmeter是java开发的，所以运行的时候必须先要安装jdk才可以。jmeter是免安装的，拿到安装包之后直接解压就可以使用，同时它在linux/windows/macos上都可以使用。 Jmeter可以做接口测试和压力测试。其中接口测试的简单操作包括做http脚本（发get/post请求、加cookie、加header、加权限认证、上传文件）、做webservice脚本、参数化、断言、关联（正则表达式提取器和处理json-json path extractor）和jmeter操作数据库等等。

二、JDK安装



由于Jmeter是基于java开发，首先需要下载安装JDK，官网下载地址：https://www.oracle.com/java/technologies/javase-downloads.html


(1)下载完成后，使用Xftp软件上传到Linux服务器上：/usr/local/java
执行命令：tar -zxvf  jdk-8u66-linux-x64.tar.gz  解压


(2)配置环境变量
修改/etc/profile文件，执行命令：vi/etc/profile 插入三条进行保存
export JAVA_HOME=/usr/local/java/jdk1.8.0_66
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$JAVA_HOME/bin:$PATH


(3)执行命令：source /etc/profile     刷新环境变量


(4)验证环境变量	java -version 和 javac -version在命令窗口显示java版本信息----配置成功。

三、Jmeter安装


Linux版：


(1)官网下载地址：http://jmeter.apache.org/download_jmeter.cgi

(2)下载完成后，使用Xftp软件上传到Linux服务器上：/user/local/jmeter5

执行命令： tar -zxvf Apache-jmeter-5.2.1.tar.gz 解压

(3)配置Jmeter环境变量 修改/etc/profile文件

export PATH=/usr/local/jmeter/apache-jmeter-5.2.1/bin/:$PATH 

(4)执行命令： source /etc/profile   刷新环境变量

(5)验证环境变量 jmeter -version 	在命令窗口显示jmeter版本信息----配置成功。


Windows版：


(1)官网下载地址：http://jmeter.apache.org/download_jmeter.cgi

(2)下载完成后直接解压

(3)配置好windows下jdk环境变量

(4)进入apache-jmeter-5.2.1\bin目录下双击jmeter.bat运行

四、编写测试计划



(1)在windows版上新建一个测试计划,形成一个jmx文件

(2)添加线程组 Thread Group

Number of Threads：表示线程数，相当于用户

Rame-Up Period(in seconds):表示JMeter每隔多少秒发动一次，如果设置为0，就代表0	秒跑一次，这里边数可以理解为多长时间跑一次（准备时间）

(3)添加http请求 HTTP Request

(4)在http请求中写入接入url、路径、请求方式和参数

(5)添加查看结果树 View Result Tree

(6)添加聚合报告 Assertion Results



五、运行测试脚本

(1)在/user/local/jmeter5下新建一个文件夹，存放jmx文件， mkdir test_jmx

(2)将测试脚本xgjcry.jmx文件上传到/user/local/jmeter5/test_jmx文件夹下

(3)在/user/local/jmeter5下新建一个文件夹，存放jtl测试报告 mkdir jtl

(4)执行命令： jmeter -n -t /usr/local/jmeter5/test_jmx/xgjcry.jmx -l /usr/local/jmeter5/jtl/result.jtl

(5)执行一段时间按ctrl+c结束，这时候jtl文件下会生成测试报告，文件有可能很大，好几十个G，进入/usr/local/jmeter5/jtl文件夹，输入 tar zcvf result.tar result.jtl 压缩成tar包，拷到本地。



六、压测结果查看



本地开启Windows的jmeter，然后点击：创建测试计划，然后点击创建监听--聚合报告，创建查看结果树等等；然后点击GUI界面的浏览，把jtl文件加载进来，就可以看到测试的报告结果了；（具体和报告，查看结果树等等）


聚合报告会显示压测的结果。主要观察Samples、Average、error、Throughput。

Samples:表示一共发出的请求数
	Average：平均响应时间，默认情况下是单个Request的平均响应时间（ms）
  
	Error%:测试出现的错误请求数量百分比。若出现错误就要看服务端的日志，配合开发查找定位原因
  
	Throughput:简称tps,吞吐量，默认情况下表示每秒处理的请求数，也就是指服务器处理能力，tps越高说明服务器处理能力越好。

结果树会显示每次的请求，请求结果，主要看Text和Sampler result
