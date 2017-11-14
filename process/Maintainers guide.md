This page contains information relevant to maintainers of the log2timeline projects.

* [Mailing list](https://github.com/log2timeline/l2tdocs/blob/master/process/Maintainers%20guide.md#mailing-list)
* [Maintainer guidelines](https://github.com/log2timeline/l2tdocs/blob/master/process/Maintainers%20guide.md#maintainer-guidelines)
* [Maintainer tools](https://github.com/log2timeline/l2tdocs/blob/master/process/Maintainers%20guide.md#maintainer-tools)
* Generating plaso test files
* Generating API docs with Sphinx-doc
* [Generating plaso wiki pages](https://github.com/log2timeline/l2tdocs/blob/master/process/Maintainers%20guide.md#generating-plaso-wiki-pages)
* [Creating a packaged release](https://github.com/log2timeline/l2tdocs/blob/master/process/Maintainers%20guide.md#creating-a-packaged-release)
  * [Fedora source rpm for GIFT COPR](https://github.com/log2timeline/l2tdocs/blob/master/process/GIFT%20COPR.md)
  * [macOS packaged release](https://github.com/log2timeline/l2tdocs/blob/master/process/Maintainers%20guide.md#macos-packaged-release)
  * [Ubuntu source dpkg for GIFT PPA](https://github.com/log2timeline/l2tdocs/blob/master/process/GIFT%20PPA.md)
  * [Windows packaged release](https://github.com/log2timeline/l2tdocs/blob/master/process/Packaging%20with%20pyinstaller.md)
  * [PyPI](https://github.com/log2timeline/l2tdocs/blob/master/process/Maintainers%20guide.md#pypi)
* [Updating plaso's docker image](https://github.com/log2timeline/l2tdocs/blob/master/process/Maintainers%20guide.md#updating-the-plasos-image-on-dockers-hub-to-the-latest-version-in-ppa)

## Mailing list

Maintainers mailing list: log2timeline-maintainers@googlegroups.com

## Maintainer guidelines

* [Feature requests and bug reports](https://github.com/log2timeline/plaso/wiki/Feature-requests-and-bug-reports)

## Maintainer tools

If you intend to help maintain on plaso you'll also need to install the following tools:

* [Sphinx-doc](https://github.com/log2timeline/l2tdocs/blob/master/process/Installing%20sphinx-doc.md)

## Generating plaso test files

To generate `pinfo_test.json.plaso` and `psort_test.json.plaso` run the following script:
```
./config/tests/generate_test_files.sh
```

## Generating API docs with Sphinx-doc

Plaso uses [sphinx](http://sphinx-doc.org/) to generate API documentation. The plaso configuration uses the [autodoc](http://sphinx-doc.org/ext/autodoc.html) plugin for automatic documentation generation, and the [napoleon](http://sphinxcontrib-napoleon.readthedocs.org/en/latest/sphinxcontrib.napoleon.html) plugin to read our “Google style” docstrings. 

The configuration is stored [here](https://github.com/log2timeline/plaso/blob/master/docs/conf.py) and the actual HTML documentation is built and stored with readthedocs.org, as described below.
The [merge_submit script](https://github.com/log2timeline/plaso/blob/master/utils/merge_submit.sh), which is run by the maintainers, triggers a [sphinx-apidoc](http://sphinx-doc.org/man/sphinx-apidoc.html) run, which will generate reStructured text files which readthedocs will use to generate the HTML docs. 

One little wrinkle in this pipeline is that to generate the API docs, readthedocs needs to `import` each python file. This will fail if it can't import all dependencies, and it's not possible to install native dependencies on readthedocs. The Sphinx configuration tries to take care of this by automatically mocking the dependencies in [dependencies.py](https://github.com/log2timeline/plaso/blob/master/plaso/dependencies.py) but it may be necessary on occasion to add a dependency explicitly to the sphinx config.

If you'd like to test the full HTML documentation build locally, not on readthedocs, cd to the ```docs``` directory and run ```make html```.

### Readthedocs.org

The plaso documentation on [readthedocs.org](https://readthedocs.org/projects/plaso/) is mirrored off the [plaso wiki](https://github.com/log2timeline/plaso/wiki). The wiki git repo does not have the same webhooks as the plaso source git repo and thus we rely on a manual build trigger in the [merge_submit script](https://github.com/log2timeline/plaso/blob/master/utils/merge_submit.sh) to refresh the documentation.

The build of the [plaso-api documentation](https://readthedocs.org/projects/plaso-api/) is triggered by github service integration with readthedocs.

### Markdown compatibility

Define links as:
```
[description](URL)
```
Note that having a space between `]` and `(` breaks on readthedocs.

## Generating plaso wiki pages

Checkout the plaso wiki pages:
```
git clone https://github.com/log2timeline/plaso.wiki.git
```

To generate the [parser and plugins](https://github.com/log2timeline/plaso/wiki/Parsers-and-plugins) page:
```
PYTHONPATH=plaso plaso/tools/log2timeline.py --use-markdown --parsers list > plaso.wiki/Parsers-and-plugins.md
```

Commit and push the changes to the wiki pages.

## Creating a packaged release
### macOS packaged release

Use l2tdevtools to download the .dmg files:
```
PYTHONPATH=. ./tools/update.py --download-only
rm -f build/hachoir*.dmg
```

Change to the plaso source directory and create a distribution package by running:
```
./utils/prep_dist.sh
./config/macosx/make_dist.sh
```

This will create a file named: `plaso-${VERSION}_macosx-10.11.dmg` at the same level as the plaso source directory.

### PyPI

Set up `.pypirc` to have both `pypitest` and `pypi`. Also see: [How to submit a package to PyPI](http://peterdowns.com/posts/first-time-with-pypi.html)

Always first test changes on `pypitest` before making changes to `pypi`.

To register a project or update its metadata run:
```
python setup.py register -r pypitest
```

To upload a new release:
```
python setup.py sdist upload -r pypitest
```

The package on PyPI does not contain the test files due to size limitations.

To create a release package with test data for release on github.
```
python setup.py sdist_test_data
```

## Updating the plaso's image on Docker's Hub to the latest version in PPA

We have a repository on Docker's hub : [https://hub.docker.com/r/log2timeline/plaso](https://hub.docker.com/r/log2timeline/plaso).

```
cd config/docker/
docker build --no-cache -f plaso-from-ppa.dockerfile .
<... wait ... wait ...>
Successfully built f0edcb57611b
```
Your new image is `f0edcb57611b`. Make sure you've installed the version you want.
```
$ docker run -t -i  --entrypoint /bin/bash f0edcb57611b
root@a730e03d8386:/home/plaso# log2timeline.py --version
plaso - log2timeline version 1.5.1
```
Mark your new image with this version, and set it as being the latest.
```
docker tag d4c356705bd9 log2timeline/plaso:1.5.1
docker tag d4c356705bd9 log2timeline/plaso:latest
```
Then push the updates to Docker Hub.
```
docker login   # Ask log2timeline-maintainers@googlegroups.com for the credentials
docker push log2timeline/plaso:1.5.1
docker push log2timeline/plaso:latest
```

