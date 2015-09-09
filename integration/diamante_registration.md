---
title: Registration on the DiamanteDesk Portal
---

When a customer registers on the [DiamanteDesk portal](http://orocrmqa.eltrino.com:8090/diamante_1.1/web/app_dev.php/portal/#login) to make a request or report an issue regarding the entity supported by the DiamanteDesk (online store, blog, etc.), the system automatically scans the contact database by the existing emails. If none of the emails match the provided credentials, a new contact is created based on the data provided by the user. If an account with the same email has  been previously registered in the system, the following warning message is displayed:

![Message](img/message.png)

Identical procedure occurs when OroCRM administartor creates a new DiamanteDesk user from the admin panel at _Customers > Contacts > Create Customer_.

This feature can be disabled at _System > Configuration > DiamanteDesk_.