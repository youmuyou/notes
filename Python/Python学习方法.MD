1. 该如何读源码

        谢邀。看到邀请已经很久了，一直没敢回答，主要是我自己没有读过多少模块的源码，因为我一直认为读源码是一种比较“低效”的学方法。
		我用 yolk -al 看了一下安装的模块，发现居然也没有几个算是“读过”的。web.py 的读过一点，它的接口很 pythonic，
		但这货的实现应该算不上是非常pythonic 的代码。
		如果一定要推荐一些 python 的源码去读，我的建议是标准库里关于网络的代码。
		从 SocketServer 开始，补上 socket 模块的知识，熟悉 TCP/UDP 编程，然后了解 Mixin 机制的最佳示例 SocketServer.

		{ForkingMixIn|ThreadingMixIn}，借这个机会了解 thread/threading 模块，这时会对并发量提出新的要求，就可以读 select 模块，
		开始对 select/{epoll|kqueue} 有深刻理解，搞懂以后就可以接触一下异步框架 asyncore 和 asynchat。
		这时开始出现分岔。如果是做 game 等以 TCP/UDP 协议为基础的应用，可以去读 greenlet 和 gevent，
		如果是做 web，则走下一条路。

		做 web，读 BaseHTTPServer、SimpleHTTPServer 和 CGIHTTPServer，读 cgi/cgitb，自己随意写框架，读cookielib，读 wsgiref，
		这时候自己写一个简便的 web framework 就 so easy 了，老板再也不担心你写 web 了，
		选择 flask/web.py/django/pyramid 都心中有数了。因为走的是 web 的路，所以难免要调用一下别人的 api，
		搞懂一下 httplib/urllib/urllib/urlparse。最后，上述提到的标准库，我大多读过。
			著作权归作者所有。
			商业转载请联系作者获得授权，非商业转载请注明出处。
			作者：赖勇浩
			链接：https://www.zhihu.com/question/20336475/answer/16093609
			来源：知乎

2. `.Learning Python, Python Cookbook, PEP-8`
3. [the-best-way-to-learn-python](http://code.tutsplus.com/tutorials/the-best-way-to-learn-python--net-26288)
4. 爬虫可以更新使用的技术

        
		urllib 				 -> requests
		re      			 -> BeautifulSoup, lxml.html,PyQuery
		框架    				-> scrapy
		验证	   				-> PIL, opencv, pybrain
		threading, celery 
        时间处理 			  -> dateutil
        字符串模糊比较		    -> fuzzywuzzy
		监控文件系统  		 -> watchdog
		调用程序     		  -> sh
        数据挖掘    		  -> pattern
        目录        		   -> path.py


著作权归作者所有。
商业转载请联系作者获得授权，非商业转载请注明出处。
作者：罗伊
链接：https://www.zhihu.com/question/33398583/answer/59017861
来源：知乎

更新:讨论区挺热闹，有人说好简单，有人说好难，其实我觉得这只适合面试2~3年工作经验的后端工程师。真的没有问很难的题目，只是可能你平时没有注意。
在这里我推荐几本书吧

	python参考手册，绝对让你更上一层楼
	图解密码技术，密码入门不二之选
	mysql技术内幕第五版，有点厚当手册读读，要有耐心，
	高性能mysql也强烈建议读读effective tcp/ip programming

为什么评论区有这么大差异？我想是个人经历不一样吧，如果是搞web的对操作系统这块和密码技术会偏弱，但如果是系统工程师或是游戏服务端这块会明显偏强。吃午饭的时候我就一直在想这个问题，我觉得重点不是Python而是后端工程师，因为Python只是系统的一部分，linux基础操作要熟吧，sql要懂吧，消息队列要知道吧，git要熟悉吧......木桶理论，每一环都不能落下，精通其中一两环就更好了。

基础功扎实，新东西学得快，代码写得溜，命令敲得顺，bug解的好，妈妈再也不用担心我天天加班了~~~

一.语言   

	1. 推荐一本看过最好的python书籍？ 拉开话题好扯淡 
	2. 谈谈python的装饰器，迭代器，yield？ 
	3. 标准库线程安全的队列是哪一个？不安全的是哪一个？logging是线程安全的吗？ 
	4. python适合的场景有哪些？当遇到计算密集型任务怎么办？ 
	5. python高并发解决方案？我希望听到twisted->tornado->gevent，能扯到golang,erlang更好

二.操作系统 可以直接认为是linux，毕竟搞后端的多数是和linux打交道。 

	1. tcp/udp的区别？tcp粘包是怎么回事，如何处理？udp有粘包吗？ 
	2. time_wait是什么情况？出现过多的close_wait可能是什么原因？ 
	3. epoll,select的区别？边缘触发，水平触发区别？


三. 存储 存储可能包含rdbms，nosql以及缓存等，我以mysql,redis举例  
 		 
		mysql相关 
		1. 谈谈mysql字符集和排序规则？ 
		2. varchar与char的区别是什么？大小限制？utf8字符集下varchar最多能存多少个字符 
		3. primary key和unique的区别？ 
		4. 外键有什么用，是否该用外键？外键一定需要索引吗？ 
		5. myisam与innodb的区别？innodb的两阶段锁定协议是什么情况？ 
		6. 索引有什么用，大致原理是什么？设计索引有什么注意点？ 
		
		

		redis相关 
		1. 什么场景用redis，为什么mysql不适合？ 
		2. 谈谈redis的事务？用事务模拟原子+1操作？原子操作还有其它解决方案吗？ 
		3. redis内存满了会怎么样？


四.安全 

		web安全相关 
		1. sql注入是怎么产生的，如何防止？ 
		2. xss如何预防？htmlescape后能否避免xss? 
		3. csrf是什么？django是如何防范的？ 

		密码技术 
		1. 什么是分组加密？加密模式有哪些？ecb和cbc模式有什么区别？为什么需要iv向量？ 
		2. 简单说说https的过程？ 
		3. 对称加密与非对称加密区别？ 
		4. 如何生成共享秘钥？ 如何防范中间人攻击？

五.杂 

		是否关注新技术啊？golang，rust是否了解？numpy,pandas是啥鸟？ 
		是否紧跟时代潮流？逛不逛微博，刷不刷知乎？ 
		可能你觉得我问的好细，但这好多都是平常经常遇到，并需要解决的，细节更能体现一个人。
		如果你觉得小kiss，欢迎投简历给我yihaibo@longtugame.com，
		龙图游戏运营支持中心数据分析部招人；觉得有点问题，那还等什么，赶快来和我交流交流。



著作权归作者所有。
商业转载请联系作者获得授权，非商业转载请注明出处。
作者：socici
链接：https://www.zhihu.com/question/20170409/answer/14354352
来源：知乎

	1. 服务器os: 比如linux 日常操作肯定要熟悉
	2. webserver : nginx apache tomcat
	3. 存储：myql nosql
	4. 网络相关知识，比如二级域名、负载均衡 智能DNS之类的。
	5. 前端 浏览器缓存 js css 技术6.安全 sql注入 cookie跨域 xss