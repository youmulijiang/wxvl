#  思科修复了可能导致 root 级远程代码执行的关键 ISE 漏洞  
鹏鹏同学  黑猫安全   2025-06-27 01:26  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/8dBEfDPEceibqiacckIpMAUAcEAiax4sINRH0wkKdXal1plctQosn2pdzEzxx9agzG04X42LbwUuly34UA2Pglv1A/640?wx_fmt=png&from=appmsg "")  
  
思科修复了身份服务引擎（ISE）及ISE被动身份连接器（ISE-PIC）中两个关键漏洞（编号CVE-2025-20281与CVE-2025-20282），未经身份验证的远程攻击者可借此以root权限执行任意代码。  
  
"思科身份服务引擎（ISE）及ISE被动身份连接器（ISE-PIC）存在的多个漏洞，可能允许未经身份验证的远程攻击者以root用户身份在底层操作系统执行命令。"安全公告指出。  
  
其中CVE-2025-20281（CVSS评分10分）影响思科ISE/ISE-PIC 3.3及以上版本，而CVE-2025-20282（CVSS评分10分）仅影响3.4版本，其他版本不受影响。  
  
CVE-2025-20281是ISE/ISE-PIC的关键漏洞，攻击者可通过存在缺陷的API以root权限远程执行代码。"该漏洞源于对用户输入验证不足，攻击者通过提交特制API请求即可利用此漏洞。成功利用后，攻击者可获得受影响设备的root权限。"公告补充说明。  
  
第二个漏洞CVE-2025-20282同样属于高危漏洞，攻击者可通过内部API以root权限上传并执行文件。"此漏洞因系统未对上传文件进行有效性检查，导致恶意文件可被存入特权目录。攻击者通过向受影响设备上传特制文件即可实现攻击。"公告强调，"成功利用该漏洞可存储恶意文件，进而执行任意代码或获取系统root权限。"  
  
思科表示目前尚无针对这些漏洞的临时解决方案。以下是已修复的版本信息表：  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/8dBEfDPEceibqiacckIpMAUAcEAiax4sINRjiaYHnicwXsC9zMFAp5FeYHcuRvBkp8ia3974OBLhMddQrzAicwxPftHhg/640?wx_fmt=png&from=appmsg "")  
  
思科产品安全事件响应团队（PSIRT）目前未发现这些漏洞在野被利用的情况。  
  
