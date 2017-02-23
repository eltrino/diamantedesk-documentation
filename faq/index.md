---
title: FAQ
---

#### Login is not working due to session storage issue

Could be an issue that your session data not written into session storage. Such issue appears when your session storage configured to use files and those files placed on NFS volume. You should reconfigure to use different session storage (Redis for example) or avoid NFS in your setup. 

#### Error "Property ... does not exist" during installation

When you install or reinstall application make sure that 

- caches have been flushed
- db is clean or you've selected appropriate option during install to drop it



