#Ansible Role: PHP Brotli Extension#

Build and install the latest version of the
[PHP Brotli Extension](https://github.com/kjdev/php-ext-brotli) on Ubuntu/Debian
based systems.

The PHP Brotli Extension integrates the brotli compression algorith into PHP and
provides the functions `brotli_compress` and `brotli_uncompress`. Brotli
provides moderately improved compression compared to gzip. 

##Requirements##

- Debian (8+)/Ubuntu(13+)
- Git. A role such as [geerlingguy.git](https://galaxy.ansible.com/geerlingguy/git/) can supply this.
- PHP (5.6+)
- PHP Development headers installed for each PHP version you want to target.

##Role Variables##

The following variables are defined in defaults/main.yml. They can be easily
over-riden by any variables defined basically anywhere else with the same name.

    brotli_php_version

The PHP version to target with this build/install. If not provided, will
attempt to select your primary version.

    brotli_clone_dest: ~/git/brotli

The location that brotli will be cloned to for building.

    brotli_enable: true

Whether or not to enable the brotli module after building & installing.

    brotli_path_ini: /etc/php/{{ brotli_php_version }}/mods-available/brotli.ini

The ini path to use to create the brotli.ini if enabling brotli.

    brotli_path_php: php{{ brotli_php_version }}

The path to the php-config binary.

    brotli_path_phpconfig: php-config{{ brotli_php_version }}

The path to the php-config binary.

    brotli_path_phpize: phpize{{ brotli_php_version }}

The path to the phpize binary.

    brotli_path_phpenable: phpenable -v {{ brotli_php_version }}

The path to the phpenable binary.

###Debian 8 with PHP 5.6###
The default paths with Debian 8 and PHP 5.6 are different than on Ubuntu and Debian 9. To seamlessly account for this, the main task checks if the generic path doesn't exist. If the path doesn't exist, it imports the variables from `vars/debian.yml`

##Example Playbook##

To  install `brotli` for just your primary PHP version:

    - hosts: all
      roles:
        -role: nickwilde1990.php-brotli

To install `brotli` for multiple PHP versions.

    - hosts: all
      tasks:
      - include_role:
        name: nickwilde1990.php-brotli
      with_items:
        - 7.0
        - 7.1
      loop_control:
        loop_var: brotli_php_version

##License##

MIT

##Author Information##

Nick Wilde ([BriarMoon Design](https://design.briarmoon.ca))
