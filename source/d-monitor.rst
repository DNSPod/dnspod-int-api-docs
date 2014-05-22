D-Monitor
=========

List All the Sub-domains Whose Type Is "A"
-----------------------
API Address：
    *  https://dnsapi.cn/Monitor.Listsubdomain
HTTP Request Type：
    * POST
Request Parameters：
    * Global parameters
    * **domain** OR **domain_id** Stand for the domain name and the domain id.You only need to and must choose one of them.
Response Code：
    * Common response code.
    * 6 Domain not exists.
    * 7 Invalid domain id.
    * 8 No records under this domain.

Example::

    curl -X POST https://dnsapi.cn/Monitor.Listsubdomain -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2317346'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 20:14:31"
            }, 
            "domain": {
                "id": 2317346, 
                "name": "testapi.com", 
                "punycode": "testapi.com", 
                "grade": "D_Plus", 
                "owner": "api@dnspod.com"
            }, 
            "subdomain": [
                "@"
            ]
        }

List All the "A" Records for A Sub-domain
------------------
API Address：
    *  https://dnsapi.cn/Monitor.Listsubvalue
HTTP Request Type：
    * POST
Request Parameters：
    * Global parameters
    * **domain** OR **domain_id** Stand for the domain name and the domain id.You only need to and must choose one of them.
    * **subdomain** The sub-domain.Essential parameter.
Response Code：
    * Common response code.
    * 6 Domain not exists.
    * 7 Invalid domain id.

Example::

    curl -X POST https://dnsapi.cn/Monitor.Listsubvalue -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2317346&subdomain=@'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 20:19:05"
            }, 
            "domain": {
                "id": 2317346, 
                "name": "testapi.com", 
                "punycode": "testapi.com", 
                "grade": "D_Plus"
            }, 
            "points": {
                "max": 999, 
                "list": {
                    "ctc": "电信", 
                    "cuc": "联通", 
                    "cmc": "移动"
                }
            }, 
            "records": [
                {
                    "id": "16909160", 
                    "area": "默认", 
                    "value": "119.180.24.194"
                }
            ]
        }

Get the Monitor List
---------
API Address：
    *  https://dnsapi.cn/Monitor.List
HTTP Request Type：
    * POST
Request Parameters：
    * Global parameters
Response Code：
    * Common response code.

Example::

    curl -X POST https://dnsapi.cn/Monitor.List -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2317346'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 20:48:02"
            }, 
            "info": {
                "total_count": 1, 
                "down_count": 0
            }, 
            "monitors": [
                {
                    "monitor_id": "281ecb9e-3635-11e2-bab7-0819a6248970", 
                    "domain": "testapi.com", 
                    "domain_id": "2317346", 
                    "domain_grade": "D_Plus", 
                    "record_id": "16909160", 
                    "sub_domain": "@", 
                    "record_line": "默认", 
                    "ip": "119.180.24.194", 
                    "now_ip": "119.180.24.194", 
                    "host": "testapi.com", 
                    "port": "80", 
                    "monitor_type": "http", 
                    "monitor_path": "/", 
                    "monitor_interval": "360", 
                    "points": "ctc,cuc,cmc", 
                    "bak_ip": "auto", 
                    "status": "Ok", 
                    "status_code": "200", 
                    "sms_notice": "me", 
                    "email_notice": "me", 
                    "less_notice": "yes", 
                    "callback_url": "", 
                    "callback_key": "", 
                    "monitor_status": "enabled", 
                    "created_on": "2012-11-24 20:47:51", 
                    "updated_on": "2012-11-24 20:47:51", 
                    "bak_ip_status": [ ]
                }
            ]
        }

Add A Monitor
---------
API Address：
    *  https://dnsapi.cn/Monitor.Create
HTTP Request Type：
    * POST
Request Parameters：
    * Global parameters
    * **domain_id** The domain id.Essential parameter.
    * **record_id** The record id.Essential parameter.
    * **port** The port number to monitor like 80.Essential parameter.
    * **monitor_interval** Monitoring spacing.Ranged {60|180|360|}.Essential parameter.
    * **host** The host from the http header like "www.dnspod.com".Essential parameter.
    * **monitor_type** {http|https} The monitor type.Essential parameter.
    * **monitor_path** The request path from the http header like "/".Essential parameter.
    * **points** The points to use.Split by ",".You can choose it from the list of your own grade.Essential parameter.
    * **bak_ip** Backup IP address.Choose one kind from the list blow:
        #. pass Just monitoring,no switching.
        #. pause The old type of pause.For more details,please visit: https://support.dnspod.cn/Kb/showarticle/tsid/179
        #. pause2 The intelligent pause who pause the record immediately when the IP is down.
        #. auto Switch intelligent.
        #. IP addresses split by ",".

    * **keep_ttl** TTL won't be changed if this is seted up.Essential parameter.
    * **sms_notice** "me" for the owner,and "share" for the shared users.Split by "," if there are more than one like "me,share".Essential parameter.
    * **email_notice** Same as the sms_notice.
    * **less_notice** {yes|no} Whether to just send one notice withen one hour.Essential parameter.
    * **callback_url** The callback URL.All the data will be sent to this URL when the IP is down.For more details,please see the directions.Optional parameter.
    * **callback_key** The callback key.If "callback_url" is set up,you shoul set this up too for sucurety.
Response Code：
    * Common response code.
    * 6 Invalid domain id.
    * 7 Invalid record id.
    * 8 Invalid host.
    * 9 Invalid monitor port number that range from 1 to 65535.
    * 10 Invalid monitor type.
    * 11 Invalid monitor path.
    * 12  Invalid monitor interval.
    * 13 Invalid monitor points.
    * 14 Too many points.
    * 15 Invalid backup IP.
    * 16 Invalid bakcup url.
    * 17 Invalid backup IP.
    * 18 Invalid sms notice.
    * 19 Invalid email notice.
    * 20 There is already been one monitor on this record.
    * 21 The number of you monitors is up to limit.
    * 22 Invalid callback URL.

Example::

    curl -X POST https://dnsapi.cn/Monitor.Create -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2317346&record_id=16909160&port=80&monitor_type=http&monitor_path=/&monitor_interval=360&points=ctc,cuc,cmc&bak_ip=pass&host=testapi.com'

Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 21:25:30"
            }, 
            "monitor": {
                "monitor_id": "6aac176e-363a-11e2-bab7-0819a6248970", 
                "record_id": 16909160
            }
        }

Modify A Monitor
---------
API Address：
    *  https://dnsapi.cn/Monitor.Modify
HTTP Request Type：
    * POST
Request Parameters：
    * Global parameters
    * **monitor_id** Monitor id.Essential parameter.
    * **port** The port number to minitor like 80.Essential parameter.
    * **monitor_interval** {60|180|360|} The monitor interval.Essential parameter.
    * **monitor_type** {http|https} The monitor type.Essential parameter.
    * **monitor_path** The path in the http header like "/".Essential parameter.
    * **points** The points to use.Split by ",".You can choose it from the list of your own grade.Essential parameter.
    * **bak_ip** Backup IP address.Choose one kind from the list blow:
        #. pass Just monitoring,no switching.
        #. pause The old type of pause.For more details,please visit: https://support.dnspod.cn/Kb/showarticle/tsid/179
        #. pause2 The intelligent pause who pause the record immediately when the IP is down.
        #. auto Switch intellgently.
        #. IP addresses split by ",".

    * **host** The host from the http header like "www.dnspod.com".Essential parameter.
    * **keep_ttl** TTL won't be changed if this is seted up.Essential parameter.
    * **sms_notice** "me" for the owner,and "share" for the shared users.Split by "," if there are more than one like "me,share".Essential parameter.
    * **email_notice** Same as the sms_notice.
    * **less_notice** {yes|no} Whether to just send one notice withen one hour.Essential parameter.
    * **callback_url**  The callback URL.All the data will be sent to this URL when the IP is down.For more details,please see the directions.Optional parameter.
    * **callback_key** The callback key.If "callback_url" is set up,you shoul set this up too for sucurety.
Response Code：
    * Common response code.
    * 7 Invalid monitor id.
    * 8 Invalid host.
    * 9 Invalid monitor port number that range from 1 to 65535.
    * 10 Invalid monitor type.
    * 11 Invalid monitor path.
    * 12  Invalid monitor interval.
    * 13 Invalid monitor points.
    * 14 Too many points.
    * 15 Invalid backup IP.
    * 16 Invalid bakcup url.
    * 17 Invalid backup IP.
    * 18 Invalid sms notice.
    * 19 Invalid email notice.
    * 22 Invalid callback URL.

Example::

    curl -X POST https://dnsapi.cn/Monitor.Modify -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2317346&monitor_id=51fc9a20-363c-11e2-bab7-0819a6248970&port=80&monitor_type=http&monitor_path=/&monitor_interval=360&points=ctc,cuc,cmc&bak_ip=pass'

Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 21:41:31"
            }
        }

Remove A Monitor
---------
API Address：
    *  https://dnsapi.cn/Monitor.Remove
HTTP Request Type：
    * POST
Request Parameters：
    * Global parameters
    * **monitor_id** I think we all know this is the monitor's id.
Response Code：
    * Common response code.
    * 6 Invalid monitor id.

Example::

    curl -X POST https://dnsapi.cn/Monitor.Modify -d 'login_email=api@dnspod.com&login_password=password&format=json&monitor_id=51fc9a20-363c-11e2-bab7-0819a6248970'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 21:51:49"
            }
        }


Get the Monitor Information
-------------
API Address：
    * https://dnsapi.cn/Monitor.Info
HTTP Request Type：
    * POST
Request Parameters：
    * Global parameters
    * **monitor_id** The monitor's id.
Response Code：
    * Common response code.
    * 7 Invalid monitor id.

Example::
        
    curl -X POST https://dnsapi.cn/Monitor.Info -d 'login_email=api@dnspod.com&login_password=password&format=json&monitor_id=e91997aa-3641-11e2-bab7-0819a6248970'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 22:19:58"
            }, 
            "info": {
                "monitor_id": "e91997aa-3641-11e2-bab7-0819a6248970", 
                "domain": "testapi.com", 
                "domain_id": "2317346", 
                "domain_grade": "D_Plus", 
                "record_id": "16909160", 
                "sub_domain": "@", 
                "record_line": "默认", 
                "ip": "119.180.24.194", 
                "now_ip": "119.180.24.194", 
                "host": "testapi.com", 
                "port": "80", 
                "monitor_type": "http", 
                "monitor_path": "/", 
                "monitor_interval": "180", 
                "points": "ctc,cuc,cmc", 
                "bak_ip": "pass", 
                "status": "Ok", 
                "status_code": "200", 
                "sms_notice": "me", 
                "email_notice": "me", 
                "less_notice": "no", 
                "callback_url": "", 
                "callback_key": "", 
                "monitor_status": "enabled", 
                "created_on": "2012-11-24 22:19:09", 
                "updated_on": "2012-11-24 22:19:09", 
                "bak_ip_status": [ ]
            }
        }

Set A Monitor's Status
-------------
API Address：
    *  https://dnsapi.cn/Monitor.Setstatus
HTTP Request Type：
    * POST
Request Parameters：
    * Global parameters
    * **monitor_id** Monitor id.Essential parameter.
    * **status** {enabled|disabled} The new status.Essential status.
Response Code：
    * Common response code.
    * 6 Invalid monitor id.
    * 7 Invalid new status.
    * 8 Please turn the domain on first.
    * 9 Please turn the record on first.
Response Code：
    * Common response code.
    * 6 Invalid monitor id.

Example::

    curl -X POST https://dnsapi.cn/Monitor.Setstatus -d 'login_email=api@dnspod.com&login_password=password&format=json&monitor_id=03e3b268-3643-11e2-bab7-0819a6248970&status=disable'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 22:33:20"
            }
        }

Get A Monitor's History
-------------
API Address：
    *  https://dnsapi.cn/Monitor.Gethistory
HTTP Request Type：
    * POST
Request Parameters：
    * Global parameters
    * **monitor_id** Monitor id.Essential parameter.
    * **hours** Within how many hours do you want to get the history.
Response Code：
    * Common response code.
    * 6 Invalid monitor id.

Example::

    curl -X POST https://dnsapi.cn/Monitor.Setstatus -d 'login_email=api@dnspod.com&login_password=password&format=json&monitor_id=03e3b268-3643-11e2-bab7-0819a6248970&hours=1'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 22:40:02"
            }, 
            "domain": {
                "id": "2317346", 
                "domain": "testapi.com", 
                "domain_grade": "D_Plus"
            }, 
            "record": {
                "id": "16909160", 
                "sub_domain": "@", 
                "ip": "119.180.24.194"
            }, 
            "monitor_history": [
                {
                    "data": {
                        "message": "ok", 
                        "code": 200, 
                        "data": [
                            {
                                "status": "Down", 
                                "status_code": -3, 
                                "createtime": "2012-11-24 22:28:31", 
                                "responsetime": 0
                            }, 
                            {
                                "status": "Down", 
                                "status_code": -3, 
                                "createtime": "2012-11-24 22:31:31", 
                                "responsetime": 0
                            }, 
                            {
                                "status": "Down", 
                                "status_code": -3, 
                                "createtime": "2012-11-24 22:34:31", 
                                "responsetime": 999
                            }, 
                            {
                                "status": "Down", 
                                "status_code": -3, 
                                "createtime": "2012-11-24 22:37:31", 
                                "responsetime": 1
                            }
                        ]
                    }, 
                    "point": "ctc"
                }, 
                {
                    "data": {
                        "message": "ok", 
                        "code": 200, 
                        "data": [
                            {
                                "status": "Down", 
                                "status_code": -3, 
                                "createtime": "2012-11-24 22:28:52", 
                                "responsetime": 0
                            }, 
                            {
                                "status": "Down", 
                                "status_code": -3, 
                                "createtime": "2012-11-24 22:31:52", 
                                "responsetime": 0
                            }, 
                            {
                                "status": "Down", 
                                "status_code": -3, 
                                "createtime": "2012-11-24 22:34:52", 
                                "responsetime": 0
                            }, 
                            {
                                "status": "Down", 
                                "status_code": -3, 
                                "createtime": "2012-11-24 22:37:52", 
                                "responsetime": 0
                            }
                        ]
                    }, 
                    "point": "cuc"
                }, 
                {
                    "data": {
                        "message": "ok", 
                        "code": 200, 
                        "data": [
                            {
                                "status": "Down", 
                                "status_code": -3, 
                                "createtime": "2012-11-24 22:30:07", 
                                "responsetime": 1
                            }, 
                            {
                                "status": "Down", 
                                "status_code": -3, 
                                "createtime": "2012-11-24 22:33:05", 
                                "responsetime": 0
                            }, 
                            {
                                "status": "Down", 
                                "status_code": -3, 
                                "createtime": "2012-11-24 22:36:06", 
                                "responsetime": 1
                            }, 
                            {
                                "status": "Down", 
                                "status_code": -3, 
                                "createtime": "2012-11-24 22:39:06", 
                                "responsetime": 1
                            }
                        ]
                    }, 
                    "point": "cmc"
                }
            ]
        }

Get A Monitor's Description
-------------
API Address：
    * https://dnsapi.cn/Monitor.Userdesc
HTTP Request Type：
    * POST
Request Parameters：
    * Global parameters
Response Code：
    * Common response code.

Example::

    curl -X POST https://dnsapi.cn/Monitor.Userdesc -d 'login_email=api@dnspod.com&login_password=password&format=json'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 22:50:14"
            }, 
            "desc": {
                "unmoniting_count": 3, 
                "moniting_count": 1, 
                "down_count": 1
            }, 
            "user": {
                "max_count": 28, 
                "use_count": 1
            }
        }


Get A Monitor's Wornings
-------------
API Address：
    *  https://dnsapi.cn/Monitor.Getdowns
HTTP Request Type：
    * POST
Request Parameters：
    * Global parameters
    * **offset** The offset of the response.The first is numbered 0.Optional parameter.
    * **length** The number of results you want get.Optional parameter.
Response Code：
    * Common response code.

Example::

    curl -X POST https://dnsapi.cn/Monitor.Getdowns -d 'login_email=api@dnspod.com&login_password=password&format=json&offset=0&length=10'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 22:54:03"
            }, 
            "info": {
                "total_count": "1"
            }, 
            "monitor_downs": [
                {
                    "monitor_id": "03e3b268-3643-11e2-bab7-0819a6248970", 
                    "host": "testapi.com", 
                    "record_line": "默认", 
                    "ip": "119.180.24.194", 
                    "warn_reason": "连接超时|访问您主机时连接超时，并且重试了5次后依然超时，建议您检查下你的服务器是否有网络不稳定的情况移动:timed out网通:timed out电信:timed out", 
                    "switch_log": [ ], 
                    "created_on": "2012-11-24 22:30:06", 
                    "updated_on": "0000-00-00 00:00:00"
                }
            ]
        }
