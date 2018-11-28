# ChinesePersonRelationGraph
ChinesePersonRelationGraph, person relationship extraction based on nlp methods.中文人物关系知识图谱项目,内容包括中文人物关系图谱构建,基于知识库的数据回标,基于远程监督与bootstrapping方法的人物关系抽取,基于知识图谱的知识问答等应用.

# 项目介绍
知识抽取(实体关系抽取)是知识图谱构建中的核心环节,实体关系抽取作为一项基本技术在自然语言处理应用中扮演着重要作用.
究其技术而言,主要分成两种三种主流方法:    
# 1, 基于规则的方法  
   在工业界大多还是使用的规则模板的方法,这个可以参考我的相关项目:  
   1)https://github.com/liuhuanyong/EventTriplesExtraction, 这是借助依存句法与语义角色标注的方法.       
   2)https://github.com/liuhuanyong/ComplexEventExtraction, 这个项目提供了复合事件的基本模式,可以初步筛选出候选的因果,反转等事件    
   3)https://github.com/liuhuanyong/SequentialEventExtration, 这个项目提供了一种基于VOB模式的顺承事件抽取方法,讲的是一种顺承关系 
   基于规则的方法,升级版的话,就是Bootstrapping了,可以通过用户自定义种子模板,不断迭代,最终扩充模式,但置信度这个问题不是很好解决    #
# 2, 基于学习的方法  
   这个在学术界用的比较多,从机器学习一直演变了到现在的各种深度学习模型,而在这种方法中,通常实体关系抽取问题转换成一个实体关系分类任务去做,主要可以分成一下几种.
   1)基于全监督的实体关系抽取  
   这个全监督,也就是说,基于完全标注数据的一种学习方式,例如著名的实体关系评测Semeval系列,给出了19种关系分类任务,ACE给出了17类的实体关系分类任务.针对这些任务,模型经历了CNN,LSTM,ATTENTION等,这里就不再说明.  
   2)基于噪声数据的远程监督实体关系抽取  
   全监督模型固然很好,但数据是一个很棘手的问题,因此就出现了远程监督的方法,所谓远程监督,个人理解就是已经存在的知识库进行数据回标,然后通过多实例学习进行一种容许噪声的监督方法.不过这种方法准确率不是很高,在NYT这个数据集上,PCNNS等工作都没有达到业业界可以使用的地步.当然,最新出现了联合训练的模型.    
   3)基于规则与学习模型融合的实体关系抽取  
   这种方式,在业界或许是一种出路,例如,将实体关系抽取中的实体识别部分交给学习模型去做序列标注,最后针对实体之间的关系,结合依存句法等语义规则去做,这个在解决实体的多种关系问题,可以去尝试.  
# 3, 当前问题 
但就针对全监督的实体关系抽取任务而言,在英文数据集上已经在刷各种state-of-art,但就中文而言,感觉还是一片贫瘠.在网上搜了很久,最终指搜到COAE2016的一个评测任务,但是,评测集不公开.因此,就抛出了本项目构建的几个初衷:  
1, 中文实体关系抽取数据集很少,能不能构建一个准确率可接受的数据集?    
2, 能不能浅显易懂地把那些"高大上"的远程监督,bootstrapping经历一遍?   
3, 人物关系数据在百科等平台上都有放出,或许可以做为远程监督的先验知识库?    
4, 能否提供一个实时动态更新的人物关系图谱方法?  
# 4,项目任务
因此,本项目将尝试完成以下几个任务:  
1, 完成一定规模的人物关系知识库, 作为公开数据集开放出去  
2, 走一遍实体关系回标,形成一个准确性相对允许的人物关系抽取数据集  
3, 走一遍基于学习方式实体关系抽取,查看一下效果,熟悉一下这个技术流程    
4, 走一便基于Bootstrapping的实体关系抽取,熟悉一下这个技术流程  
5, 基于构建起来的人物关系图谱,完成一个面向人物关系图谱的知识问答  

# 项目架构图
![image](https://github.com/liuhuanyong/ChinesePersonRelationGraph/blob/master/image/project_route.png)


# 人物关系基础知识库
1,收集人名词典  
2,基于人名词典,采集搜狗人物关系图谱数据库  

# 刘备人物关系网
![image](https://github.com/liuhuanyong/ChinesePersonRelationGraph/blob/master/image/person_graph1.png)

2#  韩寒人物关系网
![image](https://github.com/liuhuanyong/ChinesePersonRelationGraph/blob/master/image/rel_graph2.png)

3,人物关系数据库规模

|项目|数量|
|:--:|:--:|
|人物|11024|
|关系对|35995|
|关系类型|1144|

4,人物关系60%

|关系类型|	频次|	频率|	累加频率|
|:--:|:--:|:--:|:--:|
|搭档	|4692|	0.1303478164240471|	0.1303478164240471|
|好友	|3771|	0.10476164018224247|	0.23510945660628957|
|队友	|1758|	0.04883875986220691	|0.2839482164684965|
|朋友	|1681|	0.04669963329258806	|0.3306478497610846|
|丈夫	|1431|	0.03975441715746194	|0.3704022669185465|
|妻子	|1198|	0.03328147571952439	|0.4036837426380709|
|师傅	|986|	0.02739193243693744	|0.4310756750750083|
|儿子	|972|	0.027003000333370376	|0.4580786754083787|
|母亲	|922|	0.02561395710634515	|0.4836926325147239|
|同学	|698|	0.01939104344927214	|0.5030836759639961|
|弟弟	|678|	0.01883542615846205	|0.5219191021224581|
|女儿	|609|	0.01691854650516724	|0.5388376486276253|
|前女友	|594|	0.016501833537059675	|0.555339482164685|
|哥哥	|580|	0.01611290143349261	|0.5714523835981776|
|合作	|573|	0.01591843538170908	|0.5873708189798867|
|前男友|	573|	0.01591843538170908	|0.6032892543615959|

# 回标语料构建
目录地址:EventMonitor  
运行方式:cd EventMonitor , scrapy crawl eventspider  
回标语料举例:

      <霍英东, 霍震宇, 三子>	据此间媒体11日报道，<e1>霍英东</e1>长房三子<e2>霍震宇</e2>再度入禀法院，要求法官颁令兄长霍震霆交出记录<e1>霍英东</e1>所有资产及财务资料的记事本1.0
      <朴宝英, 金秀贤, 绯闻>	【组图】最爱人妻全智贤“初恋”秀智一再插足 <e1>朴宝英</e1>韩佳人T-ara恩静已成往事 <e2>金秀贤</e2>绯闻女友大盘点1.0
      <辰亦儒, 炎亚纶, 飞轮海组合>	飞轮海曾是火遍亚洲的偶像组合，飞轮海四名成员吴尊、汪东城、<e1>辰亦儒</e1>和<e2>炎亚纶</e2>四人也曾是不少人心目中的偶像，象征着我们的一代人的青春1.0
      <唐贝欣, 唐贝诗, 姐姐>	<e1>唐贝欣</e1>在伦敦大学毕业姐姐<e2>唐贝诗</e2>当然捧场1.0
      <刘琳, 刘孜, 同学>	<e2>刘孜</e2>是徐静蕾、<e1>刘琳</e1>的同学，最初是主持综艺节目，后投入影视剧的拍摄1.0
      <高晓松, 沈欢, 第一任妻子>	<e1>高晓松</e1>老婆<e2>沈欢</e2>相识过程：关于<e1>高晓松</e1>和第一任妻子<e2>沈欢</e2>的相识，颇具戏剧性1.0
      <高崚, 张军, 搭档>	<e1>高崚</e1>是国羽历史上的又一位女子兼项英雄，2000年8月，<e1>高崚</e1>搭档<e2>张军</e2>参加悉尼奥运会羽毛球混双比赛中爆冷为中国队夺得了奥运会历史上第一枚混双金牌1.0
      <李行亮, 黄雅莉, 好友>	陈俊彤自出道以来收获了不少圈内好友，<e1>李行亮</e1>、<e2>黄雅莉</e2>等也纷纷为陈俊彤新专辑的推出送上了祝福，他们对于音乐同样的执着和热爱令友谊长存，也令现场火速升温1.0
      <谢坤达, 黄鸿升, 好友>	修杰楷和好友<e2>黄鸿升</e2>、<e1>谢坤达</e1>2017年上《小燕有约》，在小燕姐的追问下侃侃而谈，回忆两人相恋，感性说：“我一直说静雯比我勇敢，她其实要付出的事情，是比我更多1.0
      <张君秋, 王婉华, 弟子>	演出结束后，董雪平、万晓慧拜京剧名家<e1>张君秋</e1>先生弟子<e2>王婉华</e2>、薛亚萍为师1.0
      <霍英东, 霍启山, 孙子>	<e2>霍启山</e2>，1983年5月生，广州人，是<e1>霍英东</e1>的孙子，父亲霍震霆为<e1>霍英东</e1>长子，母亲是港姐冠军朱玲玲，哥哥是霍启刚，弟弟是霍启仁1.0
      <苗侨伟, 苗彤, 女儿>	4.<e1>苗侨伟</e1>女儿<e2>苗彤</e2>1.0
      <万方, 曹禺, 父亲>	知名作家、<e2>曹禺</e2>三女儿<e1>万方</e1>在会后接受专访时表示，自己曾因为父亲在话剧方面的成就而感到压力，直到五十岁才写出第一部话剧作品1.0
      <姜文, 姜一郎, 女儿>	近日，<e1>姜文</e1>女儿<e2>姜一郎</e2>和外国朋友的合影在网络曝光，合影中<e2>姜一郎</e2>长发红唇，很有大腕风范1.0
      <陈建斌, 曹卫宇, 同学>	<e2>曹卫宇</e2>在剧中饰演吴昆才，和大学同学也是多年好兄弟的<e1>陈建斌</e1>有大量对手戏，两人在片场配合十分默契，<e2>曹卫宇</e2>更是大呼和兄弟演戏很过瘾1.0
      <曹敏莉, 曹蕙兰, 妹妹>	<e1>曹敏莉</e1>的妹妹<e2>曹蕙兰</e2>(前名曹敏宝)通过电话访问，激赞未来姐夫爱屋及乌，问她姐姐是否有喜，<e2>曹蕙兰</e2>说：“一定不是，反而大姐姐七月就生了1.0
      <付笛声, 付豪, 儿子>	1992年，任静和<e1>付笛声</e1>的儿子<e2>付豪</e2>出生了，让这个家庭更添了许多的欢乐1.0
      <王洪礼, 王亮, 儿子>	而<e1>王洪礼</e1>的儿子<e2>王亮</e2>也从事了足球职业，并且取得了不错的成绩1.0
      <韩庚, 银赫, sj成员>	出道当时的成员有利特、希澈、<e1>韩庚</e1>、艺声、强仁、神童、晟敏、<e2>银赫</e2>、东海、始源、厉旭和起范1.0
      <刘少奇, 刘允斌, 儿子>	1955年，在俄罗斯已经扎根立足的<e2>刘允斌</e2>接到了父亲的来信，<e1>刘少奇</e1>希望儿子能回到祖国，加入到新中国第1.0
      <丁俊晖, 蔡剑忠, 恩师>	他拥有出众的台球能力，而且很懂事，性格比较开朗，深得教练喜爱，<e1>丁俊晖</e1>昔日恩师<e2>蔡剑忠</e2>[微博]就曾公开表示，“如果袁思俊发展好，未来极有可能追上甚至超越<e1>丁俊晖</e1>的成就1.0
      <郁可唯, 黄英, 同是快女>	搜狐娱乐讯“快女”三强正式出炉！与传闻相符，最后一位离开的选手在同是成都赛区的<e2>黄英</e2>和<e1>郁可唯</e1>之间进行抉择，唱功备受肯定的<e1>郁可唯</e1>最终止步三强，成为今年“快女”第四名1.0
      <王皓, 闫博雅, 妻子>	腾讯体育9月29日讯近日，乒乓名将<e1>王皓</e1>在综艺节目中因与妻子<e2>闫博雅</e2>意见不合而愤然离场，这件事引起不小的轰动1.0
      <蔡康永, 刘坤龙, 同志男友>	<e1>蔡康永</e1>泣诉心酸路感动金星 <e1>蔡康永</e1>男友<e2>刘坤龙</e2>个人资料曝光(图)1.0
      <张晨, 卢卫中, 教练>	多年来，江苏队先后为国家队培养和输送了袁伟民、邹志华、邸安和、曹平、薛永业、张友生、<e2>卢卫中</e2>、陆飞、张晓东、施海荣、陈平、<e1>张晨</e1>等一大批优秀国手和教练，为我国排球事业做出卓越的贡献1.0
      <叶莉, 苗立杰, 好友>	陈楠与<e2>苗立杰</e2>均为姚夫人<e1>叶莉</e1>在女篮国家队中的好友，因此她们与姚明夫妇的关系极佳1.0
      <于震, 辛月, 妻子>	演员<e1>于震</e1>的妻子<e2>辛月</e2>貌美如花【图】1.0
      <马唯中, 周美青, 母亲>	马英九夫人<e2>周美青</e2>几次出境，据了解，<e1>马唯中</e1>趁同行机会，要蔡沛然向她母亲请安1.0
      <康希, 何耀珊, 妻子>	新加坡<e1>康希</e1>等牧者失信案二审 其妻子<e2>何耀珊</e2>被指募资1.0
      <卢燕, 李桂芬, 母亲>	<e1>卢燕</e1>的母亲是京剧名伶<e2>李桂芬</e2>，曾拜梅兰芳为义父，而京剧大师梅兰芳正是第一位将京剧介绍到海外的文化使者，并使京剧跻身于世界戏剧之林1.0
      <李健, 沈梦辰, 经纪人>	记者了解到包括<e2>沈梦辰</e2>在内的《歌手3》(在线观看)芒果经纪人也将加盟《好好学吧》，至于<e2>沈梦辰</e2>会否带着清华哥<e1>李健</e1>一起上节目，备受期待1.0
      <林志玲, 吴慈美, 母亲>	<e1>林志玲</e1>母亲<e2>吴慈美</e2>表示，“她每年都要缴很多税款，应该不会(漏税)吧1.0
      <钱三强, 钱民协, 女儿>	<e1>钱三强</e1>女儿<e2>钱民协</e2>：三钱中两钱曾是邻居1.0
      <杨元龙, 杨敏德, 女儿>	1978年由<e1>杨元龙</e1>创立的香港溢达集团，早在20年前就交班到女儿<e2>杨敏德</e2>的手中1.0
# 
