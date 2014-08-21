D-Monitor
=========

List All the Sub-domains Whose Type Is "A"
------------------------------------------
URL：
    *  https://api.dnspod.com/Monitor.Listsubdomain
Method：
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

    curl -X POST https://api.dnspod.com/Monitor.Listsubdomain -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2317346'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-05 10:12:24"
            },
            "domain": {
                "id": "9",
                "name": "dnspod.com",
                "punycode": "dnspod.com",
                "grade": "DP_Free",
                "owner": "yizerowu@dnspod.com"
            },
            "subdomain": [
                "@"
            ]
        }


List All the "A" Records for a Sub-domain
-----------------------------------------
URL：
    *  https://api.dnspod.com/Monitor.Listsubvalue
Method：
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

    curl -X POST https://api.dnspod.com/Monitor.Listsubvalue -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2317346&subdomain=@'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-05 10:14:17"
            },
            "domain": {
                "id": "9",
                "name": "dnspod.com",
                "punycode": "dnspod.com",
                "grade": "DP_Free"
            },
            "points": {
                "max": 3,
                "list": {
                    "ctc-4": "Hangzhou, Telecom, CN",
                    "usa-1": "HE, CA, US",
                    "hk-1": "PCCW, HK"
                }
            },
            "balance": 8,
            "records": [
                {
                    "id": "50",
                    "area": "Default",
                    "value": "96.126.115.73",
                    "record_type": "A",
                    "sub_domain": "@"
                }
            ]
        }


Get the Monitor List
--------------------
URL：
    *  https://api.dnspod.com/Monitor.List
Method：
    * POST
Request Parameters：
    * Global parameters
Response Code：
    * Common response code.

Example::

    curl -X POST https://api.dnspod.com/Monitor.List -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2317346'
    
Response：

    * JSON::

       {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-05 10:21:00"
            },
            "info": {
                "total_count": 1,
                "down_count": 0
            },
            "monitors": [
                {
                    "monitor_id": "792626",
                    "domain": "usertest.com",
                    "domain_id": "15132",
                    "domain_grade": "DP_Free",
                    "record_id": "283118",
                    "sub_domain": "eeee",
                    "record_line": "Default",
                    "ip": "4.4.4.4",
                    "now_ip": "4.4.4.4",
                    "host": "eeee.usertest.com",
                    "port": "80",
                    "monitor_type": "http",
                    "monitor_path": "/",
                    "monitor_interval": "180",
                    "points": "hk-1,usa-1,ctc-4",
                    "bak_ip": "auto",
                    "status": "Ok",
                    "status_code": "200",
                    "sms_notice": "me",
                    "email_notice": "me",
                    "weixin_notice": "",
                    "less_notice": "yes",
                    "callback_url": "",
                    "callback_key": "",
                    "monitor_status": "enabled",
                    "created_on": "2014-06-05 10:20:41",
                    "updated_on": "2014-06-05 10:20:41",
                    "bak_ip_status": [],
                    "delay_notify": "60",
                    "warnasdown": "",
                    "sms2voice": ""
                }
            ]
        } 


Add a Monitor
-------------
URL：
    *  https://api.dnspod.com/Monitor.Create
Method：
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

    * **keep_ttl** TTL won't be changed if this is set up.Essential parameter.
    * **sms_notice** "me" for the owner,and "share" for the shared users.Split by "," if there are more than one like "me,share".Essential parameter.
    * **email_notice** Same as the sms_notice.
    * **less_notice** {yes|no} Whether to just send one notice within one hour.Essential parameter.
    * **callback_url** The callback URL.All the data will be sent to this URL when the IP is down.For more details,please see the directions.Optional parameter.
    * **callback_key** The callback key.If "callback_url" is set up,you should set this up too for security.
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
    * 16 Invalid backup url.
    * 17 Invalid backup IP.
    * 18 Invalid sms notice.
    * 19 Invalid email notice.
    * 20 There is already been one monitor on this record.
    * 21 The number of you monitors is up to limit.
    * 22 Invalid callback URL.

Example::

    curl -X POST https://api.dnspod.com/Monitor.Create -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2317346&record_id=16909160&port=80&monitor_type=http&monitor_path=/&monitor_interval=360&points=ctc,cuc,cmc&bak_ip=pass&host=testapi.com'

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

Modify a Monitor
----------------
URL：
    *  https://api.dnspod.com/Monitor.Modify
Method：
    * POST
Request Parameters：
    * Global parameters
    * **monitor_id** Monitor id.Essential parameter.
    * **port** The port number to monitor like 80.Essential parameter.
    * **monitor_interval** {60|180|360|} The monitor interval.Essential parameter.
    * **monitor_type** {http|https} The monitor type.Essential parameter.
    * **monitor_path** The path in the http header like "/".Essential parameter.
    * **points** The points to use.Split by ",".You can choose it from the list of your own grade.Essential parameter.
    * **bak_ip** Backup IP address.Choose one kind from the list blow:
        #. pass Just monitoring,no switching.
        #. pause The old type of pause.For more details,please visit: https://support.dnspod.cn/Kb/showarticle/tsid/179
        #. pause2 The intelligent pause who pause the record immediately when the IP is down.
        #. auto Switch intelligently.
        #. IP addresses split by ",".

    * **host** The host from the http header like "www.dnspod.com".Essential parameter.
    * **keep_ttl** TTL won't be changed if this is set up.Essential parameter.
    * **sms_notice** "me" for the owner,and "share" for the shared users.Split by "," if there are more than one like "me,share".Essential parameter.
    * **email_notice** Same as the sms_notice.
    * **less_notice** {yes|no} Whether to just send one notice within one hour.Essential parameter.
    * **callback_url**  The callback URL.All the data will be sent to this URL when the IP is down.For more details,please see the directions.Optional parameter.
    * **callback_key** The callback key.If "callback_url" is set up,you should set this up too for security.
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
    * 16 Invalid backup url.
    * 17 Invalid backup IP.
    * 18 Invalid sms notice.
    * 19 Invalid email notice.
    * 22 Invalid callback URL.

Example::

    curl -X POST https://api.dnspod.com/Monitor.Modify -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2317346&monitor_id=51fc9a20-363c-11e2-bab7-0819a6248970&port=80&monitor_type=http&monitor_path=/&monitor_interval=360&points=ctc,cuc,cmc&bak_ip=pass'

Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 21:41:31"
            }
        }

Remove a Monitor
----------------
URL：
    *  https://api.dnspod.com/Monitor.Remove
Method：
    * POST
Request Parameters：
    * Global parameters
    * **monitor_id** I think we all know this is the monitor's id.
Response Code：
    * Common response code.
    * 6 Invalid monitor id.

Example::

    curl -X POST https://api.dnspod.com/Monitor.Modify -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&monitor_id=51fc9a20-363c-11e2-bab7-0819a6248970'
    
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
---------------------------
URL：
    * https://api.dnspod.com/Monitor.Info
Method：
    * POST
Request Parameters：
    * Global parameters
    * **monitor_id** The monitor's id.
Response Code：
    * Common response code.
    * 7 Invalid monitor id.

Example::
        
    curl -X POST https://api.dnspod.com/Monitor.Info -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&monitor_id=e91997aa-3641-11e2-bab7-0819a6248970'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-05 10:23:16"
            },
            "info": {
                "monitor_id": "792626",
                "domain": "usertest.com",
                "domain_id": "15132",
                "domain_grade": "DP_Free",
                "record_id": "283118",
                "sub_domain": "eeee",
                "record_line": "Default",
                "ip": "4.4.4.4",
                "now_ip": "4.4.4.4",
                "host": "eeee.usertest.com",
                "port": "80",
                "monitor_type": "http",
                "monitor_path": "/",
                "monitor_interval": "180",
                "points": "hk-1,usa-1,ctc-4",
                "bak_ip": "auto",
                "status": "Ok",
                "status_code": "200",
                "sms_notice": "me",
                "email_notice": "me",
                "less_notice": "yes",
                "callback_url": "",
                "callback_key": "",
                "monitor_status": "enabled",
                "created_on": "2014-06-05 10:20:41",
                "updated_on": "2014-06-05 10:20:41",
                "bak_ip_status": []
            }
        }


Set a Monitor's Status
----------------------
URL：
    *  https://api.dnspod.com/Monitor.Setstatus
Method：
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

    curl -X POST https://api.dnspod.com/Monitor.Setstatus -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&monitor_id=03e3b268-3643-11e2-bab7-0819a6248970&status=disable'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 22:33:20"
            }
        }

Get a Monitor's History
-----------------------
URL：
    *  https://api.dnspod.com/Monitor.Gethistory
Method：
    * POST
Request Parameters：
    * Global parameters
    * **monitor_id** Monitor id.Essential parameter.
    * **hours** Within how many hours do you want to get the history.
Response Code：
    * Common response code.
    * 6 Invalid monitor id.

Example::

    curl -X POST https://api.dnspod.com/Monitor.Setstatus -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&monitor_id=03e3b268-3643-11e2-bab7-0819a6248970&hours=1'
    
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

Get a Monitor's Description
---------------------------
URL：
    * https://api.dnspod.com/Monitor.Userdesc
Method：
    * POST
Request Parameters：
    * Global parameters
Response Code：
    * Common response code.

Example::

    curl -X POST https://api.dnspod.com/Monitor.Userdesc -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json'
    
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


Get a Monitor's Warnings
------------------------
URL：
    *  https://api.dnspod.com/Monitor.Getdowns
Method：
    * POST
Request Parameters：
    * Global parameters
    * **offset** The offset of the response.The first is numbered 0.Optional parameter.
    * **length** The number of results you want get.Optional parameter.
Response Code：
    * Common response code.

Example::

    curl -X POST https://api.dnspod.com/Monitor.Getdowns -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&offset=0&length=10'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-05 10:25:04"
            },
            "info": {
                "total_count": "1"
            },
            "monitor_downs": [
                {
                    "down_id": "15132",
                    "monitor_id": "792626",
                    "host": "eeee.usertest.com",
                    "record_line": "Default",
                    "ip": "4.4.4.4",
                    "warn_reason": "Connection timed out",
                    "switch_log": [
                        "2014-06-05 10:24:28 No available spare server to switch to"
                    ],
                    "created_on": "2014-06-05 10:23:14",
                    "updated_on": "0000-00-00 00:00:00"
                }
            ]
        }
