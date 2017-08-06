The log2timeline projects distribute binary packages for Ubuntu via the
[GIFT PPA](https://launchpad.net/~gift).

### Building source dpkg files

To build source dpkg file use [l2tdevtools](https://github.com/log2timeline/l2tdevtools)
with build target: [dpkg-source](https://github.com/log2timeline/l2tdevtools/wiki/Build-script#build-target-dpkg-source).

Alternatively build a source dpkg file manually with:
```
debuild -Sa
```

### Uploading source dpkg files to the GIFT PPA

**Always upload to the testing track first**

To upload to the testing track of GIFT:
```
dput ppa:gift/testing python-plaso_20170806-1ppa1~trusty_source.changes
```

