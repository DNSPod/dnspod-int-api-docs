Records
=======

Add a Record
------------
URL:
    * https://api.dnspod.com/Record.Create
HTTP Request Type:
    * POST
Request Parameters:
    * Global Parameters
    * **domain_id** The domain id. Mandatory parameter.
    * **sub_domain** The record name like "www".The default value is "@".Optional parameter.
    * **record_type** The record type.You can get the list of all allowed types from the API.Capital letters like "A" or "CNAME". Mandatory parameter.
    * **record_line** The record line.You can get the list from the API.The default value is "default", such as "default", "AD", "AE". Mandatory parameter.
    * **value** The record value.For example: IP:200.200.200.200, CNAME: cname.dnspod.com., MX: mail.dnspod.com. Mandatory parameter.
    * **mx** {1-20} This only need to and must be set when record_type is "MX".Range from 1 to 20.
    * **ttl** {1-604800}  TTL，range from 1 to 604800.Every grade has its own min value.Optional parameter.
Response Code:
    * Common Response Codes
    * -15 Domain got prohibited.
    * -7 A upgrade for the company account is needed before this.
    * -8 You need a upgrade for the domain you are acting for.
    * 6 Lack of parameters or something wrong with it.
    * 7 You don't have the permission.
    * 21 Domain got locked.
    * 22 Invalid sub_domain.
    * 23 Sub domain level is up to limit.
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

    curl -X POST https://api.dnspod.com/Record.Create -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2317346&sub_domain=@&record_type=A&record_line=default&value=1.1.1.1'
    
Response Example:

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
URL:
    * https://api.dnspod.com/Record.List
HTTP Request Type:
    * POST
Request Parameters:
    * Global Parameters
    * **domain_id** The domain id. Mandatory parameter.
    * **offset** The offset of the response.The first one is numbered as 0.Optional parameter.
    * **length** The number of response result.Optional parameter.
    * **sub_domain** If the subsidiary domain is set,only the information about it will be responded.
Response Code:
    * Common Response Codes
    * -7 A domain of a company account need a upgrade first.
    * -8 You need a upgrade for the domain you are acting for.
    * 6 Invalid domain id.
    * 7 Invalid offset.
    * 8 Invalid length.
    * 9 You don't have the permission.
    * 10 Empty result.

Attention:
    * If there are more than 500 records,only the first 500 will be responded.You may need to set "offset" and "length" to get all the records with requests.

Example::

     curl -X POST https://api.dnspod.com/Record.List -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2317346'
    
Response Example:

    * JSON::

       {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-05 09:58:40"
            },
            "domain": {
                "id": "9",
                "name": "dnspod.com",
                "punycode": "dnspod.com",
                "grade": "DP_Free",
                "owner": "yizerowu@dnspod.com"
            },
            "info": {
                "sub_domains": "5",
                "record_total": "5"
            },
            "records": [
                {
                    "id": "50",
                    "name": "@",
                    "line": "Default",
                    "type": "A",
                    "ttl": "600",
                    "value": "96.126.115.73",
                    "mx": "0",
                    "enabled": "1",
                    "status": "enabled",
                    "monitor_status": "",
                    "remark": "",
                    "updated_on": "2014-06-05 09:47:59"
                },
                {
                    "id": "49",
                    "name": "@",
                    "line": "Default",
                    "type": "MX",
                    "ttl": "600",
                    "value": "cloudmx.qq.com.",
                    "mx": "5",
                    "enabled": "1",
                    "status": "enabled",
                    "monitor_status": "",
                    "remark": "",
                    "updated_on": "2014-06-05 09:47:59"
                },
                {
                    "id": "46",
                    "name": "@",
                    "line": "Default",
                    "type": "NS",
                    "ttl": "600",
                    "value": "a.dnspod.com.",
                    "mx": "0",
                    "enabled": "1",
                    "status": "enabled",
                    "monitor_status": "",
                    "remark": "",
                    "updated_on": "2014-06-05 09:47:40",
                    "hold": "hold"
                },
                {
                    "id": "47",
                    "name": "@",
                    "line": "Default",
                    "type": "NS",
                    "ttl": "600",
                    "value": "b.dnspod.com.",
                    "mx": "0",
                    "enabled": "1",
                    "status": "enabled",
                    "monitor_status": "",
                    "remark": "",
                    "updated_on": "2014-06-05 09:47:40",
                    "hold": "hold"
                },
                {
                    "id": "48",
                    "name": "@",
                    "line": "Default",
                    "type": "NS",
                    "ttl": "600",
                    "value": "c.dnspod.com.",
                    "mx": "0",
                    "enabled": "1",
                    "status": "enabled",
                    "monitor_status": "",
                    "remark": "",
                    "updated_on": "2014-06-05 09:47:40",
                    "hold": "hold"
                }
            ]
        } 


Update a Record
---------------
URL:
    * https://api.dnspod.com/Record.Modify
HTTP Request Type:
    * POST
Request Parameters:
    * Global Parameters
    * **domain_id** The domain id. Mandatory parameter.
    * **record_id** The record id. Mandatory parameter.
    * **sub_domain** The record name like "www".The default value is "@".Optional parameter.
    * **record_type** The record type.You can get the list from the API.All capital letters like "A". Mandatory parameter.
    * **record_line** The record line.You can get the list from the API.The default value is "default", such as "default", "AD", "AE". Mandatory parameter.
    * **value** The record value.For example: IP:200.200.200.200, CNAME: cname.dnspod.com., MX: mail.dnspod.com. Mandatory parameter.
    * **mx** {1-20} This only need to and must be set when record_type is "MX".Range from 1 to 20.
    * **ttl** {1-604800} TTL，range from 1 to 604800.Every grade has its own min value.Optional parameter.
Response Code:
    * Common Response Codes
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
    * 35 The IP is not allowed.
    * 36 When the sub_domain is "@" and the record_type is "NS",the record_line can only be "default".

Example::

    curl -X POST https://api.dnspod.com/Record.Modify -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2317346&record_id=16894439&sub_domain=www&value=3.2.2.2&record_type=A&record_line=default'
   
Response Example:

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
URL:
    * https://api.dnspod.com/Record.Remove
HTTP Request Type:
    * POST
Request Parameters:
    * Global Parameters
    * **domain_id** The domain id. Mandatory parameter.
    * **record_id** The record id. Mandatory parameter.
Response Code:
    * Common Response Codes
    * -15 Domain got prohibited.
    * -7 A domain of a company account need a upgrade first.
    * -8 You need a upgrade for the domain you are acting for.
    * 6 Invalid domain id.
    * 7 You don't have the permission.
    * 8 Invalid record id.
    * 21 Domain got locked.

Example::

    curl -X POST https://api.dnspod.com/Record.Remove -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2317346&record_id=16894439'
    
Response Example:

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
URL:
    * https://api.dnspod.com/Record.Ddns
HTTP Request Type:
    * POST
Request Parameters:
    * Global Parameters
    * **domain_id** The domain id. Mandatory parameter.
    * **record_id** The record id. Mandatory parameter.
    * **sub_domain** The record name like "www".
    * **record_line** The record line.You can get the list from the API.The default value is "default", such as "default", "AD", "AE". Mandatory parameter.
    * **value** The IP address like "6.6.6.6".Optional parameter.
Response Code:
    * Common Response Codes
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

    curl -X POST https://api.dnspod.com/Record.Ddns -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2317346&record_id=16894439&record_line=default&sub_domain=www'
    
Response Example:

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
URL:
    * https://api.dnspod.com/Record.Remark
HTTP Request Type:
    * POST
Request Parameters:
    * Global Parameters
    * **domain_id** The domain id. Mandatory parameter.
    * **record_id** The record id. Mandatory parameter.
    * **remark** The remark information.Set it a empty string if you want to remove it. Mandatory parameter.
Response Code:
    * Common Response Codes
    * 6 Invalid domain id.
    * 8 Invalid record id.

Example::

    curl -X POST https://api.dnspod.com/Record.Remark -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2317346&record_id=16894439&remark=test'
    
Response Example:

    * JSON::

        {
            "status": {
                "code": "1", 
                "message": "Action completed successful", 
                "created_at": "2012-11-24 17:32:23"
            }
        }


Get the Record Information
--------------------------
URL:
    * https://api.dnspod.com/Record.Info
HTTP Request Type:
    * POST
Request Parameters:
    * Global Parameters
    * **domain_id** The domain id. Mandatory parameter.
    * **record_id** The record id. Mandatory parameter.
Response Code:
    * Common Response Codes
    * -15 Domain got prohibited.
    * -7 A domain of a company account need a upgrade first.
    * -8 You need a upgrade for the domain you are acting for.
    * 6 Invalid domain id.
    * 7 You don't have the permission.
    * 8 Invalid record id.

Example::

    curl -X POST https://api.dnspod.com/Record.Info -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2317346&record_id=16894439'
    
Response Example:

    * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-05 10:07:05"
            },
            "domain": {
                "id": "9",
                "domain": "dnspod.com",
                "domain_grade": "DP_Free"
            },
            "record": {
                "id": "50",
                "sub_domain": "@",
                "record_type": "A",
                "record_line": "Default",
                "value": "96.126.115.73",
                "mx": "0",
                "ttl": "600",
                "enabled": "1",
                "monitor_status": "",
                "remark": "",
                "updated_on": "2014-06-05 09:47:59",
                "domain_id": "9"
            }
        }


Set the Record Status
---------------------
URL:
    * https://api.dnspod.com/Record.Status
HTTP Request Type:
    * POST
Request Parameters:
    * Global Parameters
    * **domain_id** The domain id. Mandatory parameter.
    * **record_id** The record id. Mandatory parameter.
    * **status** {enable|disable} The new status. Mandatory parameter.
Response Code:
    * Common Response Codes
    * -15 Domain got prohibited.
    * -7 A domain of a company account need a upgrade first.
    * -8 You need a upgrade for the domain you are acting for.
    * 6 Invalid domain id.
    * 7 You don't have the permission.
    * 8 Invalid record id.
    * 21 Domain got locked.

Example:: 

    curl -X POST https://api.dnspod.com/Record.Status -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2317346&record_id=16894439&status=disable'
    
Response Example:

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
