# Docksal powered Drupal 8 Installation

This is a sample vanilla Drupal 8 installation pre-configured for use with Docksal.  

Features:

- Vanilla Drupal 8
- `fin init` [example](.docksal/commands/init)
- Using the [default](.docksal/docksal.env#L9) Docksal LAMP stack with [image version pinning](.docksal/docksal.env#L13-L15)
- PHP and MySQL settings overrides [examples](.docksal/etc)
- Drush aliases [example](drush/aliases.drushrc.php) (`drush @docksal status`)

## Setup instructions

### Step #1: Docksal environment setup

**This is a one time setup - skip this if you already have a working Docksal environment.**  

Follow [Docksal environment setup instructions](https://docs.docksal.io/en/master/getting-started/env-setup)

### Step #2: Project setup

1. Clone this repo into your Projects directory

    ```
    git clone https://github.com/docksal/drupal8.git drupal8
    cd drupal8
    ```

2. Initialize the site

    This will initialize local settings and install the site via drush

    ```
    fin init
    ```

3. Point your browser to

    ```
    http://drupal8.docksal
    ```

When the automated install is complete the command line output will display the admin username and password.


## More automation with 'fin init'

Site provisioning can be automated using `fin init`, which calls the shell script in [.docksal/commands/init](.docksal/commands/init).  
This script is meant to be modified per project. The one in this repo will give you a good starting example.

Some common tasks that can be handled by the init script (an other [custom commands](https://docs.docksal.io/en/master/fin/custom-commands/)):

- initialize local settings files for Docker Compose, Drupal, Behat, etc.
- import DB or perform a site install
- compile Sass
- run DB updates, revert features, clear caches, etc.
- enable/disable modules, update variables values


## Security notice

This repo is intended for quick start demos and includes a hardcoded value for `hash_salt` in `settings.php`.  
If you are basing your project code base on this repo, make sure you regenerate and update the `hash_salt` value.  
A new value can be generated with `drush ev '$hash = Drupal\Component\Utility\Crypt::randomBytesBase64(55); print $hash . "\n";'` 
