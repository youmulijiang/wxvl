#  【漏洞预警】Redis hyperloglog远程代码执行漏洞风险通告  
原创 MasterC  企业安全实践   2025-07-09 01:27  
  
## 一、漏洞描述  
  
Redis是一个开源的内存数据库，以其高性能、灵活性和广泛的数据结构支持而闻名。它被广泛应用于缓存、会话存储、消息队列、实时分析等场景。Redis支持多种数据类型，包括字符串、哈希表、列表、集合、有序集合以及 HyperLogLog等高级数据结构。  
  
近日，互联网上披露了关于Redis中存在一个远程代码执行漏洞。在受影响版本中，由于Redis在处理 hyperloglog操作时，未对用户输入的字符串进行严格验证，导致经过身份验证的用户可以使用特制的字符串来触发hyperloglog操作中的堆栈/堆越界写入，成功利用可导致执行任意系统命令、数据泄露或业务系统沦陷等严重危害。该漏洞对应的CVE编号为CVE-2025-32023，该漏洞影响较高，请受影响的用户做好安全加固措施。  
## 二、漏洞等级  
  
高  
## 三、影响范围  
  
8.0.0 <= version <= 8.0.2  
  
7.4.0 <= version <= 7.4.4  
  
7.2.0 <= version <= 7.2.9  
  
2.8 <= version <= 6.2.18  
## 四、安全版本  
  
version >= 7.4.5  
  
version >= 7.2.10  
  
version >= 6.2.19  
  
version >= 8.0.3  
## 五、修复建议  
  
目前官方已修复该漏洞，建议受影响用户尽快前往官网升级至安全版本。  
## 六、缓解方案  
  
使用ACL限制用户执行hyperloglog操作。  
## 七、参考链接  
  
https://github.com/redis/redis/security/advisories/GHSA-rp2m-q4j6-gr43  
  
https://github.com/redis/redis/commit/50188747cbfe43528d2719399a2a3c9599169445  
  
https://www.oscs1024.com/hd/MPS-8hrg-zfb6  
  
https://github.com/leesh3288/CVE-2025-32023  
  
  
