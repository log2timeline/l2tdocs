The package on PyPI does not contain the test files due to size limitations.

To create a release package with test data for release on github.
```
python setup.py sdist_test_data
```

## .pypirc

Set up `.pypirc` to have both `pypitest` and `pypi`:
```
[distutils]
index-servers =
  pypi
  pypitest

[pypi]
repository=https://upload.pypi.org/legacy/
username=$USERNAME
password=$PASSWORD

[pypitest]
repository=https://test.pypi.org/legacy/
username=$USERNAME
password=$PASSWORD
```

Also see: https://packaging.python.org/guides/migrating-to-pypi-org/

## PyPI

Always first test changes on `pypitest` before making changes to `pypi`.

To create a new release:
```
rm -rf build/ dist/
python setup.py sdist
DIST_PACKAGE=`ls -1 dist/*.tar.gz`
gpg --armor --detach-sign --output ${DIST_PACKAGE}.asc ${DIST_PACKAGE}
```

To upload a new release to pypitest:
```
twine upload --repository pypitest ${DIST_PACKAGE} ${DIST_PACKAGE}.asc
```

To upload a new release to pypi:
```
twine upload ${DIST_PACKAGE} ${DIST_PACKAGE}.asc
```

### Also see:

* [How to submit a package to PyPI](http://peterdowns.com/posts/first-time-with-pypi.html)
* [Migrating to PyPI.org](https://packaging.python.org/guides/migrating-to-pypi-org)
* [Packaging and Distributing Projects - Create an account](https://packaging.python.org/tutorials/distributing-packages/#create-an-account)
* [Packaging and Distributing Projects - Upload your distributions](https://packaging.python.org/tutorials/distributing-packages/#upload-your-distributions)

