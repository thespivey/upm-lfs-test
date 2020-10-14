# Overview

This is a bug repro.   Git LFS appears not work when UPM packages are fetched with a path parameter.

# Details
This repo contains a Unity app, targeting Unity 2019.4.12f1.
All it contains is a Packages/manifest.json that points to two git packages:
```
    "com.microsoft.testupm.root": "git+https://github.com/thespivey/upm-lfs-package.git",
    "com.microsoft.testupm.child": "git+https://github.com/thespivey/upm-lfs-package.git?path=child",
```

The existence of two packages in the same repo is not important here, it only serves to illustrate the LFS issue.

```
# Root package works correctly
> type .\Library\PackageCache\com.microsoft.testupm.root@d5f1335615\child\test.lfs
This file is stored in LFS.

# Child package does not pull from LFS
> type .\Library\PackageCache\com.microsoft.testupm.child@d5f1335615\test.lfs
version https://git-lfs.github.com/spec/v1
oid sha256:9b7003770c79e47c0a5fdeb91d3e1ca9b6bced7ef1fd912d754cef629b0c4ed5
size 27
```
