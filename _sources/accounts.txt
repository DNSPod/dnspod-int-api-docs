Accounts
========


Get Account Information
-----------------------
URL:
    * https://api.dnspod.com/User.Detail
HTTP Request Type:
    * POST
Request Parameters:
    * Global Parameters
Response Code:
    * Common Response Codes

Example::
    
    curl -X POST https://api.dnspod.com/User.Detail -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json'

Response Example:

    * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-04 20:58:37"
            },
            "info": {
                "user": {
                    "real_name": "",
                    "user_type": "personal",
                    "telephone": null,
                    "im": null,
                    "nick": "Yizero Mr",
                    "id": "730060",
                    "email": "yizero@qq.com",
                    "status": "enabled",
                    "email_verified": "no",
                    "telephone_verified": "no",
                    "weixin_binded": "no",
                    "agent_pending": false,
                    "balance": 0,
                    "smsbalance": 0
                }
            }
        }     


Update Information
------------------
URL:
    * https://api.dnspod.com/User.Modify
HTTP Request Type:
    * POST
Request Parameters:
    * Global Parameters
    * **real_name** Your real name for personal accounts,and company name for company accounts.
    * **nick** Your nickname that make it easier to contact to the users.
    * **telephone** The users' phone number.
    * **im** Your Instant Messaging account.
Response Code:
    * Common Response Codes
    * 8 Invalid phone number.
    * 9 Invalid im account.

Example::
    
    curl -X POST https://api.dnspod.com/User.Modify -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&im=10000000'

Response Example:

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
URL:
    * https://api.dnspod.com/Userpasswd.Modify
HTTP Request Type:
    * POST
Request Parameters:
    * Global Parameters
    * **old_password** The old password.
    * **new_password** The new password.
Response Code:
    * Common Response Codes
    * 8 Wrong old password.
    * 9 Invalid new password.

Example::
    
    curl -X POST https://api.dnspod.com/Userpassword.Modify -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&old_password=old_password&new_password=new_password'

Response Example:

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
URL:
    * https://api.dnspod.com/Useremail.Modify
HTTP Request Type:
    * POST
Request Parameters:
    * Global Parameters
    * **old_email** Old email address.
    * **new_email** New email address.
    * **password** Your current password for verifying.
Response Code:
    * Common Response Codes
    * 8 Old email address is not correct.
    * 9 New email address is invalid.
    * 10 Wrong password.

Example:: 

    curl -X POST https://api.dnspod.com/Useremail.Modify -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json&old_email=api1@dnspod.com&new_email=api@dnspod.com&password=password'   

Response Example:

    * JSON::
        
        {
            "status": {
                "code":"1",
                "message":"Action completed successful",
                "created_at":"2012-08-24 14:49:41"
            }
        }

        

Get The Account's Operate Log
-----------------------------
URL:
    * https://api.dnspod.com/User.Log
HTTP Request Type:
    * POST
Request Parameters:
    * Global Parameters
Response Code:
    * Common Response Codes

Example::

    curl -X POST https://api.dnspod.com/User.Log -d 'user_token=730060,e1a8a$f14dc5dcbafd83680b3d2a553c4d553d&format=json'

Response Example:

    * JSON::

        {
            "status": {
                "code": "1",
                "message": "Action completed successful",
                "created_at": "2014-06-04 21:09:50"
            },
            "log": [
                "There is no user logs at the moment."
            ]
        }
