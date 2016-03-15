Introduction
============
This documentation applies to the 5.6.0 version of [nodejs](https://nodejs.org/en/).

Windows
=======

Custom Setup
------------
Use defaults

Global
======
To view the globally installed packages:
```bash
npm ls -global -depth 0
```

The following global packages are used by archetypal
```bash
npm install -g aws-sdk
npm install -g bower
npm install -g gulp
npm install -g tsd
npm install -g yo
```


Version
=======
To check installed version:

```bash
node --version
```

Latest package version:

```bash
npm view <package> version
```
