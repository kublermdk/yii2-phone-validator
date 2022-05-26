yii2-phone-validator
==============

Yii2 phone validator is a validator uses phone number util to validate and format the phone number attribute of model.

> This is a very slightly modified version of https://github.com/udokmeci/yii2-phone-validator but with the latest giggsey/libphonenumber-for-php
>
> Created Q2 2022 and the whole reason is to add >= in the requires line for the composer.json i.e `"giggsey/libphonenumber-for-php": ">=8.0"`
>
> This means there's support for newer phone numbers as giggsey/libphonenumber-for-php is up to v8.12.48 as for 2022-05-26th whilst the original udokmeci/yii2-phone-validator was stuck on v7



Note: You'll want to change from `udokmeci\yii2-phone-validator` to `kublermdk\yii2PhoneValidator` if you were using the old one.



How to use?
==============
##Installation with Composer
Just add the line under `require` object in your `composer.json` file.
If you have issues with Composer not finding the repo, then try adding the repositories entry so it knows where to look on Github

``` json
{
    "require": {
        "kublermdk/yii2-phone-validator" : ">=1.0"
    },
    "repositories": [
      {
        "type": "git",
        "url": "https://github.com/kublermdk/yii2-phone-validator"
      }
    ]
}
```
then run 

``` console
$> composer update
```

##Configuration
Now add following in to your `model` rules. 
###Note: ISO 3166-1 alpha-2 codes are required for country attribute. You can use [db-regions](https://github.com/udokmeci/db-regions) for countries list.

``` php
    /**
     * @inheritdoc
     */
    public function rules()
    {
        return [
          [['name', 'country'], 'string', 'max' => 50],
          // add this line
          [['phone'], 'kublermdk\yii2PhoneValidator\PhoneValidator'],
        ];
    }
```
##Advanced
The `country` and `country_code` attributes are tried if `country` or `countryAttribute` is not specified.

``` php
  // All phones will be controlled according to Turkey and formatted to TR Phone Number
  [['phone'], 'kublermdk\yii2PhoneValidator\PhoneValidator','country'=>'TR'],// 

  //All phones will be controlled according to value of $model->country_code
  [['phone'], 'kublermdk\yii2PhoneValidator\PhoneValidator','countryAttribute'=>'country_code'],

  //All phones will be controlled according to value of $model->country_code
  //If model has not a country attribute then phone will not be validated
  //If phone is a valid one will be formatted for International Format. default behavior.
  [['phone'], 'kublermdk\yii2PhoneValidator\PhoneValidator','countryAttribute'=>'country_code','strict'=>false,'format'=>true],  

```

Any forks are welcome.
