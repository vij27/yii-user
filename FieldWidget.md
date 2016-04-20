

# User Field Widget #
class name UW`*` and file name UW`*`.php

## Public Properties ##
|Property|Type|Description|
|:-------|:---|:----------|
|$params |array|           |

## Public Methods ##
|Property|Description|@param|@return|
|:-------|:----------|:-----|:------|
|init()  |Initialization widget|      |array  |
|setAttributes()|           |$value - profile value, $model - profile model, $field\_varname - profile field name|string |
|viewAttribute()|           |$model - profile model,$field - profile fields model item|string |
|editAttribute()|           |$model - profile model,$field - profile fields model item,$htmlOptions=array() - htmlOptions|string |


## Example init() ##
```
public function init() {
	return array(
		'name'=>__CLASS__,
		'label'=>UserModule::t('File field'),
		'fieldType'=>array('VARCHAR'),
		'params'=>$this->params,
		'paramsLabels' => array(
			'path'=>UserModule::t('Upload path'),
		),
		'other_validator'=>array(
			// validators
			'file'=>array(
				// parameters
				'allowEmpty'=>array('','false','true'),
				'maxFiles'=>'',
				'maxSize'=>'',
				'minSize'=>'',
				'tooLarge'=>'',
				'tooMany'=>'',
				'tooSmall'=>'',
				'types'=>'',
				'wrongType'=>'',
			),
		),
	);
}
```

# Profile Relation Widget #
## Example - Country list ##

Table Country model
|id|title|
|:-|:----|
|1 |Afghanistan|
|2 |Albania|
|3 |Algeria|
|4 |American Samoa|
|5 |Andorra|
|...| |

## Add relation to Country model ##
```
class Country extends CActiveRecord {
...

public function relations()
{
	return array(
		'profiles'=>array(self::HAS_MANY, 'Profile', 'country_id'),
	);
}

...
}
```

## Add new field ##
Create Profile Field
  * Variable name - country\_id
  * Title - Country ID
  * Widget - Relation Belongs To
  * Widget parametrs
    * Model Name - Country
    * Lable field name - title
    * Empty item name - "----"
    * Profile model relation name - country

![http://2mx.org/projects/yii-user/screenshots/add_profile_relation_field.png](http://2mx.org/projects/yii-user/screenshots/add_profile_relation_field.png)

## Add relation to Profile model ##
./config/main.php
```

'modules'=>array(
	'user'=>array(
...
		'profileRelations'=>array(
			'country'=>array(CActiveRecord::BELONGS_TO, 'Country', 'country_id'),
		),
...
	),
...
),
```