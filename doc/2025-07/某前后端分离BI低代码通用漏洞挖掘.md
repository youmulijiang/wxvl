#  某前后端分离BI低代码通用漏洞挖掘  
原创 zkaq - 腾风起  掌控安全EDU   2025-07-05 07:20  
  
扫码领资料  
  
获网安教程  
  
![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrpvQG1VKMy1AQ1oVvUSeZYhLRYCeiaa3KSFkibg5xRjLlkwfIe7loMVfGuINInDQTVa4BibicW0iaTsKw/640?wx_fmt=other&from=appmsg&wxfrom=5&wx_lazy=1&wx_co=1&tp=webp "")  
  
  
![图片](https://mmbiz.qpic.cn/mmbiz_png/b96CibCt70iaaJcib7FH02wTKvoHALAMw4fchVnBLMw4kTQ7B9oUy0RGfiacu34QEZgDpfia0sVmWrHcDZCV1Na5wDQ/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1&tp=webp "")  
  
  
# 本文由掌控安全学院 -  腾风起 投稿  
  
**来****Track安全社区投稿~**  
  
**千元稿费！还有保底奖励~（ https://bbs.zkaq.cn）**  
  
   
  
> 小编寄语：手拿把恰~  
  
# 免责声明  
  
本报告仅用于安全研究和授权测试，未经授权的渗透测试行为是违法的，切勿用于其他用途，请确保在合法授权的情况下进行安全测试，出现任何后果与本人无关。  
# 前言  
  
师傅们好久不见，最近陆陆续续打了不少，这个产出算近期比较大的，前前后后打了小一周。所以从头到尾整理了一下思路和想法，希望能够一起学习，碰撞思路。也恳请大佬批评指点，小子不胜感激，如有小子能帮忙的，必当竭尽所能。  
#   
# 猎杀时刻  
  
前面写了两篇任意用户密码重置的文章，这个学校也差不多这样进来的统一门户。  
  
找到了打开心门的万能钥匙——记一套统一通杀  
  
我那么费尽心思懂你，重置的了你的密码却得不到你  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_jpg/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmISyxS1rVhteKV0srJ24wHZbeh0JGSW0ribg0ic7MPnvd8NelhnqAwsqRA/640?wx_fmt=jpeg&from=appmsg "")  
  
进来之后呢，这里应该只是一个统一身份认证，不存在跳转别的系统的功能。直接 hunter 固定这个学校的域名，检索到了一个资源平台（学校为了方便，会把用到的系统集成在这里）。用统一身份访问之后，就和 vpn 一样，可以直接跳到别的系统而不需要再去登录。  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmI6OwdRic0N5qZMLuZxsUkXODno6DJ7t6gznOzyVOxKIbSHuYVicM47PeA/640?wx_fmt=png&from=appmsg "")  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIWKCnl6UGtWIfI3JIsrDDKRJJnB6ZWm4lajUhA6dc0DOEeXAwQZ5xmQ/640?wx_fmt=png&from=appmsg "")  
#   
# 接口利用  
  
因为这个用到了 webpack 打包技术，我对这个研究还是蛮多的。js 找了一些路径直接拼接  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIlEuTZKic5gjLraGMibhkdyLdtupfcnJjibUa8McRTaaVm2zm6xteiaoNgQ/640?wx_fmt=png&from=appmsg "")  
  
其中有一个接口会跳到别的页面，跳到别的页面之后会加载一些新的 js，从新加载的 js 里面继续找接口，又跳到了新的页面，没错他又又加载了新的 js，再继续找接口拼接（具体可以看我之前写的 webpack 文章，有好几篇）  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmISRqicre3733r78YArTtHKErLuziafexu806JBIBp7nVWzZWsjkXROb2A/640?wx_fmt=png&from=appmsg "")  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmI1s3TI35LQ4Vj1M41zUCSiaMpn4dgHcMEs7MFMTL5RafC4YaYk3lhyVA/640?wx_fmt=png&from=appmsg "")  
  
可惜你不听周杰伦，更不知道他的“接口"  
  
利用shuji还原webpack打包源码  
  
#   
# 接口提权  
  
  
好的拼到了这里，可以提权任意用户到超管，到这危害打满了。  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIhOQ4iajYI6vibawlD2gsnnYmvluaUOGTDs2JHr4Qm26eMSywibjXX8iaEQ/640?wx_fmt=png&from=appmsg "")  
##   
#   
# 信息泄露  
  
  
内置有 68 个应用系统，每一个都有大量敏感信息，全校所有的数据都走的这个控制台下面的这些系统。  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIIbX4zOVhSzT1HLckibAhByNl8HVKVpDpS1x96GmIXEGEyibyZgicssffA/640?wx_fmt=png&from=appmsg "")  
  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIUsDSAv40RorcqXdBecddraWFgqYn0GyZRNSEaw6nRVCp2gvAZKKK4A/640?wx_fmt=png&from=appmsg "")  
  
其中一个  
数字通行系统举例 敏感信息条数二百六十多万  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIK6eJ3o4drtbj7Atez1J7TNg0n0LgHQDSuezHd3Dsf9UyPe04ZUDmUQ/640?wx_fmt=png&from=appmsg "")  
##   
#   
# 未授权  
  
  
每一个敏感信息返回的接口，都可以删除认证信息尝试尝试，说不定就存在未授权。  
  
这里也是未授权很多哈，直接都一起交了  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIlg8fflmPKQ90MqHBicd4KHOXIewpcWUeogXibtwZAKUjwjRibdDjbIMdQ/640?wx_fmt=png&from=appmsg "")  
  
这是一套通用，这个学校危害打的很高，接下来去看同样用这套的单位。  
  
#   
# 通用资产查找  
  
  
  
我没有写过找通用的文章，这里找了个若依的 举例补充一下  
  
F12 检查来到网络，刷新一下页面，会加载一个.ico  
  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIww9aribQVGiaSmib6k7gFicDQyqAq0hUtzuzV92rejjk65ebN8zLnDw5bQ/640?wx_fmt=png&from=appmsg "")  
  
访问 ico 的链接下载下来  
  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIlCoZtYeHcZvrJWFoFfjCwv8TLwCvspA0fcRaUNLy30E2pvprmbU3ag/640?wx_fmt=png&from=appmsg "")  
  
  
用资产测绘平台检索，可以检索到同样存在这个 ico 的资产  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIoyWicW0OEgWCMClAOlmKeaFDHn3uHtQ1mibPVYFpG77KwSg44ow4o77A/640?wx_fmt=png&from=appmsg "")  
  
  
这里不推荐，拿学校举例，学校会把这个 ico 换成自己学校的图标，这样 ico 检索就检索不到了。  
  
这种比较特殊的接口，和这种一看就感觉有点特殊的 css，js 或者接口啥的，也都可以作为指纹来检索,可以多尝试，这里随便举个例子  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIGc2ico8KH57XFNvkpYh1Y7zcUYVjZa6ZqMrMiccbbGAKZpVcBXicBF9fQ/640?wx_fmt=png&from=appmsg "")  
  
  
包括查看网页源代码，这种比较特殊的文字内容，都可以作为指纹  
  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIRHGZfiaMp7saWTkJiaaqhJhqFm8d6JtQj0klPG8sGg4TzVbDZbv1fM2w/640?wx_fmt=png&from=appmsg "")  
  
  
检索出来一打开也都很明显是若依框架，查 ico 就查不出来的  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIk3qlSb4XLibHD3LCBlWpRPg5t4Beia18iceSc0Y5eseHJduFB9zuibFj5w/640?wx_fmt=png&from=appmsg "")  
  
  
    知道开发商是谁后，直接查他们的官网，他们官网一般也都会有合作单位的案例，然后直接 hunter 定向检索就行，或许会有其他收获  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIBpHRaeS9KkzBKlyaTSuvWpXfxVhdPSANQgtseo4s3y36w297TKSYBg/640?wx_fmt=png&from=appmsg "")  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIPRzjPZK3R0PZayapEq23bcaRWEykibRGTr1h75NjmuchibEQicSUGzxFg/640?wx_fmt=png&from=appmsg "")  
  
    通过上述办法找到了用这套的学校单位。问题来了，首先我想拼到那个接口的话，必须要有一个账号登录进去，可是别的学校我没有账号密码咋办，先找功能点。  
  
账号激活功能点需要学号姓名身份证。  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmISribt8mx7BwLAySyRcRUFYsWF8A5jJ3XAkYm16IibqnBUFF3lwz7gb8A/640?wx_fmt=png&from=appmsg "")  
#   
#   
# 信息收集  
  
## 社工大法 1 刷抖音   
  
很推荐，一边看美女一边搜集  
  
搜集到了某位美女的姓名和身份证号  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmInVcndJ5k83LraDxrLNlAJ6XhhmYVv1bdlBehE2SAoHrdsal63ZQysw/640?wx_fmt=png&from=appmsg "")  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmI2aPfCibyia2hUDgNicdb3Ju6bNLmWFaMHmIewJMsK0Td3dcJQSaJLJ3uQ/640?wx_fmt=png&from=appmsg "")  
  
根据需求去检索  
  
还差学号，谷歌语法直接检索这个同学，没有检索的这个同学的学号  
```
site:xxxx.edu.cn ( "xx雨”)
```  
  
继续刷这个同学的主页知道了这位同学专业是 xx 体育专业  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIVMX52B3sJ7vcib2WREZdWibxs5Zab0vlUZiaVo818JUO88UZOvDSzeiaEw/640?wx_fmt=png&from=appmsg "")  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_jpg/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIcltReTpHJt5o5reNHia95ajeRM8k76Gjibc9ywj0e2CtCupIhAdMibKuw/640?wx_fmt=jpeg&from=appmsg "")  
```
site:xxxx.edu.cn ( "xx体育”)
```  
  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIg6LMasQnJQoFQm6E4qw1Tt6MQlQOYibeJjZLkYzUGDGsqlxP6UufMfQ/640?wx_fmt=png&from=appmsg "")  
  
  
发现 2021 级和 2020 级这个专业的同学，前几位全是一样的，除了代表学年的 202X,只有后三位不一样。那上面搜集到身份证和姓名的同学学号大概率就是 2024+(打码的三位)+07+(需要爆破的三位)  
  
三位数还是值得去爆破的  
  
最后如愿爆破出来了，但是很可惜，此账号已经激活  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIuZYwXicTY36toib2M84d9Vhhibx0JuX9ibUogKiaX2tjCWEiaYZQ6hoib0QkA/640?wx_fmt=png&from=appmsg "")  
  
尝试密码爆破了一下，五次之后直接封锁账号,这种情况我能想到的固定密码去跑账号，这里用的还是强口令规则，也就直接放弃去爆破了。  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIDTKiaQqic3dVh7edzkjic7oefkhkhPQun2lBU5yQdJibgonEj49CRzrbaA/640?wx_fmt=png&from=appmsg "")  
## 社工大法 2 利诱  
  
十块钱我还是给的起的。。。 不推荐 有风险  这里只找了两个在咸鱼上售卖自己的自强不息的贫困生试了试。想了想觉得没必要花钱....我也是贫困生，十块钱都能吃顿饭了。  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_jpg/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmINtKRmFzTbm4VdXZibFn9NeqKOq1Ne4sIMKlWJick4P1e5qWtp77GpYxg/640?wx_fmt=jpeg&from=appmsg "")  
## 社工大法 3  
  
水群，有的群里面的信息还是非常给力的，被拒绝也无所谓，适合我这种社恐。  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_jpg/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIe9j1nbm7oyZDsOcLLfhuAyOXHUrSbBr7TnkRfZkzXLLZn0RW03BWmw/640?wx_fmt=jpeg&from=appmsg "")  
  
别的接口也跟了跟，什么注册，忘记密码，都没有产出。  
  
没辙了，暂时先放过这个学校，来到了第三个、第四个用这个系统的学校。  
  
用的同一个系统，在别的学校打出来，相当于打了这个学校。  
# 打通用  
### 密码重置  
  
好的来到了这个学校，发现这个学校还多了一个账号解冻的接口，尝试走走  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIS023cDib00gpZSfjBm13yoKSY9PzKBwwCvWcHIBht6eIehuKZSpzZdA/640?wx_fmt=png&from=appmsg "")  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmI6JpyccKWrI7x4tky4iaKicNfy7EP3TbJUTD2qic2HYeGmJj69s4KnWNGQ/640?wx_fmt=png&from=appmsg "")  
  
账号admin成功进入下一步  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIeiaHPvG15u2SlSDzmUH7MdibmOYtkGCC30j9ZaibGiagMuAW1QsYwWUyHw/640?wx_fmt=png&from=appmsg "")  
  
  
按照顺序选了三个验证问题，答案都随便填了个 1  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIiaTbG0HILCWQ7Sd8OKVnQWMFjVqatQyVZ4FricprIIomCWDfBwsPkcFw/640?wx_fmt=png&from=appmsg "")  
  
嗯？ 九个有十个的不对劲，怎么我 tm 还答对了一个呢  
  
经过检验发现安全问题答案分别为1，2，3  
  
有点意思，我这应该是拿阳寿换的。  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIwTL7tbbvK6Yc6kGiaic1s38ibVp9GlaicIeygvqkVOmdJhs3qzc1mGaHJg/640?wx_fmt=png&from=appmsg "")  
  
  
登录成功，统一系统的超级管理员权限  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIIr5y3uzia6I7Yqk3YDuDmLMtpxVbbyDvqhic7w4bKenbt4Dwnkpded6A/640?wx_fmt=png&from=appmsg "")  
  
这个解冻的接口，拼接到别的学校，最后也都没有走通。这个点确实是运气来了，捡到了。  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIh8rdwdcqdPW0LPNsv94niaIb4iaABEbs7KXcyM9BcqVn7k8MKe77qm4g/640?wx_fmt=png&from=appmsg "")  
### 通用未授权拿下别的单位  
  
在这个系统里面就走的很细致了，最后找到了一处敏感信息接口的未授权，能返回全校所有人的账号，身份证，手机号，密码加密值等等信息。  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIX0kyW8msu7ltshicf5k6NpEV4Zjsa0dTbus3RibbgF2oFicgcLrSUgWog/640?wx_fmt=png&from=appmsg "")  
  
这个接口可以拼接到别的学校同样存在这个的未授权  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmI7mDzgFshOtwCqjC75USiaItxg9SKvjCX9l9mUrZHJGUM6avfKia09gng/640?wx_fmt=png&from=appmsg "")  
# springboot 站 env+peapdump 敏感信息泄露  
  
在拼接路径的时候，出现了下图，这一看就是 springboot 站点，那熟知的肯定就是 env 和解 heapdump 拿数据库啥的各种账号密码  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIFxHkRbiaq1DW6ygLic54B96SB5Qot3JuYmmLeWMQYHiaNUN4nFqRcoA2g/640?wx_fmt=png&from=appmsg "")  
  
  
因为这里用 springbootscan 工具跑的时候有 waf 直接给拦截了，所以我后根据其特定路径手动构造，拼到了 env，和 heapdump   
  
heapdump由于可读性比较差，一般配合env接口一起分析，env接口返回全部环境变量但会将带有password、secret等常见的敏感字段值替换为掩码******。  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIYYjnJdLZqYdianGbE21vAfL9TgJzIytVoz9FLmsBDrP65ic7fwkibV94w/640?wx_fmt=png&from=appmsg "")  
  
用 heapdump_tool 之类的工具可以解 heapdump 拿到 env 里面******的密码  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmInR0sUTiagEbkJ3GVbeXjLEHa3Zm5XZefFhB8zDUHhwd42ibVB07yNvBg/640?wx_fmt=png&from=appmsg "")  
  
但是我在解 heapdump 的时候出现了下面这个问题，求大佬指点  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIISShckniasTreDibKkUIjuU1SuMWDpRWicj96fjQbrmQhkXLhnFQ8CHOQ/640?wx_fmt=png&from=appmsg "")  
  
最后是看了一些公众号  
  
利用 Eclipse MemoryAnalyzer 工具对泄露的heap  
dump文件  
进行分析，查询加载到内存中的明文密码信息。  
  
[https://mp.weixin.qq.com/s/NbZinWBh6wuiyoONwNiHdA](https://mp.weixin.qq.com/s?__biz=MzIzNDE0Mzk0NA==&mid=2649595407&idx=1&sn=582ea175d8b5be6599275f5b61888a09&scene=21#wechat_redirect)  
  
### 借助这些敏感信息，以及一开始打的普通用户提权到超管，也是拿下了别的学校的这套系统。  
#### 学校 1  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIbXgzUscm6GibibBIO2291TFUIDHQ5wRqM4IlGFGhSevc3HRjhPY5EE6w/640?wx_fmt=png&from=appmsg "")  
#### 学校 2  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIGLTCALj4BkJtwn8USOXajFtOJNYem5ZVpJjRD3lQnemKl8r2unBSVQ/640?wx_fmt=png&from=appmsg "")  
#### 学校 3  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIu2pZuCdK1SJ3s91vqarFTUNblEb6Jt76Dia9CBpJJiagYiaraZ8s90PBQ/640?wx_fmt=png&from=appmsg "")  
#### 学校 4  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/BwqHlJ29vcrSD5mlpwS9a541pjKG4CmIV36UQmqSq15panGoRwdJgQnNkT4icCMYa0icCxp85yInc2oJIJNKADAA/640?wx_fmt=png&from=appmsg "")  
  
  
