#  一个用于 Burp Suite 的插件，专为检测和分析 SQL 注入漏洞而设计。  
JaveleyQAQ  夜组安全   2025-07-07 08:05  
  
免责声明  
  
由于传播、利用本公众号夜组安全所提供的信息而造成的任何直接或者间接的后果及损失，均由使用者本人负责，公众号夜组安全及作者不为此承担任何责任，一旦造成后果请自行承担！如有侵权烦请告知，我们会立即删除并致歉。谢谢！  
**所有工具安全性自测！！！VX：**  
**baobeiaini_ya**  
  
朋友们现在只对常读和星标的公众号才展示大图推送，建议大家把  
**夜组安全**  
“**设为星标**  
”，  
否则可能就看不到了啦！  
  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/icZ1W9s2Jp2WrOMH4AFgkSfEFMOvvFuVKmDYdQjwJ9ekMm4jiasmWhBicHJngFY1USGOZfd3Xg4k3iamUOT5DcodvA/640?wx_fmt=png&from=appmsg "")  
  
## 工具介绍  
  
SQL Injection Scout 是一个用于 Burp Suite 的扩展，专为帮助安全研究人员和开发人员检测和分析 SQL 注入漏洞而设计。该扩展提供了丰富的配置选项和直观的用户界面，便于用户自定义扫描和分析过程。  
## 💯 功能特性  
- **被动检测SQL**  
：支持对除OPTIONS  
外的所有请求的参数进行 FUZZ  
 测试，支持 XML  
、JSON  
、FORM  
等表单数据格式。  
  
- **最小化探测**  
：通过最小化的 payload  
 探测，减少对目标的影响。  
  
- **响应差异分析**  
：对响应进行 diff  
 分析，自动标记无趣（灰色）和有趣（绿色）的响应。  
  
- ....  
  
- **判断原理**  
：假设页面参数为反射类型，通过比较 payload  
 和 diff  
 的长度，相同则认为无趣。  
  
- **重复内容过滤**  
：对绿色标记的分组进行进一步分析，出现6  
次以上重复的 diff  
 被标记为无趣。  
  
- **结果排序**  
：根据颜色对最终结果进行排序展示。  
  
- **✅：标记为值得进一步分析的响应。**  
  
- **🔥：标记为存在Sql注入**  
  
- **Error：标记为检测到SQL Error信息存在Response中**  
  
- **Max Params：标记为请求参数大于配置数**  
  
- **Skip URL：匹配配置中需绕过的URL**  
  
-   
- **自动匹配**  
：在扫描页面的响应中自动匹配 diff  
 结果，默认取第一处的差异。  
  
- **正则匹配**  
：正则匹配无需扫描的URL  
  
- **内置范围**  
：支持内置的 scope  
 范围设置。  
  
- **延时扫描**  
：支持固定抖动+随机抖动发包检测，更精准规避 WAF  
。  
  
- **自定义扫描参数数量**  
：防止参数过多导致的性能问题或误报，默认50  
  
- **🔥 Fuzz隐藏参数SQL注入**  
: 支持用户在原始请求中追加隐藏参数列表，进行FUZZ  
测试  
  
- 在Site map  
/HTTP history  
/Logger  
面板添加右键菜单，支持检测站点**单个**  
与**所有**  
请求  
  
- （搭配CaA使用本插件的Fuzz Params List  
功能）  
  
## ✅️ 安装  
1. 确保已安装 Burp Suite。  
  
1. 下载或克隆此项目到本地:  
  
```
   git clone  https://github.com/JaveleyQAQ/SQL-Injection-Scout.git
```  
1. 使用 Gradle 构建项目：  
  
```
   cd SQL-Injection-Scout   ./gradlew shadowJar
```  
1. 在 Burp Suite  
 中加载生成的 JAR  
 文件：  
  
1. 打开 Burp Suite  
，导航到 Extender  
 -> Extensions  
。  
  
1. 点击 Add  
 按钮，选择生成的 JAR  
 文件（位于 build/libs  
 目录下）。  
  
## 🥰  使用指南  
1. 启动 Burp Suite 并确保 SQL Injection Scout 扩展已加载。  
  
1. 在 Extender  
 选项卡中，找到 SQL Injection Scout 并打开其配置面板。  
  
1. 根据需要调整参数和模式设置。  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/icZ1W9s2Jp2UoMfH0BInAJyGYB6oXJvzPcxW0MhVJ2IHBpKsENC63NlDand0FCiahYfpkr6snibqwE9rDItTlHR6A/640?wx_fmt=png&from=appmsg "")  
1. 使用 Burp Suite 的代理、扫描器等功能进行测试，SQL Injection Scout 将自动应用配置并提供结果。  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/icZ1W9s2Jp2UoMfH0BInAJyGYB6oXJvzPVVz05ia2LVSibFN4Ocu0RzcI9RlEJ3IafbInicHzXfmSmAmicPuia7T6fCQ/640?wx_fmt=png&from=appmsg "")  
  
  
## 工具获取  
  
  
  
点击关注下方名片  
进入公众号  
  
回复关键字【  
250707  
】获取  
下载链接  
  
  
## 往期精彩  
  
  
往期推荐  
  
[十款免费的恶意样本分析工具](http://mp.weixin.qq.com/s?__biz=Mzk0ODM0NDIxNQ==&mid=2247494690&idx=1&sn=32c119203374701411a8d9572174b5dc&chksm=c36ba8daf41c21cc7ec7d636f92bfbaaab079f8a55292cb65b31395bfbe9b79d2ae45613ec0d&scene=21#wechat_redirect)  
  
  
[一个专为数字钱包助记词本地安全备份设计的加密工具。助记词数据加密 & 解密](http://mp.weixin.qq.com/s?__biz=Mzk0ODM0NDIxNQ==&mid=2247494661&idx=1&sn=347e22606381188baf5cf640a969e519&chksm=c36ba8fdf41c21eb792672415d86141a93ad6e8a9abbd9b0b852a7cddd966b2cf40db99d8e4d&scene=21#wechat_redirect)  
  
  
[PassGuard是一个轻量级安全工具，专为防护Linux系统中的脏牛(Dirty COW)内核漏洞而设计。](http://mp.weixin.qq.com/s?__biz=Mzk0ODM0NDIxNQ==&mid=2247494660&idx=1&sn=aa557759e534cc95f47181c56432377b&chksm=c36ba8fcf41c21ea800497d928fd66778c5f035328a0f138321d4624c7ae409129e60997c5bc&scene=21#wechat_redirect)  
  
  
[为渗透测试工程师设计的纯前端工具集，专注于信息收集和文本处理，提供 URL 处理、路径分析、信息收集等功能。](http://mp.weixin.qq.com/s?__biz=Mzk0ODM0NDIxNQ==&mid=2247494659&idx=1&sn=cc30a929b1d60d6cf79279fd545f7e77&chksm=c36ba8fbf41c21edc6aa3c62eaddc47d292c113b1f0c662bbe2b42a71da842914ab6b5e5c529&scene=21#wechat_redirect)  
  
  
[一个专为渗透测试人员、红队工程师打造的浏览器插件，便于快速保存当前所有打开的网页 URL，避免在测试过程中遗漏关键目标。](http://mp.weixin.qq.com/s?__biz=Mzk0ODM0NDIxNQ==&mid=2247494647&idx=1&sn=eb97224ab6ac83686e2b8a7928fa425f&chksm=c36baf0ff41c2619ac886d3b93a5d0256b4c16386eb58df5bc1a1483f5b98bf0a95fbcf2403d&scene=21#wechat_redirect)  
  
  
![](https://mmbiz.qpic.cn/mmbiz_png/OAmMqjhMehrtxRQaYnbrvafmXHe0AwWLr2mdZxcg9wia7gVTfBbpfT6kR2xkjzsZ6bTTu5YCbytuoshPcddfsNg/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1&random=0.8399406679299557&tp=webp "")  
  
