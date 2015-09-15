---
title: Upgrade Guide
---

DiamanteDesk offers our customers a simple and reliable  set of tools designed to take care of their clients, quickly solve any emerging issues and increase the overall customer satisfaction.

DiamanteDesk system can be installed and used in one of the following ways:

* **as a standalone application**. Check out [installation guide](index.md) for detailed instructions on how to install DiamanteDesk as a standalone application that can be used with a web store or website of any kind using [RESTful API](../developer-guide/restful-api-guide.md). 
* **as an extension to OroCRM**. Current version of DiamanteDesk is available only for OroCRM,however in the following versions it will also be available for other CRMs.

## Standalone Application Upgrade

The following instructions are based on the assumption that the application code has been initially obtained from [GitHub repository](https://github.com/eltrino/diamantedesk-application).

**First and foremost**, before performing any steps aimed at help desk upgrading, make sure you have the latest complete backup of all databases and files of your current version, otherwise, you may end up losing the necessary data while upgrading the application.

To start the application update pull the changes from the DiamanteDesk repository using the following command:

{% highlight http %}

git pull

{% endhighlight %}

Checkout the latest stable or any of the previous versions of the application:

{% highlight http %}

git checkout <VERSION TO UPGRADE> 

{% endhighlight %}

Next, execute the following command to upgrade composer dependency:

{% highlight http %}

composer install --prefer-dist

{% endhighlight %}

Remove old caches and assets:

{% highlight http %}

rm -rf app/cache/*
rm -rf web/js/*
rm -rf web/css/*

{% endhighlight %}

And finally, upgrade the application using this command:

{% highlight http %}

php app/console oro:platform:update --env=prod --force
php app/console diamante:update

{% endhighlight %}