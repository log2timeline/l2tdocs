Packages on PyPI are deployed automatically.

Packages on PyPI do not contain the test files due to size limitations.

To manually create a release package with test data for release on GitHub.
```
cp MANIFEST.test_data.in MANIFEST.in 
python -m build --sdist
```
