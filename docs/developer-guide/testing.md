# Testing (Quality Assurance)

DiamanteDesk team goes to all lengths to create a user-friendly product of high quality both for our Clients and their customers; hence, we take each step of the development process seriously. Certainly, software testing is among top priority phases as it ensures that each Client can truly rely on the support function of a help desk.

We use three major types of software testing to ensure stable work of DiamanteDesk functionality: **unit testing** and **functional testing** as automated strategies and **manual testing** that covers other possible defects. 

## Unit Testing

Unit testing is a strategy used to ensure that an individual unit (function or method) in a class performs a set of its tasks correctly. This type of testing is performed separately from the operational environment,

DiamanteDesk has a suite of unit tests in the tests directory, covering the key functionality of the application. All the newly added functionality that cannot make it through the test suite can't get checked into DiamanteDesk.

All the automated tests are performed in the PHPUnit. To start the unit testing, use the following command:

    phpunit -c src/Diamante/{Bundle}/phpunit.xml.dist src/Diamante/DeskBundle/Tests


The **{Bundle}** variable defines specific part of the application responsible for the certain functionality. DiamanteDesk is separated into separate **bundles**, such as ApiBindle, FrontBundle, EmbeddedFormBundle, EmailProcessingBundle, etc. When performing unit testing, add the name of a corresponding  bundle into the command.

To learn more about Unit testing on PHPUnit, folllow this [link](https://phpunit.de/manual/current/en/phpunit-book.pdf).

##Functional Testing

Functional testing is performed using the test data as it deals with the methods that may interact with certain dependencies such as databases or web services. In other words, functional testing ensures that the system functions just as it is expected to.

Test parameters can be configured and updated in the ```parameters_test.yml``` file.

To start functional testing, we setup a test database and load it with fixtures (specific set of data). Use the following command to create testing environment:

    app/console doctrine:database:create --env=test
    
The following command creates tables in the database:

    app/console doctrine:schema:update --force --env=test

##Manual Testing

While automated unit and functional testing covers most of the issues concerning the proper application functioning and helps developers detect the majority of bugs in code, it still has some limitations. Manual testing is more appropriate for the UI testing and dealing with less predictable user behavior.