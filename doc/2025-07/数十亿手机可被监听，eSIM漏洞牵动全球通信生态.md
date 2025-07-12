#  数十亿手机可被监听，eSIM漏洞牵动全球通信生态  
 安全客   2025-07-11 09:19  
  
过去几年，全球手机用户正加速告别传统 SIM 卡，拥抱新一代**eSIM（嵌入式用户身份模块）技术**  
。这种无法物理插拔的芯片，被认为更加安全、便利，广泛应用于智能手机、平板、可穿戴设备乃至车联网终端中。然而，一项最新研究却揭示：这一看似“安全”的通信核心，正隐藏着一场悄无声息的安全危机。  
  
  
Security Explorations 公司创始人 Adam Gowdiak 近期披露，**全球数十亿 eSIM 卡中使用的关键组件 Java Card 存在严重安全漏洞**  
，攻击者不仅可在物理接触设备后提取关键凭据，甚至能够远程 OTA（空中下载）方式在 eSIM 芯片中植入恶意代码，实现**监听、SIM 克隆、通信劫持**  
等多种攻击手段。这并非边缘技术问题，而是与全球移动通信根基相关的系统性安全漏洞。  
  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/Ok4fxxCpBb4ZlVOZhMsM6ibGRbzvicWk5tGbmHDHfhtPDNrgh7JPwYiacMNoCYVvpcGdXMHKo9gdXt9mB8oG3NZGw/640?wx_fmt=png&from=appmsg "")  
  
  
**01**  
  
**漏洞源头：六年前被忽视的安全缺陷**  
  
  
事件核心在于 Oracle Java Card 虚拟机中的**“类型混淆”漏洞**  
。Java Card 是 Oracle 专为资源受限设备打造的 Java 应用执行平台，广泛集成于 eSIM 芯片、银行卡、身份认证设备等领域。早在六年前，Gowdiak 就发现其在执行字节码时**缺乏关键类型校验，可能导致权限绕过**  
。但 Oracle 以“问题不适用”为由未予修复。  
  
  
近期，Gowdiak 利用该漏洞对 Kigen 生产的 eUICC（嵌入式通用集成电路卡）进行攻击测试：他通过物理方式提取设备私钥，随后下载运营商配置文件（profile），这些文件**竟以明文传输且包含关键密钥**  
。借助 Java Card 字节码验证缺失的缺陷，攻击者能**安装任意恶意 applet，完全控制 eSIM，且过程无任何安全告警**  
。  
  
  
**02**  
  
**eSIM多配置共存：一处破防，全局失守**  
  
  
相比传统 SIM 卡，eSIM 支持**多个配置文件并存**  
——用户可以同时保有主运营商与本地临时运营商的服务，出境漫游、切换资费变得更加灵活。然而，这种“共处一芯”的机制，也带来了新的攻击面。  
  
  
Hacker News 论坛用户曾指出：“假如你在某国旅行时安装当地运营商的 eSIM 作为副配置，若该国政府与运营商合作，可能借此提取你主配置中的关键密钥，监听所有通信。”  
  
  
Gowdiak 认可这一推测：“一旦某个恶意配置被植入，它可以突破芯片边界，影响上面存储的所有运营商配置安全。”这意味着，攻击者无需攻破每一个运营商的网络，**只需利用其中一个“合作”或“被攻陷”的节点，便可能达成系统级控制。**  
  
  
此次被测试的是 Kigen 的芯片——该公司为全球数十亿设备提供 eSIM 服务。Kigen 宣称已向“数百万”受影响设备推送补丁，但考虑到其服务覆盖规模，尚有大量设备仍处于暴露状态。  
  
  
据悉，Java Card 并非 Kigen 独有，而是根据 GSMA 规范被全球所有 eSIM 供应商广泛采用的标准组件。这意味着，这一漏洞的影响可能远超一个厂商、一个型号，而是**波及整个 eSIM 产业生态**  
。  
  
  
**03**  
  
**攻击路径明确，国家级威胁尤为严峻**  
  
  
从攻击路径来看，本次漏洞利用需**具备以下几步能力**  
：  
  
  
  
初期需获取目标设备的物理接触权限（或通过供应链实现）；  
  
  
熟悉 eSIM 配置机制与运营商密钥管理流程；  
  
  
编写并植入 Java Card Applet，完成远程 OTA 部署。  
  
  
这意味着，普通网络犯罪团伙短期内难以大规模复现。但对于具备资源、时间、供应链渗透能力的国家级攻击者而言，这或许是又一个可利用的**“通信根基漏洞”**  
。  
  
  
攻击者可通过该漏洞**实现以下行为**  
：  
  
  
  
克隆 eSIM，实现短信、电话中转与监听；  
  
  
植入持久恶意代码，长期驻留于设备通信模块；  
  
  
拦截 2FA 认证信息，发起账户接管与横向攻击；  
  
  
破坏或封锁通信能力，制造信息断网或瘫痪效果。  
  
  
在零信任架构尚未覆盖通信芯片、安全审计盲区未填补的今天，这类“芯片级后门”很难被传统防御工具发现。  
  
  
eSIM 的便利性和普及是通信未来的趋势，但其安全机制若无法与技术演进同步，带来的将非自由，而是失控。此次事件警示产业界，安全不是上线之后的补救，而应从架构选型开始介入。  
  
  
从 Java Card 规范，到 eSIM 多配置设计，再到 OTA 信任模型，每一环节的“合规”技术决策，都可能成为系统性风险的诱因。面对新一代通信技术，唯有从“底层信任”重塑，才能筑牢真正安全的通信生态。  
  
  
消息来源：  
  
https://www.darkreading.com/endpoint-security/esim-bug-millions-phones-spying-takeover  
  
  
推荐阅读  
  
  
  
  
  
<table><tbody><tr style="box-sizing: border-box;"><td data-colwidth="100.0000%" width="100.0000%" style="border-width: 1px;border-color: rgb(62, 62, 62);border-style: none;box-sizing: border-box;padding: 0px;"><section style="box-sizing: border-box;"><section style="display: flex;flex-flow: row;margin: 10px 0% 0px;justify-content: flex-start;box-sizing: border-box;"><section style="display: inline-block;vertical-align: middle;width: auto;min-width: 10%;max-width: 100%;height: auto;flex: 0 0 auto;align-self: center;box-shadow: rgb(0, 0, 0) 0px 0px 0px;box-sizing: border-box;"><section style="font-size: 14px;color: rgb(115, 215, 200);line-height: 1;letter-spacing: 0px;text-align: center;box-sizing: border-box;"><p style="margin: 0px;padding: 0px;box-sizing: border-box;"><strong style="box-sizing: border-box;"><span leaf="">01</span></strong></p></section></section><section style="display: inline-block;vertical-align: middle;width: auto;flex: 100 100 0%;align-self: center;height: auto;box-sizing: border-box;"><section style="font-size: 14px;letter-spacing: 1px;line-height: 1.8;color: rgb(140, 140, 140);box-sizing: border-box;"><p style="white-space: normal;margin: 0px;padding: 0px;box-sizing: border-box;"><span style="color: rgb(224, 224, 224);box-sizing: border-box;"><span leaf="">｜</span></span><span style="font-size: 12px;box-sizing: border-box;"><span leaf=""><a class="normal_text_link" target="_blank" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);margin: 0px;padding: 0px;outline: 0px;color: rgb(87, 107, 149);text-decoration: none;-webkit-user-drag: none;cursor: default;max-width: 100%;font-family: &#34;PingFang SC&#34;, system-ui, -apple-system, BlinkMacSystemFont, &#34;Helvetica Neue&#34;, &#34;Hiragino Sans GB&#34;, &#34;Microsoft YaHei UI&#34;, &#34;Microsoft YaHei&#34;, Arial, sans-serif;font-size: 12px;font-style: normal;font-variant-ligatures: normal;font-variant-caps: normal;font-weight: 400;letter-spacing: 1px;orphans: 2;text-align: justify;text-indent: 0px;text-transform: none;widows: 2;word-spacing: 0px;-webkit-text-stroke-width: 0px;white-space: normal;background-color: rgb(255, 255, 255);box-sizing: border-box !important;overflow-wrap: break-word !important;" href="https://mp.weixin.qq.com/s?__biz=MzA5ODA0NDE2MA==&amp;mid=2649788766&amp;idx=1&amp;sn=45be51f79306fed040d0aa40d9d39592&amp;scene=21#wechat_redirect" textvalue="3小时盗空6家银行储备金" data-itemshowtype="0" linktype="text" data-linktype="2">3小时盗空6家银行储备金</a></span></span></p></section></section></section><section style="margin: 5px 0%;box-sizing: border-box;"><section style="background-color: rgb(224, 224, 224);height: 1px;box-sizing: border-box;"><svg viewBox="0 0 1 1" style="float:left;line-height:0;width:0;vertical-align:top;"></svg></section></section></section></td></tr><tr style="box-sizing: border-box;"><td data-colwidth="100.0000%" width="100.0000%" style="border-width: 1px;border-color: rgb(62, 62, 62);border-style: none;box-sizing: border-box;padding: 0px;"><section style="box-sizing: border-box;"><section style="display: flex;flex-flow: row;margin: 10px 0% 0px;justify-content: flex-start;box-sizing: border-box;"><section style="display: inline-block;vertical-align: middle;width: auto;min-width: 10%;max-width: 100%;height: auto;flex: 0 0 auto;align-self: center;box-sizing: border-box;"><section style="font-size: 14px;color: rgb(115, 215, 200);line-height: 1;letter-spacing: 0px;text-align: center;box-sizing: border-box;"><p style="margin: 0px;padding: 0px;box-sizing: border-box;"><strong style="box-sizing: border-box;"><span leaf="">02</span></strong></p></section></section><section style="display: inline-block;vertical-align: middle;width: auto;flex: 100 100 0%;align-self: center;height: auto;box-sizing: border-box;"><section style="font-size: 14px;letter-spacing: 1px;line-height: 1.8;color: rgb(140, 140, 140);box-sizing: border-box;"><p style="white-space: normal;margin: 0px;padding: 0px;box-sizing: border-box;"><span style="color: rgb(224, 224, 224);box-sizing: border-box;"><span leaf="">｜</span></span><span style="font-size: 12px;box-sizing: border-box;"><span leaf=""><a class="normal_text_link" target="_blank" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);margin: 0px;padding: 0px;outline: 0px;color: rgb(87, 107, 149);text-decoration: none;-webkit-user-drag: none;cursor: default;max-width: 100%;font-family: &#34;PingFang SC&#34;, system-ui, -apple-system, BlinkMacSystemFont, &#34;Helvetica Neue&#34;, &#34;Hiragino Sans GB&#34;, &#34;Microsoft YaHei UI&#34;, &#34;Microsoft YaHei&#34;, Arial, sans-serif;font-size: 12px;font-style: normal;font-variant-ligatures: normal;font-variant-caps: normal;font-weight: 400;letter-spacing: 1px;orphans: 2;text-align: justify;text-indent: 0px;text-transform: none;widows: 2;word-spacing: 0px;-webkit-text-stroke-width: 0px;white-space: normal;background-color: rgb(255, 255, 255);box-sizing: border-box !important;overflow-wrap: break-word !important;" href="https://mp.weixin.qq.com/s?__biz=MzA5ODA0NDE2MA==&amp;mid=2649788757&amp;idx=1&amp;sn=d868d9b3dbbf425ea9312d4241658643&amp;scene=21#wechat_redirect" textvalue="伊朗黑客组织盯上特朗普" data-itemshowtype="0" linktype="text" data-linktype="2">伊朗黑客组织盯上特朗普</a></span></span></p></section></section></section><section style="margin: 5px 0%;box-sizing: border-box;"><section style="background-color: rgb(224, 224, 224);height: 1px;box-sizing: border-box;"><svg viewBox="0 0 1 1" style="float:left;line-height:0;width:0;vertical-align:top;"></svg></section></section></section></td></tr><tr style="box-sizing: border-box;"><td data-colwidth="100.0000%" width="100.0000%" style="border-width: 1px;border-color: rgb(62, 62, 62);border-style: none;box-sizing: border-box;padding: 0px;"><section style="box-sizing: border-box;"><section style="display: flex;flex-flow: row;margin: 10px 0% 0px;justify-content: flex-start;box-sizing: border-box;"><section style="display: inline-block;vertical-align: middle;width: auto;min-width: 10%;max-width: 100%;height: auto;flex: 0 0 auto;align-self: center;box-sizing: border-box;"><section style="font-size: 14px;color: rgb(115, 215, 200);line-height: 1;letter-spacing: 0px;text-align: center;box-sizing: border-box;"><p style="margin: 0px;padding: 0px;box-sizing: border-box;"><strong style="box-sizing: border-box;"><span leaf="">03</span></strong></p></section></section><section style="display: inline-block;vertical-align: middle;width: auto;flex: 100 100 0%;align-self: center;height: auto;box-sizing: border-box;"><section style="font-size: 14px;letter-spacing: 1px;line-height: 1.8;color: rgb(140, 140, 140);box-sizing: border-box;"><p style="white-space: normal;margin: 0px;padding: 0px;box-sizing: border-box;"><span style="color: rgb(224, 224, 224);box-sizing: border-box;"><span leaf="">｜</span></span><span style="font-size: 12px;box-sizing: border-box;"><span leaf=""><a class="normal_text_link" target="_blank" style="" href="https://mp.weixin.qq.com/s?__biz=MzA5ODA0NDE2MA==&amp;mid=2649788773&amp;idx=1&amp;sn=55305289f7f57f30bee8bcac340fbe90&amp;scene=21#wechat_redirect" textvalue="电动汽车充电控制器现严重漏洞" data-itemshowtype="0" linktype="text" data-linktype="2">电动汽车充电控制器现严重漏洞</a></span></span></p></section></section></section><section style="margin: 5px 0%;box-sizing: border-box;"><section style="background-color: rgb(224, 224, 224);height: 1px;box-sizing: border-box;"><svg viewBox="0 0 1 1" style="float:left;line-height:0;width:0;vertical-align:top;"></svg></section></section></section></td></tr></tbody></table>  
  
  
**安全KER**  
  
  
安全KER致力于搭建国内安全人才学习、工具、淘金、资讯一体化开放平台，推动数字安全社区文化的普及推广与人才生态的链接融合。目前，安全KER已整合全国数千位白帽资源，联合南京、北京、广州、深圳、长沙、上海、郑州等十余座城市，与ISC、XCon、看雪SDC、Hacking Group等数个中大型品牌达成合作。  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/Ok4fxxCpBb4ZlVOZhMsM6ibGRbzvicWk5tWATZuUic03hU9NPydNdib9OPE9BUhRuNByDrb8bxUEcspSsfXiaasaiapQ/640?wx_fmt=png&from=appmsg "")  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/Ok4fxxCpBb4ZlVOZhMsM6ibGRbzvicWk5tZGibsdum2SfQMIEscgtpibZR0jTV3DENFzNE7mWOcsxo3fJAHQ4tk72A/640?wx_fmt=png&from=appmsg "")  
  
**注册安全KER社区**  
  
**链接最新“圈子”动态**  
  
