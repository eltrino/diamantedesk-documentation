---
title: Testing
---

Software testing is an essential part of the development process. Deliberate and thorough testing ensures that software will work properly and our Clients will not face unforeseen consequences when using it. 

DiamanteDesk team pays proper attention to testing, both **unit** and **functional**, and we rely heavily on PHPUnit, a software suite designed for testing, which is commonly accepted as an industrial standard for quality assurance. 

DiamanteDesk application offers all the required tests bundled with the most reliable version of PHPUnit. 

##Unit Testing

Unit testing is intended to test individual software components in strict isolation from the _live_ system resources, thus, ensuring application integrity. Unit testing utilizes the "mock" object approach to test the behavior of each component in different cases without affecting any other part of the system. 

DiamanteDesk Unit Test Suite is available in each bundle and can be run from the command line. 
The way of calling the PHPUnit binary may vary on your setup. The following examples are be based on the assumption  that your PHPUnit is installed globally, the DiamanteDesk application is installed via the Composer, and the source code resides in the *vendor/diamante* folder of your server's document root.

To run the test suite, issue the following command:

{% highlight sh %}
bash phpunit -c vendor/diamante/{BundleName}/phpunit.xml.dist vendor/diamante/{BundleName}/Tests
{% endhighlight %}

_**Note:** {BundleName} is a placeholder for a name of the bundle you want to test, e.g. DeskBundle, ApiBundle, FrontBundle, etc._

The output consists of the test results, including the general number of tests run, assertions made and the number of failed and skipped tests or tests containing errors.

##Functional Testing

Functional testing is aimed at testing the application integrity within the current setup. Depending on the incoming request parameters it may include the database interaction, file system operation and result processing testing, which is a reason why functional testing is commonly referred to as Integration testing.

The best practice for functional testing is using the test database filled with randomly generated test data (also known as fixtures). The testing engine mimics the "real" request via different internal tools and analyzes the systems response. Moreover, the built-in tools allow building complex testing scenarios with different parameters which is a great way to test system behavior and analyze system response on our interaction with different UI elements; for example, when clicking buttons and filling out the forms on the web pages.

DiamanteDesk Unit Testing Suite is available by issuing the following command:

{% highlight sh %}
bash phpunit -c vendor/diamante/{BundleName}/Tests/Functional/phpunit/xml.dist vendor/diamante/{BundleName}/Tests/Functional
{% endhighlight %}

The output of the command execution is similar to the unit testing output. 

_**Note:** We highly recommend setting up a separate database for the proper software testing._

### How to Setup Testing Environment

* Set up your test environment parameters by creating the following file:

{% highlight sh %}
app/config/parameters_test.yml
{% endhighlight %}

The  structure of this file is similar to your *prod* environment one.

* Reinstall DiamanteDesk, using **--env=test** flag if required (depends on your setup). Please refer to the [Installation Manual](../installation-guide/index.html) for more details. 

### Running the Suite of Functional Tests

When the command described above is issued, the following happens:

1. There is an option in the configuration file, specifying the default **bootstrap.php** file, required to inform the application on its environment. The script in that file runs every time you run the test suite. Utilizing this file makes it possible to provide the test database with the test data (fixtures) that shall be processed.
2. When fixtures are being loaded, the existing tables shall be truncated in order to get rid of the data from the previous test. This shall be done every time we run the test suite to ensure getting consistent results.
3. Next, the new set of automatically generated data shall be loaded.
4. Eventually, the test suite launches the first test and continues the process as specified in the **phpunit.xml.dist** file.

###Adding New Tests and Test Data

DiamanteDesk application is open for contributing, so if you want to add a new functionality to the system, we strongly recommend writing unit/functional tests for your bundle and testing it against the existing code to ensure the app integrity.  All the newly added functionality that cannot make it through the test suite can't get checked into DiamanteDesk.

Here are a few rules we follow when testing DiamanteDesk application:

1. Unit tests are placed in the **Tests** folder of your bundle. 
2. Functional tests are placed in the **Tests/Functional** folder.
3. Each set of tests has it's own config. 
4. Functional test suite is required to have a **bootstrap** script for correct autoloading.
5. Fixtures are added via placing your data generator class into the **DataFixtures/Test** folder.
6. Each file name, which contains tests, has to end with **Test.php**.

These simple recommendations enable seamless integration of new tests into the existing test suites.