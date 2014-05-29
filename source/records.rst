Records
=======

Add a Record
------------
URL：
    * https://api.dnspod.com/Record.Create
Method：
    * POST
Request Parameters：
    * Global parameters
    * **domain_id** The domain id.Essential parameter.
    * **sub_domain** The record name like "www".The default value is "@".Optional parameter.
    * **record_type** The record type.You can get the list of all allowed types from the API.Capital letters like "A" or "CNAME".Essential parameter.
    * **record_line** The record line.You can get the list of all allowed lines from the API.Essential parameter.
    * **value** The record value.For example: IP:200.200.200.200, CNAME: cname.dnspod.com., MX: mail.dnspod.com.Essential parameter.
    * **mx** {1-20} This only need to and must be seted when record_type is "MX".Range from 1 to 20.
    * **ttl** {1-604800}  TTL，range from 1 to 604800.Every grade has its own min value.Optional parameter.
Response Code：
    * Common response code.
    * -15 Domain got prohibited.
    * -7 A upgrade for the company account is needed before this.
    * -8 You need a upgrae for the domain you are acting for.
    * 6 Lack of parameters or something wrong with it.
    * 7 You don't have the permission.
    * 21 Domain got locked.
    * 22 Invalid sub_domain.
    * 23 Sub domain level is up to limie.
    * 24 Invalid sub domain for general analysis.
    * 25 The number of poll is up to limit.
    * 26 Invalid line.
    * 27 Invalid record type.
    * 30 Invalid MX value.
    * 31 The number of URL record is up to limit.
    * 32 The number of NS record is up to limit.
    * 33 The number of AAAA record is up to limit.
    * 34 Invalid record value.
    * 36 When the sub_domain is "@" and the record_type is "NS",the record_line can only be "default".

Example::

    curl -X POST https://api.dnspod.com/Record.Create -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2317346&sub_domain=@&record_type=A&record_line=默认&value=1.1.1.1'
    
Response：

    * JSON::

        {
            "status": {
                "code":"1",
                "message":"Action completed successful",
                "created_at":"2012-11-23 22:17:47"
            },
            "record": {
                "id":"16894439",
                "name":"@",
                "status":"enable"
            }
        }

Get Record List
---------------
URL：
    * https://api.dnspod.com/Record.List
Method：
    * POST
Request Parameters：
    * Global parameters
    * **domain_id** The domain id.Essential parameter.
    * **offset** The offset of the response.The first one is numbered as 0.Optional parameter.
    * **length** The number of response result.Optional parameter.
    * **sub_domain** If the subsidiary domain is set,only the information about it will be responsed.
Response Code：
    * Common response code.
    * -7 A domain of a company account need a upgrade first.
    * -8 You need a upgrade for the domain you are acting for.
    * 6 Invalid domain id.
    * 7 Invalid offset.
    * 8 Invalid length.
    * 9 You don't have the permission.
    * 10 Empty result.

Attention：
    * If there are more than 3000 records,only the first 3000 will be responsed.You may need to set "offset" and "length" to get all the records with requests.

Example::

     curl -X POST https://api.dnspod.com/Record.List -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2317346'
    
Response：

    * JSON::

        {
            "status": {
                "code":"1",
                "message":"Action completed successful",
                "created_at":"2012-11-23 22:20:59"
            },
            "domain": {
                "id":2317346,
                "name":"testapi.com",
                "punycode":"testapi.com",
                "grade":"D_Plus",
                "owner":"api@dnspod.com"
            },
            "info": {
                "sub_domains":"3",
                "record_total":"3"
            },
            "records": [
                {
                    "id":"16894439",
                    "name":"@",
                    "line":"\u9ed8\u8ba4",
                    "type":"A",
                    "ttl":"600",
                    "value":"1.1.1.1",
                    "mx":"0",
                    "enabled":"1",
                    "status":"enabled",
                    "monitor_status":"",
                    "remark":"",
                    "updated_on":"2012-11-23 22:17:47"
                },
                {
                    "id":"16662141",
                    "name":"@",
                    "line":"\u9ed8\u8ba4",
                    "type":"NS",
                    "ttl":"600",
                    "value":"ns1.dnsv2.com.",
                    "mx":"0",
                    "enabled":"1",
                    "status":"enabled",
                    "monitor_status":"",
                    "remark":"",
                    "updated_on":"2012-11-16 15:52:56",
                    "hold":"hold"
                },
                {
                    "id":"16662142",
                    "name":"@",
                    "line":"\u9ed8\u8ba4",
                    "type":"NS",
                    "ttl":"600",
                    "value":"ns2.dnsv2.com.",
                    "mx":"0",
                    "enabled":"1",
                    "status":"enabled",
                    "monitor_status":"",
                    "remark":"",
                    "updated_on":"2012-11-16 15:52:56",
                    "hold":"hold"
                }
            ]
        }

Update a Record
---------------
URL：
    *  https://api.dnspod.com/Record.Modify
Method：
    * POST
Request Parameters：
    * Global parameters
    * **domain_id** The domain id.Essential parameter.
    * **record_id** The record id.Essential parameter.
    * **sub_domain** The record name like "www".The default value is "@".Optional parameter.
    * **record_type** The record type.You can get the list from the API.All capital letters like "A".Essential parameter.
    * **record_line** The record line.You can get the list from the API.The default value is "default".Essential parameter.
    * **value** The record value.For example: IP:200.200.200.200, CNAME: cname.dnspod.com., MX: mail.dnspod.com.Essential parameter.
    * **mx** {1-20} This only need to and must be seted when record_type is "MX".Range from 1 to 20.
    * **ttl** {1-604800} TTL，range from 1 to 604800.Every grade has its own min value.Optional parameter.
Response Code：
    * Common response code.
    * -15 Domain got prohibited.
    * -7 A domain of a company account need a upgrade first.
    * -8 You need a upgrade for the domain you are acting for.
    * 6 Invalid domain id.
    * 7 You don't have the permission.
    * 8 Invalid record id.
    * 21 Domain got locked.
    * 22 Invalid sub domain.
    * 23 The number of the record level is up to limit.
    * 24 Invalid sub domain for general analysis.
    * 25 The number of poll is up to limit.
    * 26 Invalid record line.
    * 27 Invalid record type.
    * 29 TTL is too small.
    * 30 Invalid MX value.
    * 31 The number of URL records is up to limit.
    * 32 The number of NS records is up to limit.
    * 33 The number of AAAA records is up to limit.
    * 34 Invalid record value.
    * 35 The IP is not allowd.
    * 36 When the sub_domain is "@" and the record_type is "NS",the record_line can only be "default".

Example::

    curl -X POST https://api.dnspod.com/Record.Modify -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2317346&record_id=16894439&sub_domain=www&value=3.2.2.2&record_type=A&record_line=默认'
   
Response：

    * JSON::

        {
            "status": {
                "code":"1",
                "message":"Action completed successful",
                "created_at":"2012-11-24 16:53:23"
            },
            "record": {
                "id":16894439,
                "name":"@",
                "value":"3.2.2.2","status":"enable"
            }
        }

Remove a Record
---------------
URL：
    *  https://api.dnspod.com/Record.Remove
Method：
    * POST
Request Parameters：
    * Global parameters
    * **domain_id** The domain id.Essential parameter.
    * **record_id** The record id.Essential parameter.
Response Code：
    * Common response code.
    * -15 Domain got prohibited.
    * -7 A domain of a company account need a upgrade first.
    * -8 You need a upgrade for the domain you are acting for.
    * 6 Invalid domain id.
    * 7 You don't have the permission.
    * 8 Invalid record id.
    * 21 Domain got locked.

Example::

    curl -X POST https://api.dnspod.com/Record.Remove -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2317346&record_id=16894439'
    
Response：

    * JSON::

        {
            "status": {
                "code":"1",
                "message":"Action completed successful",
                "created_at":"2012-11-24 16:58:07"
            }
        }

Update the Dynamic DNS Record
-----------------------------
URL：
    *  https://api.dnspod.com/Record.Ddns
Method：
    * POST
Request Parameters：
    * Global parameters
    * **domain_id** The domain id.Essential parameter.
    * **record_id** The record id.Essential parameter.
    * **sub_domain** The record name like "www".
    * **record_line** The record line.You can get the list from the API.The default value is "default".Essential parameter.
    * **value** The IP address like "6.6.6.6".Optional parameter.
Response Code：
    * Common response code.
    * -15 Domain got prohibited.
    * -7 A domain of a company account need a upgrade first.
    * -8 You need a upgrade for the domain you are acting for.
    * 6 Invalid domain id.
    * 7 You don't have the permission.
    * 8 Invalid record id.
    * 21 Domain got locked.
    * 22 Invalid sub domain.
    * 23 The number of the record level is up to limit.
    * 24 Invalid sub domain for general analysis.
    * 25 The number of poll is up to limit.
    * 26 Invalid record line.

Example::

    curl -X POST https://api.dnspod.com/Record.Ddns -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2317346&record_id=16894439&record_line=默认&sub_domain=www'
    
Response：

    * JSON::

        { 
            "status": {
                "code":"1",
                "message":"Action completed successful",
                "created_at":"2012-11-24 17:23:58"
            },
            "record": {
                "id":16909160,
                "name":"@",
                "value":"111.111.111.111"
            }
        }

Remark a Record
---------------
URL：
    *  https://api.dnspod.com/Record.Remark
Method：
    * POST
Request Parameters：
    * Global parameters
    * **domain_id** The domain id.Essential parameter.
    * **record_id** The record id.Essential parameter.
    * **remark** The remark information.Set it a empty string if you want to remove it.Essential parameter.
Response Code：
    * Common response code.
    * 6 Invalid domain id.
    * 8 Invalid record id.

Example::

    curl -X POST https://api.dnspod.com/Record.Remark -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2317346&record_id=16894439&remark=test'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 17:32:23"
            }
        }


Get the Record Informtion
-------------------------
URL：
    *  https://api.dnspod.com/Record.Info
Method：
    * POST
Request Parameters：
    * Global parameters
    * **domain_id** The domain id.Essential parameter.
    * **record_id** The record id.Essential parameter.
Response Code：
    * Common response code.
    * -15 Domain got prohibited.
    * -7 A domain of a company account need a upgrade first.
    * -8 You need a upgrade for the domain you are acting for.
    * 6 Invalid domain id.
    * 7 You don't have the permission.
    * 8 Invalid record id.

Example::

    curl -X POST https://api.dnspod.com/Record.Info -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2317346&record_id=16894439'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 17:36:10"
            }, 
            "domain": {
                "id": 2317346, 
                "domain": "testapi.com", 
                "domain_grade": "D_Plus"
            }, 
            "record": {
                "id": "16909160", 
                "sub_domain": "@", 
                "record_type": "A", 
                "record_line": "默认", 
                "value": "111.111.111.111", 
                "mx": "0", 
                "ttl": "10", 
                "enabled": "1", 
                "monitor_status": "", 
                "remark": "test", 
                "updated_on": "2012-11-24 17:23:58", 
                "domain_id": "2317346"
            }
        }


Set the Record Status
---------------------
URL：
    *  https://api.dnspod.com/Record.Status
Method：
    * POST
Request Parameters：
    * Global parameters
    * **domain_id** The domain id.Essential parameter.
    * **record_id** The record id.Essential parameter.
    * **status** {enable|disable} The new status.Essential parameter.
Response Code：
    * Common response code.
    * -15 Domain got prohibited.
    * -7 A domain of a company account need a upgrade first.
    * -8 You need a upgrade for the domain you are acting for.
    * 6 Invalid domain id.
    * 7 You don't have the permission.
    * 8 Invalid record id.
    * 21 Domain got locked.

Example:: 

    curl -X POST https://api.dnspod.com/Record.Status -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2317346&record_id=16894439&status=disable'
    
Response：

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 20:07:29"
            }, 
            "record": {
                "id": 16909160, 
                "name": "@", 
                "status": "disable"
            }
        }
