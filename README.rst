deployer-media-typo3
=====================

      .. image:: http://img.shields.io/packagist/v/sourcebroker/deployer-media-typo3.svg?style=flat
         :target: https://packagist.org/packages/sourcebroker/deployer-extended-typo3

      .. image:: https://img.shields.io/badge/license-MIT-blue.svg?style=flat
         :target: https://packagist.org/packages/sourcebroker/deployer-media-typo3

.. contents:: :local:

What does it do?
----------------

This package provides settings to use `sourcebroker/deployer-extended-media`_ package with TYPO3 CMS.
It allows to sync media between instances.

Installation
------------

1) Install package with composer:
   ::

      composer require sourcebroker/deployer-media-typo3


2) Put following lines on the beginning of your deploy.php:
   ::

      require_once(__DIR__ . '/vendor/sourcebroker/deployer-loader/autoload.php');
      new \SourceBroker\DeployerMediaTypo3\Loader();


Synchronizing media
-------------------

The command for synchronizing media from production to local instance (usually your laptop):
::

   dep media:pull live


Command for synchronizing media from production to staging instance is:
::

   dep media:copy production --options=target:staging

   # Creates symlinks to each file in shared folder. Good to safe space on disk.
   dep media:link production --options=target:staging


Example of working configuration
--------------------------------

This is example of working configuration for TYPO3 13.

::

  <?php

  namespace Deployer;

  require_once(__DIR__ . '/vendor/sourcebroker/deployer-loader/autoload.php');

  new \SourceBroker\DeployerMediaTypo3\Loader();

  host('production')
      ->setHostname('vm-dev.example.com')
      ->setRemoteUser('deploy')
      ->set('bin/php', '/home/www/t3base11-public/production/.bin/php');
      ->set('deploy_path', '/home/www/t3base13/production');

  host('staging')
      ->setHostname('vm-staging.example.com')
      ->setRemoteUser('deploy')
      ->set('bin/php', '/home/www/t3base11-public/staging/.bin/php');
      ->set('deploy_path', '/home/www/t3base13/staging');

  localhost('local')
      ->set('bin/php', 'php')
      ->set('deploy_path', getcwd());



Changelog
---------

See https://github.com/sourcebroker/deployer-media-typo3/blob/master/CHANGELOG.rst


.. _sourcebroker/deployer-extended-media: https://github.com/sourcebroker/deployer-extended-media
