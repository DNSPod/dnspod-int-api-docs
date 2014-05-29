Accounts
========


Get Account Information
-----------------------
URL：
    * https://api.dnspod.com/User.Detail
Method：
    * POST
Request Parameters：
    * Global Parameters
Response Code：
    * Common Response

Example::
    
    curl -X POST https://api.dnspod.com/User.Detail -d 'login_email=api@dnspod.com&login_password=password&format=json'

Response Example：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-10 11:22:26"
            },
            "info": {
                "user": {
                    "id": "625033",
                    "email": "api@dnspod.com",
                    "status": "enabled",
                    "email_verified": "no",
                    "telephone_verified": "yes",
                    "agent_pending": false,
                    "real_name": "",
                    "user_type": "personal",
                    "telephone": "15012345678",
                    "im": "10000000",
                    "nick": "DNSPod 先生",
                    "balance": "0",
                    "smsbalance": "4"
                }
            }
        }

Update Information
------------------
URL：
    * https://api.dnspod.com/User.Modify
Method：
    * POST
Request Parameters：
    * Global parameters
    * **real_name** Your real name for personal accounts,and company name for company accounts.
    * **nick** Your nickname that make it easier to contact to the users.
    * **telephone** The users' phone number.
    * **im** Your Instant Messaging account.
Response Code：
    * Common response
    * 8 Invalid phone number.
    * 9 Invalid im account.

Example::
    
    curl -X POST https://api.dnspod.com/User.Modify -d 'login_email=api@dnspod.com&login_password=password&format=json&im=10000000'

Response：

    * JSON::

        {
            "status": {
                "code":"1",
                "message":"Action completed successful",
                "created_at":"2012-08-24 13:34:56"
            }
        }

Change Password
---------------
URL：
    * https://api.dnspod.com/Userpasswd.Modify
Method：
    * POST
Request Parameters：
    * Global Parameters
    * **old_password** The old password.
    * **new_password** The new password.
Response Code：
    * Common Response Code
    * 8 Wrong old password.
    * 9 Invalid new password.

Example::
    
    curl -X POST https://api.dnspod.com/Userpassword.Modify -d 'login_email=api@dnspod.com&login_password=password&format=json&old_password=old_password&new_password=new_password'

Response：

    * JSON::

        {
            "status": {
                "code":"1",
                "message":"Action completed successful",
                "created_at":"2012-08-24 13:45:27"
            }
        }

Update Email Address
--------------------
URL：
    * https://api.dnspod.com/Useremail.Modify
HTTP Resquest Type：
    * POST
Request Parameters：
    * Global Parameters
    * **old_email** Old email address.
    * **new_email** New email address.
    * **password** Your current password for verifying.
Response Code：
    * Common Response Code.
    * 8 Old email address is not correct.
    * 9 New email address is invalid.
    * 10 Wrong password.

Example:: 

    curl -X POST https://api.dnspod.com/Useremail.Modify -d 'login_email=api@dnspod.com&login_password=password&format=json&old_email=api1@dnspod.com&new_email=api@dnspod.com&password=password'   

Response：

    * JSON::
        
        {
            "status": {
                "code":"1",
                "message":"Action completed successful",
                "created_at":"2012-08-24 14:49:41"
            }
        }

        
Get Telephone Verify Code
-------------------------
URL：
    * https://api.dnspod.com/Telephoneverify.Code
Method：
    * POST
Request Parameters :
    * Global Parameters.
    * **telephone** The telephone number.
Response Code：
    * Common Response
    * 4 You already did this.
    * 5 Invalid telephone number.

Example::
    
    curl -X POST https://api.dnspod.com/Telephoneverify.Code -d 'login_email=api@dnspod.com&login_password=password&format=json&telephone=18600000000'

Response：

    * JSON::
        
        {
            "status": {
                "code":"4",
                "message":"Telephone is verified",
                "created_at":"2012-08-24 15:57:21"
            }
        }

        {
            "status": {
                "code":"1",
                "message":"Action completed successful",
                "created_at":"2012-11-23 16:01:52"
            }, 
            "user": {
                "verify_code":"676479",
                "verify_desc":"\u8bf7\u4f7f\u7528 18600000000 \u7f16\u8f91\u77ed\u4fe1\uff0c\u5c06 676479 \u53d1\u9001\u81f3\u53f7\u7801  159 6183 3568\u3002"
            }
        }

Get The Account's Operate Log
-----------------------------
URL：
    * https://api.dnspod.com/User.Log
Method：
    * POST
Request Parameters：
    * Global Parameters
Response Code：
    * Common response code.

Example::

    curl -X POST https://api.dnspod.com/User.Log -d 'login_email=api@dnspod.com&login_password=password&format=json'

Response：

    * JSON::
        
        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2012-09-10 11:29:36"
            },
            "log": 
            [
                "2012-09-04 13:56:24: 111.111.111.111 登陆 成功",
                "2012-08-30 17:01:47: 111.111.111.111 登陆 成功",
                "2012-08-29 22:12:35(API): (111.111.111.111) 添加域名 api2.com",
                "2012-08-29 21:59:55: (111.111.111.111) 添加域名 api1.com",
                "2012-08-29 21:59:45: (111.111.111.111) 添加域名 apiapi.com",
                "2012-08-29 21:59:30: 111.111.111.111 登陆 成功",
                "2012-08-24 15:49:53: 111.111.111.111 登陆 成功",
            ]
        }

