The log2timeline projects distribute binary packages for Fedora via the
[GIFT COPR](https://copr.fedorainfracloud.org/groups/g/gift/coprs).

### Building source rpm files

To build source rpm files use [l2tdevtools](https://github.com/log2timeline/l2tdevtools)
with build target: [srpm](https://github.com/log2timeline/l2tdevtools/wiki/Build-script#build-target-srpm).

Alternatively build a source rpm file manually with:
```
rpmbuild -bs
```

### Uploading source rpm files to the GIFT COPR

**Always upload to the testing track first**

To upload to the testing track of GIFT:
```
copr-cli build @gift/testing --nowait dist/plaso-1.5.1-1.src.rpm
```

### Determining which source rpm files to upload

To determine which source rpm files are newer or are not present on GIFT run:

```
PYTHONPATH=. ./tools/manage.py copr-diff-testing
```

