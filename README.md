
## Sample Codes 20170407:

### 1. Put all the file into common folder, not the frontend folder
common/utils

common/models

### 2. Change the common/models/User.php

```
use common\models\UserIdentity;  
use common\utils\WpCheckPassword;  

class User extends UserIdentity

```
......

```
    public function validatePassword($password)
    {
		
		
		$wp_check = new WpCheckPassword();
		return $wp_check->wp_check_password($password, $this->password_hash);
        //return Yii::$app->getSecurity()->validatePassword($password, $this->password_hash);
    }
```

### 3. Change the configure parameters in WpCookieCheck.php according to the wp-config.php

### 4. import all the wordpress's table 'user' to yii2's table 'user'






WordPress 2 Yii2 Password Migration
===================================

These are helper classes, taken from WordPress Source Code.

If you are migrating a website from WordPress to Yii2, and want to be able to handle user 
authentication basedn on WordPress `user` table pwsswords, you will need WordPress functions
to validate password.



HOW DOES IT WORK
----------------
This script will check, to see if user has Yii2 password hash or WordPress one.
Check is based on password_hash length. If password_hash is not 60 characters, then
system tries to validate password via WordPress functions.
And if succeed, it will then convert the raw password into Yii2 password hash, 
generate and auth_key and save into database. So that after first log-in, users will have Yii2 password hash.



WORDPRESS COOKIE LOG-IN
----------------------
This script is able to handle log-ins, via WordPress cookies.
For this you need to configure parameters in WpCookieCheck.php,
crate instance of WPCookieCheck class, and call wp_validate_auth_cookie() function.


DIRECTORY STRUCTURE
-------------------

This is based on yii2 advanced application template
root
|	/_protected
|		/backend
|		/common
|			/utils
|				- WpCheckPassword.php
|				- WpCookiesCheck.php
|				- WpPasswordHash.php
|		/frontend
|			/models
|				- UserIdentity.php
