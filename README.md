Yii2 cronjobs extension
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

- **Step 1:** The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```sh
php composer.phar require --prefer-dist denisogr/yii2-cronjobs "dev-master"
```

or add

```json
"denisogr/yii2-cronjobs": "dev-master"
```

to the require section of your `composer.json` file.
- **Step 2:**  Set aliase  @runnerScript in console config. This absolutely path to runner script (I can not find another way to get runner script).
Change path to runner script as your project. 
```php
Yii::setAlias('@runnerScript', dirname(dirname(dirname(__FILE__))) .'/yii');
```
- **Step 3:**  Add to console config: 
```
config/console.php
```
```php
return [
    //...
    'controllerMap' => [
    	'cron' => [
    	    'class' => 'denisog\cronjobs\CronController'
    	],
    ],
]
```
- **Step 4:**  Add task to system scheduler (cron on unix, task scheduler on windows) to run every minute:

```sh
* * * * * /path/to/yii/application/protected/yii cron
```
Usage
-----

Add in params array with cron sets:
```php
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

Usage examples
--------------
1 Use log path for stdout:
```php

/**
 * Parameters stdout and stderr can be a mask including next variables:
 *     %L - yii2 logsDir
 *     %C - command name
 *     %A - action name
 *     %P - PID of running process
 *     %D(format) - date format; the same sintax as that date()
 *
 */
 return [
    'cronJobs' =>[
    	'test/example1' => [
    	    'cron'        => '* * * * *',
    	    'cron-stdout' => '/tmp/Example_%C.%A.log'
	],
    ]
]
```

2 Using custom stderr:
```php
return [
    'cronJobs' =>[
    	'test/example2' => [
    	    'cron'        => '* * * * *',
    	    'cron-stdout' => '/tmp/Example_%C.%A.log',
    	    'cron-stderr' => '/tmp/ExampleCommandError.log'
    	],
    ]
]
```

3 Using args:
```php
return [
    'cronJobs' =>[
    	'test/example2' => [
    	    'cron'        => '* * * * *',
    	    'cron-args' => '--limit=5 --offset=10'
    	],
    ]
]
```

4 Using tags:
```php
return [
    'cronJobs' =>[
    	'test/example2' => [
    	    'cron'        => '* * * * *',
    	    'cron-tags' => 'dbserver cacheserver'
    	],
    ]
]
```

5 Using extended time format:
```php
return [
    'cronJobs' =>[
    	'test/example2' => [
    	    'cron'        => '10,25-30,40 *\2 15-21,23-27 1-6\2 *'
    	],
    ]
]
```
