Domains
=======

Add New Domain
--------------
URL：
    * https://api.dnspod.com/Domain.Create
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain** The domain to add. No prefix.Example:dnspod.com
    * **group_id** The domain group ID. Optional parameter.
    * **is_mark** {yes|no} Whether to mark it or not. Optional parameter.
Response Code：
    * Common Response Code
    * 6 Invalid domain.
    * 7 Domain already exists.
    * 11 Domain already exists as an alias of another domain.
    * 12 Domain already exists on which you have no permit to operate.
    * 41 The website falls short of the term of service of DNSPod.

Example::

    curl -X POST https://api.dnspod.com/Domain.Create -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&domain=api2.com&format=json'

Response：

    * JSON::
        
        {
            "status": {
                "code":"1",
                "message":"Action completed successful",
                "created_at":"2012-08-29 22:12:35"
            },
            "domain": {
                "id":"1992403",
                "punycode":"api2.com",
                "domain":"api2.com"
            }
        }


Get The Domain List
-------------------
URL：
    * https://api.dnspod.com/Domain.List
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **type** The domain type.Optional parameter.Default value:'all'.Here are all the choseable values :
        * all：All the domains
        * mine：Only mine.
        * share：Domains that shared with me.
        * ismark：Marked domains.
        * pause：Paused domains.
        * vip：VIP domains.
        * recent：Domains operated recentily.
        * share_out：Domains that I shared out.
    * **offset** The offset of the response.Optional parameter.The first domain is numbered as 0.
    * **length** The number of domains you want to get on this request.Optional parameter.
    * **group_id** The group ID.Only in this group can the domain be in the results if this parameter is seted.Optional parameter.
Attention：
    * If there are more than 500 domains in your account,only the first 500 domains will responsed for split page.You may need to set the parameter "offset" and "length" to get all your domains with multi requests.
Response Code：
    * Common Response Code
    * 6 Invalid offset.
    * 7 Invalid length.
    * 9 Empty result.

Example::
    
    curl -X POST https://api.dnspod.com/Domain.List -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json'

Response：

   * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-04 21:22:08"
            },
            "info": {
                "domain_total": 1,
                "all_total": 1,
                "mine_total": 1,
                "share_total": 0,
                "vip_total": 0,
                "ismark_total": 0,
                "pause_total": 0,
                "error_total": 1,
                "lock_total": 0,
                "spam_total": 0,
                "vip_expire": 0,
                "share_out_total": 0
            },
            "domains": [
                {
                    "id": 6,
                    "name": "dnspod.com",
                    "grade": "DP_Free",
                    "grade_title": "Free",
                    "status": "enable",
                    "ext_status": "notexist",
                    "records": "3",
                    "group_id": "1",
                    "is_mark": "no",
                    "remark": "",
                    "is_vip": "no",
                    "searchengine_push": "yes",
                    "beian": "no",
                    "created_on": "2014-06-04 16:19:31",
                    "updated_on": "2014-06-04 16:20:05",
                    "ttl": "600",
                    "owner": "yizero@qq.com"
                }
            ]
        }


Delete Domain
-------------
URL：
    * https://api.dnspod.com/Domain.Remove
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
Response Code：
    * Common Response Code
    * -15 Domain got prohibited.
    * 6 Invalid domain id.
    * 7 Domain got locked.
    * 8 VIP domains is not allowed to delete.
    * 9 You have no permit to do this.

Example::

    curl -X POST https://api.dnspod.com/Domain.Remove -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=1992403'
    
Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-12 11:09:31"
            }
        }

Set Domain Status
-----------------
URL：
    * https://api.dnspod.com/Domain.Status
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
    * **status** {enable, disable} The domain status.
Response Code：
    * Common Response Code
    * -15 Domain got prohibited.
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 7 Domain got locked.
    * 8 You have no permit to do this.

Example::

    curl -X POST https://api.dnspod.com/Domain.Status -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2058967&status=disable'

Response：

    * JSON::
            
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-12 12:02:04"
            }
        }

Get The Domain Information
--------------------------
URL：
    * https://api.dnspod.com/Domain.Info
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
Response Code：
    * Common Response Code
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 8 You have no permit to do this.

Example::

    curl -X POST https://api.dnspod.com/Domain.Info  -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079'

Response：

    * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-04 21:25:21"
            },
            "domain": {
                "id": "6",
                "name": "dnspod.com",
                "punycode": "dnspod.com",
                "grade": "DP_Free",
                "grade_title": "Free",
                "status": "enable",
                "ext_status": "notexist",
                "records": "3",
                "group_id": "1",
                "is_mark": "no",
                "remark": false,
                "is_vip": "no",
                "searchengine_push": "yes",
                "beian": "no",
                "user_id": "730060",
                "created_on": "2014-06-04 16:19:31",
                "updated_on": "2014-06-04 16:20:05",
                "ttl": "600",
                "owner": "yizero@qq.com"
            }
        }


Get the Operate Logs of a Domain
--------------------------------
URL：
    * https://api.dnspod.com/Domain.Log
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
Response Code：
    * Common Response Code
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 8 You have no permit to do this.

Example::
    
    curl -X POST https://api.dnspod.com/Domain.Log  -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079'

Response：

    * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-04 21:31:00"
            },
            "log": [
                "There is no domain logs at the moment."
            ],
            "info": {
                "count": 0,
                "page_size": 500
            }
        } 


Push Domain to Search Engine
----------------------------
URL：
    * https://api.dnspod.com/Domain.Searchenginepush
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
    * **status** {yes,no} Whether to push it.
Response Code：
    * Common Response Code
    * -15 Domain got prohibited.
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 7 Domain got locked.
    * 8 You have no permit to do this.

Example::

    curl -X POST https://api.dnspod.com/Domain.Searchenginepush -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&status=yes'
    
Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 17:28:44"
            }
        }


Share a Domain
--------------
URL：
    * https://api.dnspod.com/Domainshare.Create
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
    * **email** The email address with who you want to share.
    * **mode** {r,rw} The share mode."r" stands for "read only",and "rw" stands for "read and write".The default value is "r".
    * **sub_domain** The subsidiary domain you want to share,like "www" or "bbs".Don't set this parameter if you want to share the whole domain.

Response Code：
    * Common Response Code
    * -15 Domain got prohibited.
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 7 Invalid target email address.
    * 8 The target email address not exists.
    * 9 The share already exists.
    * 10 Your shared number is up to limit.

Example::

    curl -X POST https://api.dnspod.com/Domainshare.Create -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&email=otheruser@dnspod.com&mode=rw'
    
Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 17:47:21"
            }
        }
    
Get Domain Share List
---------------------
URL：
    * https://api.dnspod.com/Domainshare.List
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
Response Code：
    * Common Response Code
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 7 No share records.

Example::
    
    curl -X POST https://api.dnspod.com/Domainshare.List -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079'

Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 17:51:50"
            },
            "share": [
                {
                    "share_to": "yizerowu@dnspod.com",
                    "mode": "rw",
                    "status": "enabled"
                }
            ],
            "owner": "api@dnspod.com"
        }

Update the Domain Share
-----------------------
URL：
    * https://api.dnspod.com/Domainshare.Modify
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
    * **email** The original target email address.Don's change it.
    * **mode** {r,rw} Share mode."r" stands for "read only",and "rw" stands for "read and write".The default value is "r".
    * **old_sub_domain** The old subsidiary domain that already shared.This parameter shouldn't be seted if you want to update the domain name.
    * **new_sub_domain** The new subsidiary domain.
Response Code：
    * Common Response Code
    * -15 Domain got prohibited.
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 7 Invalid email address.
    * 8 The email address not exists.
    * 9 There's no share for this email address.

Example

1. Change a domain's share mode from "rw" to "r"::
        
    curl -X POST https://api.dnspod.com/Domainshare.Modify -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&email=yizerowu@dnspod.com&mode=r'
    
2. Change a domain's share mode from "rw" to "r"::
            
    curl -X POST https://api.dnspod.com/Domainshare.Modify -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&email=yizerowu@dnspod.com&mode=r&old_sub_domain=www&new_sub_domain=www'
    
3. Change a domain's share type from the whole domain to subsidiary domain.::

    curl -X POST https://api.dnspod.com/Domainshare.Modify -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&email=yizerowu@dnspod.com&mode=rw&new_sub_domain=www'
    
4. Change a domain's share type from subsidiary domain to the whole domain.::

    curl -X POST https://api.dnspod.com/Domainshare.Modify -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&email=yizerowu@dnspod.com&mode=rw&old_sub_domain=www'
    
5. Change the subsidiary domain from "www" to "bbs"::

    curl -X POST https://api.dnspod.com/Domainshare.Modify -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&email=yizerowu@dnspod.com&mode=rw&old_sub_domain=www&new_sub_domain=bbs'
    
Response：

   * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 18:54:18"
            }
        } 

Delete a Domain Share
---------------------
URL：
    *  https://api.dnspod.com/Domainshare.Remove
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
    * **email** The original email address.
Response Code：
    * Common Response Code
    * -15 Domain got prohibited.
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 7 Invalid email address.
    * 8 The email address not exists.
    * 9 There's no share for this email address.

Example::
    
    curl -X POST https://api.dnspod.com/Domainshare.Remove -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&email=yizerowu@dnspod.com'

Response：

    * JSON::    
    
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 20:19:20"
            }
        }

Transfer a Domain to Another Account
------------------------------------
URL：
    * https://api.dnspod.com/Domain.Transfer
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
    * **email** The original email address.
Response Code：
    * Common Response Code
    * -15 Domain got prohibited.
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 7 Invalid email address.
    * 8 Email address not exists.
    * 9 You cannt transfer it to yourself.
    * 10 You can't transfer a domain from a persional account to a company account.
    * 11 You can't transfer a domain from a company account to a persional account.

Example::
    
    curl -X POST https://api.dnspod.com/Domainshare.Transfer -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&email=yizerowu@dnspod.com'
    
Response：

    * JSON::    
    
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 20:21:33"
            }
        }

Lock a Domain
-------------
URL：
    * https://api.dnspod.com/Domain.Lock
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** The domain ID
    * **days** For how many days.
Response Code：
    * Common Response Code
    * -15 Domain got prohibited.
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 7 You don't have the permission.
    * 8 Wrong parameter "days".
    * 9 The parameter "days" is too big.
    * 21 Domain is already locked.

Example::
    
    curl -X POST https://api.dnspod.com/Domain.Lock -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&days=3'

Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 20:31:13"
            },
            "lock": {
                "domain_id": 2059079,
                "lock_code": "fdd638",
                "lock_end": "2012-09-21"
            }
        }

Lock Status
-----------
URL：
    * https://api.dnspod.com/Domain.Lockstatus
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
Response Code：
    * Common Response Code
    * -15 Domain got prohibited.
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 7 The domain is not locked.

Example::
    
    curl -X POST https://api.dnspod.com/Domain.Lockstatus -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079'
    
Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 20:35:04"
            },
            "lock": {
                "lock_status": "yes",
                "start_at": "2012-09-18",
                "end_at": "2012-09-21"

            }
        }

Domain Unlock
-------------
URL：
    * https://api.dnspod.com/Domain.Unlock
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
    * **lock_code** The code that you will get when you lock the domain.
Response Code：
    * Common Response Code
    * -15 Domain got prohibited.
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 7 You don't have the permission.
    * 8 The domain is not locked.
    * 9 Invalid lock code.

Example::
    
    curl -X POST https://api.dnspod.com/Domain.Unlock -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&lock_code=fdd638'

Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 20:38:58"
            },
            "lock": {
                "lock_status": "yes",
                "start_at": "2012-09-18",
                "end_at": "2012-09-21"
            }
        }

Get Domain Alias List
---------------------
URL：
    * https://api.dnspod.com/Domainalias.List
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
Response Code：
    * Common Response Code
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 7 Empty result.

Example::
    
    curl -X POST https://api.dnspod.com/Domainalias.List -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079'

Response：

   * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 21:11:20"
            },
            "alias": [
                {
                    "id": "18737",
                    "domain": "dnspodapi.com"
                }
            ]
        } 


Add a Domain Alias
------------------
URL：
    * https://api.dnspod.com/Domainalias.Create
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** The domain ID.
    * **domain** The domain to bind.Without "www".
Response Code：
    * Common Response Code
    * -15 Domain got prohibited.
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 7 Invalid domain.
    * 8 The domain is already added.
    * 9 The domain already exists.
    * 10 The number of domains is up to limit.

Example::
    
    curl -X POST https://api.dnspod.com/Domainalias.Create -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&domain=dnspodapi.com'

Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 21:09:57"
            },
            "alias": {
                "id": "18737",
                "punycode": "dnspodapi.com"
            }
        }

Remove a Domain Alias
---------------------
URL：
    * https://api.dnspod.com/Domainalias.Remove
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
    * **alias_id** The alias id that you will get when you create it.
Response Code：
    * Common Response Code
    * -15 Domain got prohibited.
    * -7 The company account need a upgrade before doing this.
    * -8 You need a upgrade for the domains you are acting for.
    * 6 Invalid domain id.
    * 7 Invalid alias id.

Example::
    
    curl -X POST https://api.dnspod.com/Domainalias.Remove -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&alias_id=18737'

Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 21:15:20"
            }
        }

Get The Domain Group List
-------------------------
URL：
    * https://api.dnspod.com/Domaingroup.List
Method：
    * POST
Request Parameters：
    * Global Parameters
Response Code：
    * Common Response Code

Example::
    
    curl -X POST https://api.dnspod.com/Domaingroup.List -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json'
    
Response：

    * JSON::
        
       {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-04 21:50:38"
            },
            "groups": [
                {
                    "group_id": 1,
                    "group_name": "Default Group",
                    "group_type": "system",
                    "size": 1
                },
                {
                    "group_id": 2,
                    "group_name": "Often Change",
                    "group_type": "system",
                    "size": 0
                },
                {
                    "group_id": 3,
                    "group_name": "Few Change",
                    "group_type": "system",
                    "size": 0
                },
                {
                    "group_id": 4,
                    "group_name": "Expiring",
                    "group_type": "system",
                    "size": 0
                },
                {
                    "group_id": 5,
                    "group_name": "Personal Domain",
                    "group_type": "system",
                    "size": 0
                },
                {
                    "group_id": 6,
                    "group_name": "Company Domain",
                    "group_type": "system",
                    "size": 0
                },
                {
                    "group_id": 7,
                    "group_name": "Customer Domain",
                    "group_type": "system",
                    "size": 0
                },
                {
                    "group_id": 8,
                    "group_name": "Shared To Me",
                    "group_type": "system",
                    "size": 0
                }
            ]
        } 

    
Add a New Domain Group
----------------------
URL：
    https://api.dnspod.com/Domaingroup.Create
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **group_name** I think you know what this stands for.
Response Code：
    * Common Response Code
    * 7 Invalid group name.
    * 8 The group name already exists.
    * 9 The number of groups is up to limit.

Example::
    
    curl -X POST https://api.dnspod.com/Domaingroup.List -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&group_name=dnspod'

Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 21:41:00"
            },
            "groups": {
                "id": "1985"
            }
        }

Attention：
    * This API only works for VIP accounts while free accounts will get an error.

Update a Domain Group
---------------------
URL：
    https://api.dnspod.com/Domaingroup.Modify
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **group_id** 
    * **group_name** 
Response Code：
    * Common Response Code
    * 6 Invalid group id.
    * 7 Invalid group name.
    * 8 The group name already exists.
    * 9 The number of groups is up to limit.

Example::
    
    curl -X POST https://api.dnspod.com/Domaingroup.Modify -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&group_id=1985&group_name=dnspodgroup'

Response：

    * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-19 10:25:32"
            }
        }
    
Remove a Domain Group
---------------------
URL：
    * https://api.dnspod.com/Domaingroup.Remove
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **group_id**
Response Code：
    * Common Response Code
    * 6 Invalid group id.

Example::
    
    curl -X POST https://api.dnspod.com/Domaingroup.Remove -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&group_id=1985'

Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-19 10:45:45"
            }
        }
    
Change a Domain's Group
-----------------------
URL：
    * https://api.dnspod.com/Domain.Changegroup
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
    * **group_id** 
Response Code：
    * Common Response Code
    * 6 Invalid domain id.
    * 7 Invalid group id.

Example::
    
    curl -X POST https://api.dnspod.com/Domain.Changegroup -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&group_id=1985'
    
Response：

   * JSON::
    
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-23 17:33:01"
            }
        } 

Directions：
    * All the domains shared by others are always put into the group named "Shared With Me" because their group is unchangeable.
    * Only the owner of the domain has the permission to change the domain's group.

Mark a Domain
-------------
URL：
    * https://api.dnspod.com/Domain.Ismark
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
    * **is_mark** {yes|no} Whether to mark this domain.
Response Code：
    * Common Response Code
    * 6 Invalid domain id.

Example::
    
    curl -X POST https://api.dnspod.com/Domain.Ismark -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&is_mark=yes'

Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-23 17:42:02"
            }
        }

Remark a Domain
---------------
URL：
    * https://api.dnspod.com/Domain.Remark
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
    * **remark** The remark information,or empty for deleting.
Response Code：
    * Common Response Code
    * 6 Invalid domain id.

Example::
    
    curl -X POST https://api.dnspod.com/Domain.Remark -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_id=2059079&remark=这个域名需要备注一下'
    
Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-23 17:50:37"
            }
        }


Get the Email Address Needed to Get Domain Back
-----------------------------------------------
URL：
    * https://api.dnspod.com/Domain.Acquire
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain** The domain you want to get back.
Response Code：
    * Common Response Code
    * 6 Invalid domain
    * 7 No Chinese character allowed in the domain.
    * 8 Invalid domain.
    * 9 Domains that end with ".tk" are not supported.No offence.
    * 10 Domain not exists.
    * 11 Domain got prohibited.
    * 12 Domain got locked.
    * 13 You can't get a domain back from a company account to a persional account.
    * 14 You can't get a domain back from a persional account to a company account.
    * 15 Fail to get email address.Maybe there's something wrong with the network or the domain doesn't support.

Example::
    
    curl -X POST https://api.dnspod.com/Domain.Acquire -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain=api4.com'
    
Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-23 18:00:05"
            },
            "emails": [
                "support@namecheap.com",
                "e31d739cb2824a5f80d7b90848a195d8.protect@whoisguard.com"
            ]
        }

Send Verify Code for Getting Domain Back
----------------------------------------
URL：
    *  https://api.dnspod.com/Domain.Acquiresend
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain** The domain you want to get back.
    * **email** One email address in the get-domain-back email list.
Response Code：
    * Common Response Code
    * 6 Invalid domain.
    * 7 No Chinese characters supported in the domain.
    * 8 Invalid domain.
    * 9 Domains end with ".tk" are not supported.No offence.
    * 10 Domain not exists.
    * 11 Domain got prohibited.
    * 12 Domain got locked.
    * 13 You can't get a domain back from a company account to a persional account.
    * 14 You can't get a domain back from a persional account to a company account.
    * 15 Fail to get email address.Maybe there's something wrong with the network or the domain doesn't support.
    * 16 Invalid email address.

Example::
    
    curl -X POST https://api.dnspod.com/Domain.Acquiresend -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain=api4.com&email=support@namecheap.com'
    
Response：
    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-23 18:07:44"
            }
        }

Verify the Verify Code
----------------------
URL：
    * https://api.dnspod.com/Domain.Acquirevalidate
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain** The domain you want to get back.
    * **code**  The code that you get from your email.
Response Code：
    * Common Response Code
    * 6 Invalid domain.
    * 7 No Chinnese characters allowed.
    * 8 Invalid domain.
    * 9 Domains end with ".tk" are not supported.No offence.
    * 10 Domain not exists.
    * 11 Domain got prohibited.
    * 12 Domain got locked.
    * 13 You can't get a domain back from a company account to a persional account.
    * 14 You can't get a domain back from a persional account to a company account.
    * 15 Wrong code.
    * 16 Invalid email address.

Example::
    
    curl -X POST https://api.dnspod.com/Domain.Acquirevalidate -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain=api4.com&code=111000'
    
Response：

    * JSON::
            
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-23 18:12:44"
            }
        }

Get All the Record Types for a Domain Grade
-------------------------------------------
URL：
    *  https://api.dnspod.com/Record.Type
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_grade** The domain grade. only 'DP_Free' for now. 
Response Code：
    * Common Response Code
    * 6 Invalid domain grade.

Example::
    
    curl -X POST https://api.dnspod.com/Record.Type -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_grade=DP_Free'

Response：

    * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-06 10:30:26"
            },
            "types": [
                "A",
                "CNAME",
                "MX",
                "TXT",
                "NS",
                "AAAA",
                "SRV",
                "URL",
                "Framed URL"
            ],
        }


Get All the Lines Allowed for a Domain Grade
--------------------------------------------
URL：
    *  https://api.dnspod.com/Record.Line
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_grade** The domain grade. only 'DP_Free' for now. 
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
Response Code：
    * Common Response Code
    * 6 Invalid domain grade.

Example::
    
    curl -X POST https://api.dnspod.com/Record.Line -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&domain_grade=DP_Free&domain=dnspod.com'

Response：

    * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-12 15:39:05"
            },
            "lines": {
                "default": {
                    "name": "Default",
                    "sub_area": {
                        "default": "Default"
                    }
                },
                "africa": {
                    "name": "Africa",
                    "sub_area": {
                        "DZ": "Algeria",
                        "AO": "Angola",
                        "BJ": "Benin",
                        "BW": "Botswana",
                        "BF": "Burkina Faso",
                        "BI": "Burundi",
                        "CM": "Cameroon",
                        "CV": "Cape Verde",
                        "CF": "Central Africa",
                        "TD": "Chad",
                        "KM": "Comoros",
                        "CG": "Congo - Brazzaville",
                        "CD": "Congo, The Democratic Republic Of The",
                        "CI": "Cote D'Ivoire",
                        "DJ": "Djibouti",
                        "EG": "Egypt",
                        "GQ": "Equatorial Guinea",
                        "ER": "Eritrea",
                        "ET": "Ethiopia",
                        "GA": "Gabon",
                        "GM": "Gambia",
                        "GH": "Ghana",
                        "GN": "Guinea",
                        "GW": "Guinea-Bissau",
                        "KE": "Kenya",
                        "LS": "Lesotho",
                        "LR": "Liberia",
                        "LY": "Libya",
                        "MG": "Madagascar",
                        "MW": "Malawi",
                        "ML": "Mali",
                        "MR": "Mauritania",
                        "MU": "Mauritius",
                        "YT": "Mayotte",
                        "MA": "Morocco",
                        "MZ": "Mozambique",
                        "NA": "Namibia",
                        "NE": "Niger",
                        "NG": "Nigeria",
                        "RE": "Reunion",
                        "RW": "Rwanda",
                        "SH": "Saint Helena",
                        "ST": "Sao Tome And Principe",
                        "SN": "Senegal",
                        "SC": "Seychelles",
                        "SL": "Sierra Leone",
                        "SO": "Somalia",
                        "ZA": "South Africa",
                        "SD": "Sudan",
                        "SZ": "Swaziland",
                        "TZ": "Tanzania",
                        "TG": "Togo",
                        "TN": "Tunisia",
                        "UG": "Uganda",
                        "EH": "Western Sahara",
                        "ZM": "Zambia",
                        "ZW": "Zimbabwe"
                    }
                },
                "antartica": {
                    "name": "Antartica",
                    "sub_area": {
                        "AQ": "Antarctica",
                        "BV": "Bouvet Island",
                        "TF": "French Southern Territories",
                        "HM": "Heard And Mc Donald Islands",
                        "GS": "South Georgia And The South Sandwich Islands"
                    }
                },
                "asia": {
                    "name": "Asia",
                    "sub_area": {
                        "AF": "Afghanistan",
                        "AM": "Armenia",
                        "AZ": "Azerbaijan",
                        "BH": "Bahrain",
                        "BD": "Bangladesh",
                        "BT": "Bhutan",
                        "IO": "British Indian Ocean Territory",
                        "BN": "Brunei Darussalam",
                        "KH": "Cambodia",
                        "CN": "China",
                        "CX": "Christmas Island",
                        "CC": "Cocos (Keeling) Islands",
                        "CY": "Cyprus",
                        "GE": "Georgia",
                        "HK": "Hong Kong",
                        "IN": "India",
                        "ID": "Indonesia",
                        "IR": "Iran, Islamic Republic Of",
                        "IQ": "Iraq",
                        "IL": "Israel",
                        "JP": "Japan",
                        "JO": "Jordan",
                        "KZ": "Kazakhstan",
                        "KP": "North Korea",
                        "KR": "Korea",
                        "KW": "Kuwait",
                        "KG": "Kyrgyzstan",
                        "LA": "Lao",
                        "LB": "Lebanon",
                        "MO": "Macao",
                        "MY": "Malaysia",
                        "MV": "Maldives",
                        "MN": "Mongolia",
                        "MM": "Myanmar",
                        "NP": "Nepal",
                        "OM": "Oman",
                        "PK": "Pakistan",
                        "PS": "Palestinian Territory",
                        "PH": "Philippines",
                        "QA": "Qatar",
                        "SA": "Saudi Arabia",
                        "SG": "Singapore",
                        "LK": "Sri Lanka",
                        "SY": "Syria",
                        "TW": "Taiwan",
                        "TJ": "Tajikistan",
                        "TH": "Thailand",
                        "TL": "Timor-Leste",
                        "TR": "Turkey",
                        "TM": "Turkmenistan",
                        "AE": "United Arab Emirates",
                        "UZ": "Uzbekistan",
                        "VN": "Viet Nam",
                        "YE": "Yemen"
                    }
                },
                "europe": {
                    "name": "Europe",
                    "sub_area": {
                        "AX": "Aland Islands",
                        "AL": "Albania",
                        "AD": "Andorra",
                        "AT": "Austria",
                        "BY": "Belarus",
                        "BE": "Belgium",
                        "BA": "Bosnia And Herzegovina",
                        "BG": "Bulgaria",
                        "HR": "Croatia",
                        "CZ": "Czech",
                        "DK": "Denmark",
                        "EE": "Estonia",
                        "EU": "European Union",
                        "FO": "Faroe Islands",
                        "FI": "Finland",
                        "FR": "France",
                        "DE": "Germany",
                        "GI": "Gibraltar",
                        "GR": "Greece",
                        "GG": "Guernsey",
                        "VA": "Holy See",
                        "HU": "Hungary",
                        "IS": "Iceland",
                        "IE": "Ireland",
                        "IM": "Isle Of Man",
                        "IT": "Italy",
                        "JE": "Jersey",
                        "CS": "Kosovo",
                        "LV": "Latvia",
                        "LI": "Liechtenstein",
                        "LT": "Lithuania",
                        "LU": "Luxembourg",
                        "MK": "Macedonia",
                        "MT": "Malta",
                        "MD": "Moldova",
                        "MC": "Monaco",
                        "ME": "Montenegro",
                        "NL": "Netherlands",
                        "NO": "Norway",
                        "PL": "Poland",
                        "PT": "Portugal",
                        "RO": "Romania",
                        "RU": "Russia",
                        "SM": "San Marino",
                        "RS": "Serbia",
                        "SK": "Slovakia",
                        "SI": "Slovenia",
                        "ES": "Spain",
                        "SJ": "Svalbard & Jan Mayen Islands",
                        "SE": "Sweden",
                        "CH": "Switzerland",
                        "UA": "Ukraine",
                        "GB": "United Kingdom"
                    }
                },
                "north_america": {
                    "name": "North America",
                    "sub_area": {
                        "AI": "Anguilla",
                        "AG": "Antigua And Barbuda",
                        "AW": "Aruba",
                        "BS": "Bahamas",
                        "BB": "Barbados",
                        "BZ": "Belize",
                        "BM": "Bermuda",
                        "BQ": "Bonaire, Saint Eustatius And Saba",
                        "CA": "Canada",
                        "KY": "Cayman Islands",
                        "CR": "Costa Rica",
                        "CU": "Cuba",
                        "CW": "Curacao",
                        "DM": "Dominica",
                        "DO": "Dominican Republic",
                        "SV": "El Salvador",
                        "GL": "Greenland",
                        "GD": "Grenada",
                        "GP": "Guadeloupe",
                        "GT": "Guatemala",
                        "HT": "Haiti",
                        "HN": "Honduras",
                        "JM": "Jamaica",
                        "MQ": "Martinique",
                        "MX": "Mexico",
                        "MS": "Montserrat",
                        "AN": "Netherlands Antilles",
                        "NI": "Nicaragua",
                        "PA": "Panama",
                        "PR": "Puerto Rico",
                        "BL": "Saint Barthelemy",
                        "KN": "Saint Kitts And Nevis",
                        "LC": "Saint Lucia",
                        "MF": "Saint Martin",
                        "PM": "Saint Pierre And Miquelon",
                        "VC": "Saint Vincent And The Grenadines",
                        "SX": "Sint Maarten",
                        "TT": "Trinidad And Tobago",
                        "TC": "Turks And Caicos Islands",
                        "US": "United States",
                        "UM": "United States Minor Outlying Islands",
                        "VG": "Virgin Islands, British",
                        "VI": "Virgin Islands, U.S."
                    }
                },
                "oceania": {
                    "name": "Oceania",
                    "sub_area": {
                        "AS": "American Samoa",
                        "AP": "Asia Pacific",
                        "AU": "Australia",
                        "CK": "Cook Islands",
                        "FJ": "Fiji",
                        "PF": "French Polynesia",
                        "GU": "Guam",
                        "KI": "Kiribati",
                        "MH": "Marshall Islands",
                        "FM": "Micronesia, Federated States Of",
                        "NR": "Nauru",
                        "NC": "New Caledonia",
                        "NZ": "New Zealand",
                        "NU": "Niue",
                        "NF": "Norfolk Island",
                        "MP": "Northern Mariana Islands",
                        "PW": "Palau",
                        "PG": "Papua New Guinea",
                        "PN": "Pitcairn",
                        "WS": "Samoa",
                        "SB": "Solomon Islands",
                        "TK": "Tokelau",
                        "TO": "Tonga",
                        "TV": "Tuvalu",
                        "VU": "Vanuatu",
                        "WF": "Wallis And Futuna Islands"
                    }
                },
                "south_america": {
                    "name": "South American",
                    "sub_area": {
                        "AR": "Argentina",
                        "BO": "Bolivia",
                        "BR": "Brazil",
                        "CL": "Chile",
                        "CO": "Colombia",
                        "EC": "Ecuador",
                        "FK": "Falkland Islands (Malvinas)",
                        "GF": "French Guiana",
                        "GY": "Guyana",
                        "PY": "Paraguay",
                        "PE": "Peru",
                        "SR": "Suriname",
                        "UY": "Uruguay",
                        "VE": "Venezuela"
                    }
                },
                "search_engine": {
                    "name": "Search Engine",
                    "sub_area": {
                        "search_engine": "Search Engine"
                    }
                }
            }
        }
