This page contains information relevant to creating a new plaso release.

Release issue template, example https://github.com/log2timeline/plaso/issues/1906:

```
- [ ] Update version
  - `review.py update-version`
- [ ] Create github release and tag
- [ ] Upload source package
  - `./setup.py sdist_test_data`
  - `gpg --armor --detach-sign dist/plaso-$VERSION.tar.gz > dist/plaso-$VERSION.tar.gz.asc`
- [ ] [Update pypi](https://github.com/log2timeline/l2tdocs/blob/master/process/PyPI.md)
- [ ] Update GIFT PPA stable
  - Build Ubuntu source debs
  - Update GIFT PPA testing, dev, stable
- [ ] Update GIFT COPR stable
  - Build Fedora source rpms
  - Update GIFT COPR testing, dev, stable
- [ ] Update l2tbinaries macos
  - Build MacOS binaries
  - update l2tbinaries, testing, dev, stable
- [ ] Update l2tbinaries win32
  - Build Windows binaries
  - update l2tbinaries, testing, dev, stable
- [ ] Update l2tbinaries win64
  - Build Windows binaries
  - update l2tbinaries, testing, dev, stable
- [ ] [Update docker image](https://github.com/log2timeline/l2tdocs/blob/master/process/Maintainers%20guide.md#updating-the-plasos-image-on-dockers-hub-to-the-latest-version-in-ppa)
- [ ] Update Github release with binaries
  - [Build macOS packaged release](https://github.com/log2timeline/l2tdocs/blob/master/process/Maintainers%20guide.md#macos-packaged-release)
  - [Build Windows pyinstaller packaged release](https://github.com/log2timeline/l2tdocs/blob/master/process/Packaging%20with%20pyinstaller.md)
- [ ] Write and publish blog post
  ```
  
