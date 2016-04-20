

# Installation #
  * Unpack files in your project/protected
  * Insert to config/main.php
```
return array(
#...
	// autoloading model and component classes
	'import'=>array(
		'application.models.*',
		'application.components.*',
		'application.modules.user.models.*',
		'application.modules.user.components.*',
	),
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
  * Insert items into zii.widgets.CMenu array (protected/views/layouts/main.php)
```
array('url'=>Yii::app()->getModule('user')->loginUrl, 'label'=>Yii::app()->getModule('user')->t("Login"), 'visible'=>Yii::app()->user->isGuest),
array('url'=>Yii::app()->getModule('user')->registrationUrl, 'label'=>Yii::app()->getModule('user')->t("Register"), 'visible'=>Yii::app()->user->isGuest),
array('url'=>Yii::app()->getModule('user')->profileUrl, 'label'=>Yii::app()->getModule('user')->t("Profile"), 'visible'=>!Yii::app()->user->isGuest),
array('url'=>Yii::app()->getModule('user')->logoutUrl, 'label'=>Yii::app()->getModule('user')->t("Logout").' ('.Yii::app()->user->name.')', 'visible'=>!Yii::app()->user->isGuest),
```

# Login #

Default users:
  * admin/admin
  * demo/demo

# Module parameters #
|Property|Type|Description|Default|
|:-------|:---|:----------|:------|
|user\_page\_size|int |items on page|10     |
|fields\_page\_sizeint|items on page|10         |
|hash    |string|hash method|md5    |
|sendActivationMail|boolean|use email for activation user account|true   |
|loginNotActiv|boolean|allow auth for is not active user|false  |
|activeAfterRegister|boolean|activate user on registration (only $sendActivationMail = false)|false  |
|autoLogin|boolean|login after registration (need loginNotActiv or activeAfterRegister = true)|true   |
|registrationUrl|array|regitration path|array("/user/registration")|
|recoveryUrl|array|recovery path|array("/user/recovery/recovery")|
|loginUrl|array|login path |array("/user/login")|
|logoutUrl|array|logout path|array("/user/logout")|
|profileUrl|array|profile path|array("/user/profile")|
|returnUrl|array|return path after login|array("/user/profile")|
|returnLogoutUrl|array|return path after logout|array("/user/login")|
|relations|array|User model relation from other models|array()|
|profileRelations|array|Profile model relation from other models|array()|
|captcha |array|use captcha|array('registration'=>true)|
|tableUsers|string|User model table|{{users}}|
|tableProfiles|string|Profile model table|{{profiles}}|
|tableProfileFields|string|ProfileField model table|{{profiles\_fields}}|