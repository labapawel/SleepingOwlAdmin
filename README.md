![bg](https://cloud.githubusercontent.com/assets/773481/14028746/24d7efa8-f20f-11e5-8e38-3d264739f0aa.png)

## Laravel 5.2 Admin Module

[![Build Status](https://travis-ci.org/SleepingOwlAdmin/demo.svg?branch=master)](https://travis-ci.org/SleepingOwlAdmin/demo)
[![StyleCI](https://styleci.io/repos/52141393/shield?style=flat)](https://styleci.io/repos/52141393)
[![Join the chat at https://gitter.im/LaravelRUS/SleepingOwlAdmin](https://badges.gitter.im/LaravelRUS/SleepingOwlAdmin.svg)](https://gitter.im/LaravelRUS/SleepingOwlAdmin?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Latest Stable Version](https://poser.pugx.org/sleeping-owl/admin/v/unstable.svg)](https://packagist.org/packages/laravelrus/sleepingowl)
[![License](https://poser.pugx.org/laravelrus/sleepingowl/license.svg)](https://packagist.org/packages/laravelrus/sleepingowl)

*Note: This is the development version. If you are looking for the stable version check out [master branch](https://github.com/LaravelRUS/SleepingOwlAdmin).*

SleepingOwl Admin is an administrative interface builder for Laravel.

### Used npm packages:

```js
"devDependencies": {
	"jquery": "^2.1.4",
	"underscore": "1.8.3",
	"bootstrap": "^3.3.7",
	"eonasdan-bootstrap-datetimepicker": "^4.15.35",
	"font-awesome": "^4.6.3",
	"moment": "^2.14.1",
	"nestable": "^0.2.0",
	"noty": "^2.3.8",
	"sortablejs": "1.4.2",
	"select2": "^4.0.3",
	"metismenu": "^2.5.2",
	"datatables.net": "^1.10.12",
	"admin-lte": "^2.3.5",
	"x-editable": "^1.5.1",
	"dropzone": "4.3.0",
	"i18next": "^3.4.1",
	"vue": "^1.0.26",
	"vue-resource": "^0.9.3",
	"sweetalert2": "^4.1.0",
	"magnific-popup": "^1.1.0"
}
```

## Installation

 1. Require this package in your composer.json and run composer update:

  ```
  "require": {
    "php": ">=5.5.9",
    "laravel/framework": "5.2.*",
    ...
    "laravelrus/sleepingowl": "4.*@dev"
  },
  ```

  Or `composer require laravelrus/sleepingowl:4.*@dev`

 2. After composer update, insert service provider `SleepingOwl\Admin\Providers\SleepingOwlServiceProvider::class,`
 before `Application Service Providers...` to the `config/app.php`

  **Example**
  ```php
      ...
      /*
       * SleepingOwl Service Provider
       */
        SleepingOwl\Admin\Providers\SleepingOwlServiceProvider::class,
  
      /*
       * Application Service Providers...
       */
      App\Providers\AppServiceProvider::class,
      ...
  ```

 3. Run this command in the terminal (if you want to know more about what exactly this command does, see [install command documentation](http://sleeping-owl.github.io/en/Commands/Install.html)):

```
$ php artisan sleepingowl:install
```
    
## Laravel 5.1 usage

SleepingOwl are compatible with Laravel 5.1. But full performance is not guaranteed.

### Installation

- See `Installation` section of Laravel 5.2
- After all actions: open `config/sleeping_owl.php` and change `'middleware' => ['web']` to `'middleware' => []`

---

## Authentication
By default, admin module uses Laravel authentication.

If you want to use auth, you can run artisan command `php artisan make:auth` (https://laravel.com/docs/5.2/authentication) 
and append middleware `auth` to `config/sleeping_owl.php` 

```php
	...
	'middleware' => ['web', 'auth']
	...
```

### Supporting of old authentication

If you want to migrate from an older version you can use old auth.

Steps:

1. Add new user provider in `config/auth.php`

  ```php
  'providers' => [
    'users' => [
      'driver' => 'eloquent',
      'model' => App\User::class,
    ],
    'administrators' => [
      'driver' => 'eloquent',
      'model' => SleepingOwl\Admin\Auth\Administrator::class,
    ],
  ],
  ```

2. Add new guards or change existing in `config/auth.php`

  ```php
  'guards' => [
    'web' => [
      'driver' => 'session',
      'provider' => 'administrators', // change existing provider
    ],
    
    // or add new
    
    'admin' => [
      'driver' => 'session',
      'provider' => 'administrators',
    ],
  ],
  ```

3. Setting up middleware

  By default `auth` middleware use default guard, selected in `config/auth.php`
  
  ```php
  'defaults' => [
    'guard' => 'web', <- default
    ...
  ],
  ```
  
  You can change default guard to `admin` or change middleware in `config/sleeping_owl.php` to
  
  ```php
  'middleware' => ['web', 'auth:admin'],
  ```

---

## Demo project

You can download the demo project at https://github.com/SleepingOwlAdmin/demo

## Documentation

* [Russian](http://sleepingowl.laravel.su/docs/4.0/)
* English

## Copyright and License

Admin was written by Sleeping Owl for the Laravel framework and is released under the MIT License. 
See the LICENSE file for details.
