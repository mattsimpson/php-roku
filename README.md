Roku PHP Library
================================================

[![Build Status](https://api.travis-ci.org/svilborg/php-roku.png?branch=master)](https://travis-ci.org/svilborg/php-roku)
[![Latest Stable Version](https://poser.pugx.org/svilborg/php-roku/v/stable.png)](https://packagist.org/packages/svilborg/php-roku)
[![Latest Unstable Version](https://poser.pugx.org/svilborg/php-roku/v/unstable.png)](https://packagist.org/packages/svilborg/php-roku)


PHP Library for communication with Roku External Control Protocol

Installation
================

Installing via Composer
-----------------------
Install composer in a common location or in your project:

```bash
curl -s http://getcomposer.org/installer | php
```

Create the composer.json file as follows:

```json
{ 
    "require": {
        "svilborg/php-roku": "dev-master"
    }
}
```

Run the composer installer:

```bash
php composer.phar install
```

Requirements
============

* PHP Version >=5.3.2.
* PHP Httpful Library

Usage
=====

Execute commands :

```php

$roku = new \Roku\Roku("192.168.72.10", 8060, 0.2);

$roku->up();

$roku->select();

$roku->literals("test@gmail.com");

$roku->down();

$roku->down();

$roku->select();

```

List the applicatioin installed on the device :

```php


$roku = new \Roku\Roku("192.168.72.10", 8060, 0.2);

$applications = $roku->apps();

foreach ($applications as $application) {
    echo $application->getId();
    echo $application->getVersion();
    echo $application->getName();
    echo "\n";
}

```

Get device information :

```php


$roku = new \Roku\Roku("192.168.72.10", 8060, 0.2);

$device = $roku->device();

echo $device->getSerialNumber();
echo $device->getModelName();
echo $device->getModelDescription();
// etc..


```

Usage Commandline
=================

For the list of commands execute :

```bash

$ vendor/bin/roku --help

```

It displays :

```bash

PHP Roku Console

Usage: roku [OPTION] ..

-h <host>       Host
-p <port>       Port
-d <delay>      Delay between each command
-i              Interactive mode (Listens for keyboard keystrokes)
-c <commands>   Command mode (Specify commands to be executed, Example -c "up down test@gmail.com down select home")
-t              Test Mode (Does not send commands.Just simulates them.)
--help          Shows this help

```

Example usage of command and interactive modes :

```bash

$ vendor/bin/roku -h 192.168.72.10 -p 8060 -d 1 -c "up test@gmailc.om down down select home"

$ vendor/bin/roku  -h 192.168.72.10 -d 1 -i

```

Running the tests
=================

First, install PHPUnit with `composer.phar install --dev`, then run
`./vendor/bin/phpunit`.
