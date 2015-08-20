# Speedfony Bundle

![GitHub License](https://img.shields.io/badge/license-GPLv2-blue.svg)
[![Build Status](https://travis-ci.org/PHPFastCGI/SpeedfonyBundle.svg?branch=master)](https://travis-ci.org/PHPFastCGI/FastCGIDaemon)
[![Coverage Status](https://coveralls.io/repos/PHPFastCGI/SpeedfonyBundle/badge.svg?branch=master)](https://coveralls.io/r/PHPFastCGI/SpeedfonyBundle?branch=master)

A symfony2 bundle which allows applications to reduce overheads by exposing symfony's Request-Response structure to a FastCGI daemon.

## Introduction

Using this bundle, symfony2 applications can stay alive between HTTP requests whilst operating behind the protection of a FastCGI enabled web server.

## Installing

By turning your Symfony application into a FastCGI application, you can keep the application in memory between request cycles.

To do this, open the terminal in your project directory and use composer to add the Speedfony Bundle to your dependencies.

```sh
composer require "phpfastcgi/speedfony-bundle:~0.5"
```

Next, register the bundle in your AppKernel.php file:

```php
// app/AppKernel.php

// ...
class AppKernel extends Kernel
{
  public function registerBundles()
  {
    $bundles = array(
      // ...
      new PHPFastCGI\SpeedfonyBundle\PHPFastCGISpeedfonyBundle(),
    );

    // ...
  }
// ...
```

## Running the Daemon

To start the daemon listening on port 5000 use the command below. Production mode is selected here for the purposes of generating accurate benchmarks. We do not recommend that you use this package in production mode as it is not yet stable.

Check the FastCGI documentation for your chosen web server to find out how to configure it to use this daemon as a FastCGI application.

```sh
php app/console speedfony:run --port 5000 --env="prod"
```

If you are using apache, you can configure the FastCGI module to launch and manage the daemon itself. For this to work you must omit the "--port" option from the command and the daemon will instead listen for incoming connections on FCGI_LISTENSOCK_FILENO (STDIN).

## Current Status

This daemon is currently in early development stages and not considered stable. A
stable release is expected by September 2015.

## Updates

### v0.5.0
- Upgraded to use FastCGIDaemon v0.5.0
- 
### v0.4.0
- Upgraded to use FastCGIDaemon v0.4.0, renamed command to 'speedfony:run'

### v0.3.2
- Bugfix: Composer dependency on FastCGIDaemon was too loose

### v0.3.1
- Bugfix: Added call to terminate method on symfony kernel (so post response listeners now work)

### v0.3.0
- Upgraded to use FastCGIDaemon v0.3.0

### v0.2.0
- Upgraded to use FastCGIDaemon v0.2.0 and Symfony 2.7 with PSR-7 messages

Contributions and suggestions are welcome.
