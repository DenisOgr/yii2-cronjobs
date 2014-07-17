Yii2 crontab extension
========
Easiest way to put crontab on your console scripts.

This extension is based on [this](https://github.com/Yiivgeny/Yii-PHPDocCrontab).
Thanks [Yiivgeny](https://github.com/Yiivgeny).

But with a few changes:
- Work eith yii2
- Set config in params (not in phpDocs).

I transfer ​​settings of crontab in local settings(params) configuration, so that the application can be run on different servers with different sets of crontab.

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist denisog/yii2-cronjobs "*"
```

or add

```
"denisog/yii2-cronjobs": "*"
```

to the require section of your `composer.json` file.
Add in params array with cron sets:
```
'cronJobs' =>[
        'test/example1' => [
            'cron'      => '* * * * *',            
        ],
	'test/example2' => [
            'cron'      => '10 * * * *',            
        ],

    ],
```
You can point any settings from [this](https://github.com/Yiivgeny/Yii-PHPDocCrontab/blob/master/examples/ExampleRuCommand.php).
Usage
-----

Once the extension is installed, simply use it in your code by  :

```php
<?= \denisog\cronjobs\AutoloadExample::widget(); ?>```
