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
    * **domain** The domain to add.No prefix.Example:dnspod.com
    * **group_id** The domain group ID.Optional parameter.
    * **is_mark** {yes|no} Whether to mark it or not.Optional parameter.
Response Code：
    * Common Response Code
    * 6 Invalid domain.
    * 7 Domain already exists.
    * 11 Domain already exists as an alias of another domain.
    * 12 Domain already exists on which you have no permit to operate.
    * 41 The website falls short of the term of service of DNSPod.

Example::

    curl -X POST https://api.dnspod.com/Domain.Create -d 'login_email=api@dnspod.com&login_password=password&domain=api2.com&format=json'

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
    * If there are more than 3000 domains in your account,only the first 3000 domains will responsed for split page.You may need to set the parameter "offset" and "length" to get all your domains with multi requests.
Response Code：
    * Common Response Code
    * 6 Invalid offset.
    * 7 Invalid length.
    * 9 Empty result.

Example::
    
    curl -X POST https://api.dnspod.com/Domain.List -d 'login_email=api@dnspod.com&login_password=password&format=json'

Response：

   * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-10 11:51:31"
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
                "share_out_total": 0
            },
            "domains": [
                {
                    "id": 1992403,
                    "name": "api2.com",
                    "grade": "D_Free",
                    "grade_title": "免费套餐",
                    "status": "enable",
                    "ext_status": "dnserror",
                    "records": "2",
                    "group_id": "1",
                    "is_mark": "no",
                    "remark": "",
                    "is_vip": "no",
                    "searchengine_push": "yes",
                    "beian": "no",
                    "created_on": "2012-08-29 22:12:35",
                    "updated_on": "2012-08-29 22:12:35",
                    "ttl": "600",
                    "owner": "api@dnspod.com"
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

    curl -X POST https://api.dnspod.com/Domain.Remove -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=1992403'
    
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

    curl -X POST https://api.dnspod.com/Domain.Status -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2058967&status=disable'

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

    curl -X POST https://api.dnspod.com/Domain.Info  -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079'

Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-12 12:10:16"
            },
            "domain": {
                "id": "2059079",
                "name": "api4.com",
                "punycode": "api4.com",
                "grade": "D_Free",
                "grade_title": "免费套餐",
                "status": "pause",
                "ext_status": "dnserror",
                "records": "9",
                "group_id": "1",
                "is_mark": "no",
                "remark": "",
                "is_vip": "no",
                "searchengine_push": "yes",
                "beian": "no",
                "user_id": "625033",
                "created_on": "2012-09-12 12:05:46",
                "updated_on": "2012-09-12 12:06:12",
                "ttl": "600",
                "owner": "api@dnspod.com"
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
    
    curl -X POST https://api.dnspod.com/Domain.Log  -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079'

Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 17:24:23"
            },
            "log": [
                "2012-09-12 12:07:05: (111.111.111.111) 启用解析 NS 记录 默认 线路 @ 值 f1g1ns1.dnspod.net.",
                "2012-09-12 12:07:04: (111.111.111.111) 启用解析 NS 记录 默认 线路 @ 值 f1g1ns2.dnspod.net. ",
                "2012-09-12 12:07:02: (111.111.111.111) 暂停解析 NS 记录 默认 线路 @ 值 f1g1ns2.dnspod.net. ",
                "2012-09-12 12:06:57: (111.111.111.111) 暂停解析 NS 记录 默认 线路 @ 值 f1g1ns1.dnspod.net. ",
                "2012-09-12 12:06:33(API): (111.111.111.111) 暂停 域名解析",
                "2012-09-12 12:06:12: (111.111.111.111) 添加 CNAME 记录 默认 线路 pop 值 mail.api4.com. ",
                "2012-09-12 12:06:12: (111.111.111.111) 添加 A 记录 默认 线路 shop 值 64.144.7.55 ",
                "2012-09-12 12:06:12: (111.111.111.111) 添加 CNAME 记录 默认 线路 smtp 值 mail.api4.com. ",
                "2012-09-12 12:06:12: (111.111.111.111) 添加 CNAME 记录 默认 线路 webmail 值 webmail.secureserver.net. ",
                "2012-09-12 12:06:11: (111.111.111.111) 添加 A 记录 默认 线路 www 值 64.144.7.51 ",
                "2012-09-12 12:06:11: (111.111.111.111) 添加 A 记录 默认 线路 ftp 值 64.144.7.51 ",
                "2012-09-12 12:06:11: (111.111.111.111) 添加 CNAME 记录 默认 线路 e 值 email.secureserver.net. ",
                "2012-09-12 12:05:46: (111.111.111.111) 添加新域名 api4.com api@dnspod.com(625033)"
            ]
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

    curl -X POST https://api.dnspod.com/Domain.Searchenginepush -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&status=yes'
    
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

    curl -X POST https://api.dnspod.com/Domainshare.Create -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&email=otheruser@dnspod.com&mode=rw'
    
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
    
    curl -X POST https://api.dnspod.com/Domainshare.List -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079'

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
        
    curl -X POST https://api.dnspod.com/Domainshare.Modify -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&email=yizerowu@dnspod.com&mode=r'
    
2. Change a domain's share mode from "rw" to "r"::
            
    curl -X POST https://api.dnspod.com/Domainshare.Modify -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&email=yizerowu@dnspod.com&mode=r&old_sub_domain=www&new_sub_domain=www'
    
3. Change a domain's share type from the whole domain to subsidiary domain.::

    curl -X POST https://api.dnspod.com/Domainshare.Modify -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&email=yizerowu@dnspod.com&mode=rw&new_sub_domain=www'
    
4. Change a domain's share type from subsidiary domain to the whole domain.::

    curl -X POST https://api.dnspod.com/Domainshare.Modify -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&email=yizerowu@dnspod.com&mode=rw&old_sub_domain=www'
    
5. Change the subsidiary domain from "www" to "bbs"::

    curl -X POST https://api.dnspod.com/Domainshare.Modify -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&email=yizerowu@dnspod.com&mode=rw&old_sub_domain=www&new_sub_domain=bbs'
    
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
    
    curl -X POST https://api.dnspod.com/Domainshare.Remove -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&email=yizerowu@dnspod.com'

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
    
    curl -X POST https://api.dnspod.com/Domainshare.Transfer -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&email=yizerowu@dnspod.com'
    
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
    
    curl -X POST https://api.dnspod.com/Domain.Lock -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&days=3'

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
    
    curl -X POST https://api.dnspod.com/Domain.Lockstatus -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079'
    
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
    
    curl -X POST https://api.dnspod.com/Domain.Unlock -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&lock_code=fdd638'

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
    
    curl -X POST https://api.dnspod.com/Domainalias.List -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079'

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
    
    curl -X POST https://api.dnspod.com/Domainalias.Create -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&domain=dnspodapi.com'

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
    
    curl -X POST https://api.dnspod.com/Domainalias.Remove -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&alias_id=18737'

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
    
    curl -X POST https://api.dnspod.com/Domaingroup.List -d 'login_email=api@dnspod.com&login_password=password&format=json'
    
Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-18 21:33:33"
            },
            "groups": [
                {
                    "group_id": 1,
                    "group_name": "默认分组",
                    "group_type": "system",
                    "size": 1
                },
                {
                    "group_id": 2,
                    "group_name": "经常修改",
                    "group_type": "system",
                    "size": null
                },
                {
                    "group_id": 3,
                    "group_name": "很少修改",
                    "group_type": "system",
                    "size": null
                },
                {
                    "group_id": 4,
                    "group_name": "即将到期",
                    "group_type": "system",
                    "size": null
                },
                {
                    "group_id": 5,
                    "group_name": "私人域名",
                    "group_type": "system",
                    "size": null
                },
                {
                    "group_id": 6,
                    "group_name": "公司域名",
                    "group_type": "system",
                    "size": null
                },
                {
                    "group_id": 7,
                    "group_name": "客户域名",
                    "group_type": "system",
                    "size": null
                },
                {
                    "group_id": 8,
                    "group_name": "与我共享",
                    "group_type": "system",
                    "size": null
                }
            ]
        }

Attention：
    * This API only works for VIP accounts while free users will get an error.
    
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
    
    curl -X POST https://api.dnspod.com/Domaingroup.List -d 'login_email=api@dnspod.com&login_password=password&format=json&group_name=dnspod'

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
    
    curl -X POST https://api.dnspod.com/Domaingroup.Modify -d 'login_email=api@dnspod.com&login_password=password&format=json&group_id=1985&group_name=dnspodgroup'

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
    
    curl -X POST https://api.dnspod.com/Domaingroup.Remove -d 'login_email=api@dnspod.com&login_password=password&format=json&group_id=1985'

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
    
    curl -X POST https://api.dnspod.com/Domain.Changegroup -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&group_id=1985'
    
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
    
    curl -X POST https://api.dnspod.com/Domain.Ismark -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&is_mark=yes'

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
    
    curl -X POST https://api.dnspod.com/Domain.Remark -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079&remark=这个域名需要备注一下'
    
Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-23 17:50:37"
            }
        }

Get The Domain's Purview
------------------------
URL：
    * https://api.dnspod.com/Domain.Purview
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
Response Code：
    * Common Response Code
    * 6 Invalid domain id

Example::
    
    curl -X POST https://api.dnspod.com/Domain.Purview -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_id=2059079'
    
Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-23 17:51:25"
            },
            "purview": [
                {
                    "name": "URL转发条数",
                    "value": 10
                },
                {
                    "name": "NS记录条数",
                    "value": 99999
                },
                {
                    "name": "AAAA记录条数",
                    "value": 99999
                },
                {
                    "name": "SRV记录条数",
                    "value": 10
                },
                {
                    "name": "域名别名绑定个数",
                    "value": 3
                },
                {
                    "name": "域名锁定天数",
                    "value": 30
                },
                {
                    "name": "域名共享个数",
                    "value": 2
                },
                {
                    "name": "子域名级数",
                    "value": 3
                },
                {
                    "name": "泛解析级数",
                    "value": 2
                },
                {
                    "name": "负载均衡数量",
                    "value": 4
                },
                {
                    "name": "记录TTL最低",
                    "value": 120
                },
                {
                    "name": "混合泛解析支持",
                    "value": "no"
                },
                {
                    "name": "增强线路类型",
                    "value": "yes"
                },
                {
                    "name": "分省线路类型",
                    "value": "no"
                },
                {
                    "name": "分大洲线路类型",
                    "value": "no"
                }
            ]
        }

Directions:
    * Store it when you get it instead of get this with API everytime you need it.This is something rarely change.

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
    
    curl -X POST https://api.dnspod.com/Domain.Acquire -d 'login_email=api@dnspod.com&login_password=password&format=json&domain=api4.com'
    
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
    
    curl -X POST https://api.dnspod.com/Domain.Acquiresend -d 'login_email=api@dnspod.com&login_password=password&format=json&domain=api4.com&email=support@namecheap.com'
    
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
    
    curl -X POST https://api.dnspod.com/Domain.Acquirevalidate -d 'login_email=api@dnspod.com&login_password=password&format=json&domain=api4.com&code=111000'
    
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
    * **domain_grade** The domain grade.It's legal values :
        * Old packages:"D_Free", "D_Plus", "D_Extra", "D_Expert", "D_Ultra" stand for "Free edition","Persion plus","Company Extra","Company expert","Company ultra"
        * New packages:"DP_Free", "DP_Plus", "DP_Extra", "DP_Expert", "DP_Ultra" stand for the same thing above.
Response Code：
    * Common Response Code
    * 6 Invalid domain grade.

Example::
    
    curl -X POST https://api.dnspod.com/Record.Type -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_grade=D_Free'

Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-23 18:23:40"
            },
            "types": [
                "A",
                "CNAME",
                "MX",
                "TXT",
                "NS",
                "AAAA",
                "SRV",
                "URL"
            ]
        }    

Get All the Lines Allowed for a Domain Grade
--------------------------------------------
URL：
    *  https://api.dnspod.com/Record.Line
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **domain_grade** The domain grade.It's legal values :
        * Old packages:"D_Free", "D_Plus", "D_Extra", "D_Expert", "D_Ultra" stand for "Free edition","Persion plus","Company Extra","Company expert","Company ultra"
        * New packages:"DP_Free", "DP_Plus", "DP_Extra", "DP_Expert", "DP_Ultra" stand for the same thing above.
    * **domain_id** OR **domain** Stand for the id and the name of the domain.You only need to and must set one of them.
Response Code：
    * Common Response Code
    * 6 Invalid domain grade.

Example::
    
    curl -X POST https://api.dnspod.com/Record.Line -d 'login_email=api@dnspod.com&login_password=password&format=json&domain_grade=D_Free&domain_id=2059079'

Response：

    * JSON::
        
            {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-23 18:29:58"
            },
            "lines": [
                "默认",
                "电信",
                "联通",
                "教育网",
                "移动",
                "铁通",
                "国内",
                "国外",
                "搜索引擎",
                "百度",
                "Google",
                "有道",
                "必应",
                "搜搜",
                "搜狗",
                "360搜索"
            ]
            }

