# Composer: From Beginning to Expert
**By Jonathan Klein @jonathanklein**

## Using 3rd Party Code

curl installer and pipe it to php.  Move composer.phar to some bin directory in your path.

### Core Components

1. Simple JSON config file, `composer.json`
2. Repository of code (packages)
3. Generated Autoload FIle, `autoload.php`

Type `composer install` to pull vendor code into the blackbox vendor directory.  Add it to your gitignore.

Commit `composer.lock`

`vendor/autoload.php` is the only include in your application

## Autoloading Your Code

PHP Framework Interop Group has approved five standards (called PSRs).

Use PSR-4

## Publishing Packages

Just add name and description to package list.

## Private Repository

Satis provides private repositories

## Advanced Usage

`require-dev` has same syntax as `require` but it allows you list dependencies that don't need to be in production.

Composer provides about a dozen events that you can hook into to run scripts.  `post-update-cmd`, `post-install-cmd`, etc.

### Other useful commands:

* `composer init`
* `composer remove <package-name>`
* `composer validate`
* `composer self-update` (common practice)
* `composer diagnose` (find common issues)
* `composer status` (show what's changed in vendor)