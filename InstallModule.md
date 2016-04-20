# Installation #
  * Unpack files in your project/protected/modules (replace UserIdentity.php)
  * Insert to config/main.php
```
return array(
#...
	'modules'=>array(
		'user',
	),
#...
	// application components
	'components'=>array(
#...
		'user'=>array(
			// enable cookie-based authentication
			'allowAutoLogin'=>true,
			'loginUrl' => array('/user/login'),
		),
#...
	),
#...
);
```
  * Create tables (dump files schema.mysql.sql and schema.sqlite.sql)
  * Insert items in to zii.widgets.CMenu array (protected/views/layouts/main.php)
```
array('url'=>Yii::app()->getModule('user')->loginUrl, 'label'=>Yii::app()->getModule('user')->t("Login"), 'visible'=>Yii::app()->user->isGuest),
array('url'=>Yii::app()->getModule('user')->registrationUrl, 'label'=>Yii::app()->getModule('user')->t("Registration"), 'visible'=>Yii::app()->user->isGuest),
array('url'=>Yii::app()->getModule('user')->profileUrl, 'label'=>Yii::app()->getModule('user')->t("Profile"), 'visible'=>!Yii::app()->user->isGuest),
array('url'=>Yii::app()->getModule('user')->logoutUrl, 'label'=>Yii::app()->getModule('user')->t("Logout").' ('.Yii::app()->user->name.')', 'visible'=>!Yii::app()->user->isGuest),
```

# Login #

Default users:
  * admin/admin
  * demo/demo

# Configuration #
```
	'modules'=>array(
		'user'=>array(
			'hash' => 'md5',                                     # encrypting method (php hash function)
			'sendActivationMail' => true,                        # send activation email
			'loginNotActiv' => false,                            # allow access for non-activated users
			'autoLogin' => true,                                 # automatically login from registration
			'registrationUrl' => array('/user/registration'),    # registration path
			'recoveryUrl' => array('/user/recovery'),            # recovery password path
			'loginUrl' => array('/user/login'),                  # login form path
			'returnUrl' => array('/user/profile'),               # page after login
			'returnLogoutUrl' => array('/user/login'),           # page after logout
		),
	),
```