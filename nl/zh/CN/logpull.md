---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: log pull, logpull, time-based, rayID

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Logpull
{:#logpull}

IBM 客户可以访问企业帐户上的 Logpull 服务。此服务允许用户使用 [CLI](/docs/cis-cli-plugin?topic=cis-cli-plugin-cis-cli-commands#log) 通过 HTTP 来使用请求日志。

这些日志包含与连接客户机、通过网络的请求路径以及来自源 Web 服务器的响应相关的数据。


## 用例
{:#logpull-usecases}

### 基于 RayID
{:#logpull-usecases-rayid}

如果用户在执行命令后收到错误消息，那么他们可以使用响应头中提供的 RayID 来获取与该命令相关的日志。

如果您的 RAY_ID 在末尾包含 `-XXX`，请务必将其除去。例如，`12ab34cdef567gh8-XXX` 变为 `12ab34cdef567gh8`。
{.note}

**请求**

```
ibmcloud cis logpull DNS_DOMAIN_ID --ray-id RAY_ID
```

**响应**

```
{
    "ClientIP": "68.278.11.89",
    "ClientRequestHost": "testing.logpull.com",
    "ClientRequestMethod": "GET",
    "ClientRequestURI": "/var/www",
    "EdgeEndTimestamp": 1545155129703000000,
    "EdgeResponseBytes": 1935,
    "EdgeResponseStatus": 403,
    "EdgeStartTimestamp": 1545155129696000000,
    "RayID": "48b371889c489b2c"
}
```

### 基于持续时间
{:#logpull-usecases-time-duration}

如果用户在执行命令后收到错误消息，但不知道响应的 RayID，那么可以改为使用持续时间。用户会收到发生错误前后的时段内给定区域的所有日志，并且可在结果中进行搜索。


**必需参数**

作为 Unix 时间戳记（以秒或纳秒为单位）或者符合 RFC 3339 的绝对时间戳记的开始和结束时间，以及以分钟或小时表示的持续时间。

**请求**
```
ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00
```
**响应**
```
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/bootstrap-collapse.js","EdgeEndTimestamp":1545067628046000000,"EdgeResponseBytes":2205,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628044000000,"RayID":"48ab19434891c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/3d.gif","EdgeEndTimestamp":1545067627970000000,"EdgeResponseBytes":2538446,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067627951000000,"RayID":"48ab1942bf96c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/logo.gif","EdgeEndTimestamp":1545067628051000000,"EdgeResponseBytes":82257,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628048000000,"RayID":"48ab194348a0c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/docs.css","EdgeEndTimestamp":1545067627952000000,"EdgeResponseBytes":540,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067627948000000,"RayID":"48ab1942af8ac7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/bootstrap.css","EdgeEndTimestamp":1545067627952000000,"EdgeResponseBytes":17311,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067627948000000,"RayID":"48ab1942af85c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/jquery.js","EdgeEndTimestamp":1545067628045000000,"EdgeResponseBytes":33555,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628042000000,"RayID":"48ab19434882c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/watson.gif","EdgeEndTimestamp":1545067628052000000,"EdgeResponseBytes":893230,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628046000000,"RayID":"48ab194348a3c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/bootstrap-386.js","EdgeEndTimestamp":1545067628046000000,"EdgeResponseBytes":1663,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628043000000,"RayID":"48ab19434884c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/Fixedsys500c.woff","EdgeEndTimestamp":1545067630272000000,"EdgeResponseBytes":14055,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067629064000000,"RayID":"48ab1949aca2c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/bios.gif","EdgeEndTimestamp":1545067628055000000,"EdgeResponseBytes":1121237,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628046000000,"RayID":"48ab1943489ec7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/bootstrap-modal.js","EdgeEndTimestamp":1545067628046000000,"EdgeResponseBytes":2569,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628043000000,"RayID":"48ab1943488ac7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/holder.js","EdgeEndTimestamp":1545067628053000000,"EdgeResponseBytes":4593,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628046000000,"RayID":"48ab19434898c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/old_school.png","EdgeEndTimestamp":1545067627960000000,"EdgeResponseBytes":1466,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067627952000000,"RayID":"48ab1942bf92c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com,"ClientRequestMethod":"GET","ClientRequestURI":"/assets/bootstrap-responsive.css","EdgeEndTimestamp":1545067627951000000,"EdgeResponseBytes":4797,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067627948000000,"RayID":"48ab1942af86c7a7"}
```

### 字段
{:#logpull-usecases-fields}

如果未在请求中指定 `fields`，那么将返回缺省字段的有限集。可在此处查找所有可用字段的完整列表：

**请求**

```
ibmcloud cis logpull DNS_DOMAIN_ID --available-fields
```

字段将以逗号分隔列表的形式传递。例如，要获取“ZoneID”和“RayID”，请使用：

```
ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00 --fields ZoneId,RayID
```

**字段列表**

当前可用的字段（截至 2018 年 12 月）：
```
"CacheCacheStatus": "string; unknown | miss | expired | updating | stale | hit | ignored | bypass | revalidated",
"CacheResponseBytes": "int; number of bytes returned by the cache",
"CacheResponseStatus": "int; HTTP status code returned by the cache to the edge: all requests (including non-cacheable ones) go through the cache: also see CacheStatus field",
"CacheTieredFill": "bool; tiered Cache was used to serve this request",
"ClientASN": "int; client AS number",
"ClientCountry": "string; country of the client IP address",
"ClientDeviceType": "string; client device type",
"ClientIP": "string; IP address of the client",
"ClientIPClass": "string; client IP class",
"ClientRequestBytes": "int; number of bytes in the client request",
"ClientRequestHost": "string; host requested by the client",
"ClientRequestMethod": "string; HTTP method of client request",
"ClientRequestPath": "string; URI path requested by the client",
"ClientRequestProtocol": "string; HTTP protocol of client request",
"ClientRequestReferer": "string; HTTP request referrer",
"ClientRequestURI": "string; URI requested by the client",
"ClientRequestUserAgent": "string; User agent reported by the client",
"ClientSSLCipher": "string; Client SSL cipher",
"ClientSSLProtocol": "string; Client SSL (TLS) protocol",
"ClientSrcPort": "int; client source port",
"EdgeColoID": "int; Cloudflare edge colo id",
"EdgeEndTimestamp": "int or string; unix nanosecond timestamp the edge finished sending response to the client",
"EdgePathingOp": "string; indicates what type of response was issued for this request (unknown = no specific action)",
"EdgePathingSrc": "string; details how the request was classified based on security checks (unknown = no specific classification)",
"EdgePathingStatus": "string; indicates what data was used to determine the handling of this request (unknown = no data)",
"EdgeRateLimitAction": "string; the action taken by the blocking rule; empty if no action taken",
"EdgeRateLimitID": "int; the internal rule ID of the rate-limiting rule that triggered a block (ban) or simulate action. 0 if no action taken",
"EdgeRequestHost": "string; host header on the request from the edge to the origin",
"EdgeResponseBytes": "int; number of bytes returned by the edge to the client",
"EdgeResponseCompressionRatio": "float; edge response compression ratio",
"EdgeResponseContentType": "string; Edge response Content-Type header value",
"EdgeResponseStatus": "int; HTTP status code returned by Cloudflare to the client",
"EdgeServerIP": "string; IP of the edge server making a request to the origin",
"EdgeStartTimestamp": "int or string; unix nanosecond timestamp the edge received request from the client",
"OriginIP": "string; IP of the origin server",
"OriginResponseBytes": "int; number of bytes returned by the origin server",
"OriginResponseHTTPExpires": "string; value of the origin 'expires' header in RFC1123 format",
"OriginResponseHTTPLastModified": "string; value of the origin 'last-modified' header in RFC1123 format",
"OriginResponseStatus": "int; status returned by the origin server",
"OriginResponseTime": "int; number of nanoseconds it took the origin to return the response to edge",
"OriginSSLProtocol": "string; SSL (TLS) protocol used to connect to the origin",
"ParentRayID": "string; ray id of the parent request if this request was made through a worker script",
"RayID": "string; Ray ID of the request",
"SecurityLevel": "string; the security level configured at the time of this request. This is used to determine the sensitivity of the IP Reputation system.",
"WAFAction": "string; action taken by the WAF, if triggered",
"WAFFlags": "string; additional configuration flags: simulate (0x1) | null",
"WAFMatchedVar": "string; the full name of the most-recently matched variable",
"WAFProfile": "string; WAF profile: low | med | high",
"WAFRuleID": "string; ID of the applied WAF rule",
"WAFRuleMessage": "string; rule message associated with the triggered rule",
"WorkerCPUTime": "int; amount of time in microseconds spent executing a worker if any",
"WorkerStatus": "string; status returned from worker daemon",
"WorkerSubrequest": "bool; whether or not this request was a worker subrequest",
"WorkerSubrequestCount": "int; number of subrequests issued by a worker when handling this request",
"ZoneID": "int; internal zone ID"
```

### 示例
{:#logpull-usecases-example}
以下是示例 `logpull` 调用和特定类型响应的示例。

**请求**
```
ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00 --fields ClientRequestURI,CEdgeResponseBytes,CParentRayID,CWorkerStatus,COriginResponseTime,CEdgeResponseStatus,CWorkerSubrequest,CClientRequestProtocol,CWAFRuleID,CEdgePathingOp,CClientSrcPort,CWorkerSubrequestCount,CEdgeRequestHost,CClientSSLCipher,CEdgePathingSrc,COriginResponseStatus,CClientIPClass,CWAFAction,CEdgeColoID,CClientCountry,CClientRequestHost,CWAFFlags,CClientASN,CEdgeServerIP,CCacheCacheStatus,CSecurityLevel,CClientRequestUserAgent,CCacheResponseBytes,CWAFMatchedVar,CEdgeStartTimestamp,CClientSSLProtocol,CEdgeEndTimestamp,CEdgeResponseContentType,CClientRequestBytes,CCacheResponseStatus,CWorkerCPUTime,CRayID,CClientRequestMethod,CClientIP,CClientRequestPath,COriginResponseHTTPExpires,CCacheTieredFill,CWAFRuleMessage,CEdgePathingStatus,CClientDeviceType,COriginSSLProtocol,CEdgeRateLimitAction,COriginIP,CEdgeRateLimitID,CZoneID,CEdgeResponseCompressionRatio,CClientRequestReferer,CWAFProfile,COriginResponseHTTPLastModified,COriginResponseBytes --timestamps=rfc3339'
```

**状态码为 200 的响应**
```
{
"CacheCacheStatus":"unknown",
"CacheResponseBytes":396,
"CacheResponseStatus":200,
"CacheTieredFill":false,
"ClientASN":56046,
"ClientCountry":"cn",
"ClientDeviceType":"desktop",
"ClientIP":"1.1.1.1",
"ClientIPClass":"noRecord",
"ClientRequestBytes":400,
"ClientRequestHost":"foo.com",
"ClientRequestMethod":"GET",
"ClientRequestPath":"/",
"ClientRequestProtocol":"HTTP/1.1",
"ClientRequestReferer":"",
"ClientRequestURI":"/",
"ClientRequestUserAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36",
"ClientSSLCipher":"NONE",
"ClientSSLProtocol":"none",
"ClientSrcPort":4532,
"EdgeColoID":134,
"EdgeEndTimestamp":"2019-01-03T01:54:11Z",
"EdgePathingOp":"wl",
"EdgePathingSrc":"macro",
"EdgePathingStatus":"nr",
"EdgeRateLimitAction":"",
"EdgeRateLimitID":0,
"EdgeRequestHost":"foo.com",
"EdgeResponseBytes":808,
"EdgeResponseCompressionRatio":1.57,
"EdgeResponseContentType":"text/html",
"EdgeResponseStatus":200,
"EdgeServerIP":"172.69.98.106",
"EdgeStartTimestamp":"2019-01-03T01:54:11Z",
"OriginIP":"2.2.2.2",
"OriginResponseBytes":0,
"OriginResponseHTTPExpires":"",
"OriginResponseHTTPLastModified":"Tue, 31 Jan 2017 15:01:11 UTC",
"OriginResponseStatus":200,
"OriginResponseTime":7000000,
"OriginSSLProtocol":"unknown",
"ParentRayID":"00",
"RayID":"4931d60516c0b0b0",
"SecurityLevel":"med",
"WAFAction":"unknown",
"WAFFlags":"0",
"WAFMatchedVar":"",
"WAFProfile":"unknown",
"WAFRuleID":"",
"WAFRuleMessage":"",
"WorkerCPUTime":0,
"WorkerStatus":"unknown",
"WorkerSubrequest":false,
"WorkerSubrequestCount":0,
"ZoneID":******
}
```

**状态码为 404 的响应**
```
{
"CacheCacheStatus":"miss",
"CacheResponseBytes":209,
"CacheResponseStatus":404,
"CacheTieredFill":false,
"ClientASN":56046,
"ClientCountry":"cn",
"ClientDeviceType":"desktop",
"ClientIP":"1.1.1.1",
"ClientIPClass":"noRecord",
"ClientRequestBytes":433,
"ClientRequestHost":"foo.com",
"ClientRequestMethod":"GET",
"ClientRequestPath":"/favicon.ico",
"ClientRequestProtocol":"HTTP/1.1",
"ClientRequestReferer":"foo.com/",
"ClientRequestURI":"/favicon.ico",
"ClientRequestUserAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36",
"ClientSSLCipher":"NONE",
"ClientSSLProtocol":"none",
"ClientSrcPort":4532,
"EdgeColoID":134,
"EdgeEndTimestamp":"2019-01-03T01:54:12Z",
"EdgePathingOp":"wl",
"EdgePathingSrc":"macro",
"EdgePathingStatus":"nr",
"EdgeRateLimitAction":"",
"EdgeRateLimitID":0,
"EdgeRequestHost":"foo.com",
"EdgeResponseBytes":556,
"EdgeResponseCompressionRatio":2.87,
"EdgeResponseContentType":"text/html",
"EdgeResponseStatus":404,
"EdgeServerIP":"172.69.98.148",
"EdgeStartTimestamp":"2019-01-03T01:54:12Z",
"OriginIP":"2.2.2.2",
"OriginResponseBytes":0,
"OriginResponseHTTPExpires":"",
"OriginResponseHTTPLastModified":"",
"OriginResponseStatus":404,
"OriginResponseTime":7000000,
"OriginSSLProtocol":"unknown",
"ParentRayID":"00",
"RayID":"4931d60a16c8b0b0",
"SecurityLevel":"med",
"WAFAction":"unknown",
"WAFFlags":"0",
"WAFMatchedVar":"",
"WAFProfile":"unknown",
"WAFRuleID":"",
"WAFRuleMessage":"",
"WorkerCPUTime":0,
"WorkerStatus":"unknown",
"WorkerSubrequest":false,
"WorkerSubrequestCount":0,
"ZoneID":******
}
```

**请求与 WAF 规则（SQLj 攻击）相匹配**
```
{
"CacheCacheStatus":"unknown",
"CacheResponseBytes":0,
"CacheResponseStatus":0,
"CacheTieredFill":false,
"ClientASN":56046,
"ClientCountry":"cn",
"ClientDeviceType":"desktop",
"ClientIP":"1.1.1.1",
"ClientIPClass":"noRecord",
"ClientRequestBytes":501,
"ClientRequestHost":"foo.com",
"ClientRequestMethod":"GET",
"ClientRequestPath":"/login.php",
"ClientRequestProtocol":"HTTP/1.1",
"ClientRequestReferer":"",
"ClientRequestURI":"/login.php?username=asdf&password=asdf",
"ClientRequestUserAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:60.0) Gecko/20100101 Firefox/60.0",
"ClientSSLCipher":"NONE",
"ClientSSLProtocol":"none",
"ClientSrcPort":48718,
"EdgeColoID":134,
"EdgeEndTimestamp":"2019-01-04T02:22:26Z",
"EdgePathingOp":"wl",
"EdgePathingSrc":"macro",
"EdgePathingStatus":"nr",
"EdgeRateLimitAction":"",
"EdgeRateLimitID":0,
"EdgeRequestHost":"",
"EdgeResponseBytes":1849,
"EdgeResponseCompressionRatio":2.82,
"EdgeResponseContentType":"text/html",
"EdgeResponseStatus":403,
"EdgeServerIP":"",
"EdgeStartTimestamp":"2019-01-04T02:22:26Z",
"OriginIP":"",
"OriginResponseBytes":0,
"OriginResponseHTTPExpires":"",
"OriginResponseHTTPLastModified":"",
"OriginResponseStatus":0,
"OriginResponseTime":0,
"OriginSSLProtocol":"unknown",
"ParentRayID":"00",
"RayID":"493a3cc9463eb0d4",
"SecurityLevel":"med",
"WAFAction":"drop",
"WAFFlags":"0",
"WAFMatchedVar":"ARGS:USERNAME",
"WAFProfile":"off",
"WAFRuleID":"100008",
"WAFRuleMessage":"SQLi probing",
"WorkerCPUTime":0,
"WorkerStatus":"unknown",
"WorkerSubrequest":false,
"WorkerSubrequestCount":0,
"ZoneID":******
}
```

**请求与防火墙规则相匹配**
```
{
"CacheCacheStatus":"unknown",
"CacheResponseBytes":0,
"CacheResponseStatus":0,
"CacheTieredFill":false,
"ClientASN":36351,
"ClientCountry":"us",
"ClientDeviceType":"desktop",
"ClientIP":"1.1.1.1",
"ClientIPClass":"noRecord",
"ClientRequestBytes":90,
"ClientRequestHost":"foo.com",
"ClientRequestMethod":"GET",
"ClientRequestPath":"/",
"ClientRequestProtocol":"HTTP/1.1",
"ClientRequestReferer":"",
"ClientRequestURI":"/",
"ClientRequestUserAgent":"curl/7.47.0",
"ClientSSLCipher":"NONE",
"ClientSSLProtocol":"none",
"ClientSrcPort":57260,
"EdgeColoID":26,
"EdgeEndTimestamp":"2019-01-03T08:48:42Z",
"EdgePathingOp":"ban",
"EdgePathingSrc":"user",
"EdgePathingStatus":"ip",
"EdgeRateLimitAction":"",
"EdgeRateLimitID":0,
"EdgeRequestHost":"",
"EdgeResponseBytes":3556,
"EdgeResponseCompressionRatio":0,
"EdgeResponseContentType":"text/html",
"EdgeResponseStatus":403,
"EdgeServerIP":"",
"EdgeStartTimestamp":"2019-01-03T08:48:42Z",
"OriginIP":"",
"OriginResponseBytes":0,
"OriginResponseHTTPExpires":"",
"OriginResponseHTTPLastModified":"",
"OriginResponseStatus":0,
"OriginResponseTime":0,
"OriginSSLProtocol":"unknown",
"ParentRayID":"00",
"RayID":"493a6341d02565e7",
"SecurityLevel":"med",
"WAFAction":"unknown",
"WAFFlags":"0",
"WAFMatchedVar":"",
"WAFProfile":"unknown",
"WAFRuleID":"",
"WAFRuleMessage":"",
"WorkerCPUTime":0,
"WorkerStatus":"unknown",
"WorkerSubrequest":false,
"WorkerSubrequestCount":0,
"ZoneID":******
}
```

**请求受到速率限制**
```
{
"CacheCacheStatus":"unknown",
"CacheResponseBytes":0,
"CacheResponseStatus":0,
"CacheTieredFill":false,
"ClientASN":36351,
"ClientCountry":"us",
"ClientDeviceType":"desktop",
"ClientIP":"1.1.1.1",
"ClientIPClass":"noRecord",
"ClientRequestBytes":90,
"ClientRequestHost":"foo.com",
"ClientRequestMethod":"GET",
"ClientRequestPath":"/",
"ClientRequestProtocol":"HTTP/1.1",
"ClientRequestReferer":"",
"ClientRequestURI":"/",
"ClientRequestUserAgent":"curl/7.47.0",
"ClientSSLCipher":"NONE",
"ClientSSLProtocol":"none",
"ClientSrcPort":33186,
"EdgeColoID":26,
"EdgeEndTimestamp":"2019-01-03T08:59:55Z",
"EdgePathingOp":"ban",
"EdgePathingSrc":"user",
"EdgePathingStatus":"rateLimit",
"EdgeRateLimitAction":"ban",
"EdgeRateLimitID":1307134,
"EdgeRequestHost":"",
"EdgeResponseBytes":3559,
"EdgeResponseCompressionRatio":0,
"EdgeResponseContentType":"text/html",
"EdgeResponseStatus":429,
"EdgeServerIP":"",
"EdgeStartTimestamp":"2019-01-03T08:59:55Z",
"OriginIP":"",
"OriginResponseBytes":0,
"OriginResponseHTTPExpires":"",
"OriginResponseHTTPLastModified":"",
"OriginResponseStatus":0,
"OriginResponseTime":0,
"OriginSSLProtocol":"unknown",
"ParentRayID":"00",
"RayID":"493a73ad468419b6",
"SecurityLevel":"med",
"WAFAction":"unknown",
"WAFFlags":"0",
"WAFMatchedVar":"",
"WAFProfile":"unknown",
"WAFRuleID":"",
"WAFRuleMessage":"",
"WorkerCPUTime":0,
"WorkerStatus":"unknown",
"WorkerSubrequest":false,
"WorkerSubrequestCount":0,
"ZoneID":******
}
```

**源服务器停机（错误 521，Web 服务器停机）**
```
{
"CacheCacheStatus":"miss",
"CacheResponseBytes":177,
"CacheResponseStatus":521,
"CacheTieredFill":false,
"ClientASN":56046,
"ClientCountry":"cn",
"ClientDeviceType":"desktop",
"ClientIP":"1.1.1.1",
"ClientIPClass":"noRecord",
"ClientRequestBytes":1082,
"ClientRequestHost":"foo.com",
"ClientRequestMethod":"GET",
"ClientRequestPath":"/favicon.ico",
"ClientRequestProtocol":"HTTP/2",
"ClientRequestReferer":"",
"ClientRequestURI":"/favicon.ico",
"ClientRequestUserAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:60.0) Gecko/20100101 Firefox/60.0",
"ClientSSLCipher":"AEAD-AES128-GCM-SHA256",
"ClientSSLProtocol":"TLSv1.3",
"ClientSrcPort":3060,
"EdgeColoID":134,
"EdgeEndTimestamp":"2019-01-03T06:33:55Z",
"EdgePathingOp":"wl",
"EdgePathingSrc":"macro",
"EdgePathingStatus":"nr",
"EdgeRateLimitAction":"",
"EdgeRateLimitID":0,
"EdgeRequestHost":"foo.com",
"EdgeResponseBytes":5177,
"EdgeResponseCompressionRatio":0,
"EdgeResponseContentType":"text/html",
"EdgeResponseStatus":521,
"EdgeServerIP":"172.69.98.148",
"EdgeStartTimestamp":"2019-01-03T06:33:55Z",
"OriginIP":"2.2.2.2",
"OriginResponseBytes":0,
"OriginResponseHTTPExpires":"",
"OriginResponseHTTPLastModified":"",
"OriginResponseStatus":0,
"OriginResponseTime":3000000,
"OriginSSLProtocol":"unknown",
"ParentRayID":"00",
"RayID":"49336fc9397ab080",
"SecurityLevel":"med",
"WAFAction":"unknown",
"WAFFlags":"0",
"WAFMatchedVar":"",
"WAFProfile":"unknown",
"WAFRuleID":"",
"WAFRuleMessage":"",
"WorkerCPUTime":0,
"WorkerStatus":"unknown",
"WorkerSubrequest":false,
"WorkerSubrequestCount":0,
"ZoneID":******
}
```