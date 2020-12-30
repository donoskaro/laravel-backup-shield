# Laravel Backup Shield

[![Latest Version on Packagist][ico-version]][link-packagist]
[![Software License][ico-license]](LICENSE.md)
[![Build Status][ico-build]][link-build]
[![Scrutinizer Score][ico-scrutinizer]][link-scrutinizer]

![backup-shield](https://user-images.githubusercontent.com/907114/40585078-b42b31ba-61ac-11e8-9db6-b5497e156f5a.png)

## Secure your backups

**This package helps you encrypt and password-protect your backups taken with [Spatie's](https://github.com/spatie) fantastic [spatie/laravel-backup](https://github.com/spatie/laravel-backup)-package.**

Backup Shield simply listens for when the .zip-file generated by Laravel-backup is done, grabs it and applies your password and encryption of your liking.

*Using older versions of Laravel? Check out the [v1 branch](https://github.com/olssonm/laravel-backup-shield/tree/v1) (for Laravel 5.2) and the [v2 branch](https://github.com/olssonm/laravel-backup-shield/tree/v2).*

## Requirements

`php: 7.3|^8.0`  
`ext-zip: ^1.14`  
`laravel: ^6|^7|^8`

An appropriate zip-extension should be come with your PHP-install since PHP 7.2. If you for some reason don't have it installed – and don't want to install/upgrade it – look a versions prior to v3.4 of this package.

## Installation

```bash
composer require olssonm/laravel-backup-shield
```

## Configuration

Publish your configuration using `php artisan vendor:publish` and select `BackupShieldServiceProvider`. Or directly via ```php artisan vendor:publish --provider="Olssonm\BackupShield\BackupShieldServiceProvider"```.

You only have the ability to set two different options; password and encryption.

```php
// Default configuration; backup-shield.php
return [
    'password' => env('APP_KEY'),
    'encryption' => \Olssonm\BackupShield\Encryption::ENCRYPTION_DEFAULT
];
```

#### Password

Your password (*duh*). The default is the application key (`APP_KEY` in your .env-file). You might want to set something more appropriate. Remember to use long strings and to keep your password safe – **without it you will never be able to open your backup**.

Set to `NULL` if you want to keep your backup without a password.

#### Encryption

Set your type of encryption. Available options are:

`\Olssonm\BackupShield\Encryption::ENCRYPTION_DEFAULT` (AES 128)  
`\Olssonm\BackupShield\Encryption::ENCRYPTION_WINZIP_AES_128` (AES 128)  
`\Olssonm\BackupShield\Encryption::ENCRYPTION_WINZIP_AES_192` (AES 192)  
`\Olssonm\BackupShield\Encryption::ENCRYPTION_WINZIP_AES_256` (AES 256)  

#### Regarding the layered archive

This package adds the backup-zip created by spatie/laravel-backup inside a new password protected archive. This is to disable its contents to be able to be viewed without a password – instead only backup.zip will be displayed. Becouse, even without a password, a zip's contents (i.e. the file- and folder names) can be extracted.

## Testing

``` bash
$ composer test
```

or

``` bash
$ phpunit
```

## License

The MIT License (MIT). Please see the [LICENSE.md](LICENSE.md) for more information.

© 2020 [Marcus Olsson](https://marcusolsson.me).

[ico-version]: https://img.shields.io/packagist/v/olssonm/laravel-backup-shield.svg?style=flat-square
[ico-license]: https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square
[ico-build]: https://img.shields.io/github/workflow/status/olssonm/laravel-backup-shield/Run%20tests.svg?style=flat-square&label=tests
[ico-downloads]: https://img.shields.io/packagist/dt/olssonm/laravel-backup-shield.svg?style=flat-square
[ico-scrutinizer]: https://img.shields.io/scrutinizer/g/olssonm/laravel-backup-shield.svg?style=flat-square
[link-packagist]: https://packagist.org/packages/olssonm/laravel-backup-shield
[link-build]: https://github.com/olssonm/laravel-backup-shield/actions?query=workflow%3A%22Run+tests%22
[link-scrutinizer]: https://scrutinizer-ci.com/g/olssonm/laravel-backup-shield
