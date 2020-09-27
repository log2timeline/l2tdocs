This page contains information relevant to maintainers of the log2timeline
projects.

* [Mailing list](https://github.com/log2timeline/l2tdocs/blob/master/process/Maintainers%20guide.md#mailing-list)
* [Maintainer guidelines](https://github.com/log2timeline/l2tdocs/blob/master/process/Maintainers%20guide.md#maintainer-guidelines)
* [Maintainer tools](https://github.com/log2timeline/l2tdocs/blob/master/process/Maintainers%20guide.md#maintainer-tools)
* Generating Plaso test files
* Readthedocs.org and generating docs with sphinx-doc
* Creating a packaged release
  * [Fedora source rpm for GIFT COPR](https://github.com/log2timeline/l2tdocs/blob/master/process/GIFT%20COPR.md)
  * [Ubuntu source dpkg for GIFT PPA](https://github.com/log2timeline/l2tdocs/blob/master/process/GIFT%20PPA.md)
  * [PyPI](https://github.com/log2timeline/l2tdocs/blob/master/process/PyPI.md)
* [Updating Plaso's docker image](https://github.com/log2timeline/l2tdocs/blob/master/process/Maintainers%20guide.md#updating-the-plasos-image-on-dockers-hub-to-the-latest-version-in-ppa)

## Mailing list

Maintainers mailing list: log2timeline-maintainers@googlegroups.com

## Maintainer guidelines

* [Feature requests and bug reports](https://plaso.readthedocs.io/en/latest/sources/user/Feature-requests-and-bug-reports.html?highlight=Feature-requests-and-bug-reports)

## Generating Plaso test files

To generate `pinfo_test.json.plaso` and `psort_test.json.plaso` run the
following script:

```
./config/tests/generate_test_files.sh
```

## Readthedocs.org and generating docs with sphinx-doc

Plaso uses [sphinx](http://sphinx-doc.org/) to generate API documentation. The
Plaso configuration uses the [autodoc](http://sphinx-doc.org/ext/autodoc.html)
plugin for automatic documentation generation, and the [napoleon](http://sphinxcontrib-napoleon.readthedocs.org/en/latest/sphinxcontrib.napoleon.html)
plugin to read our "Google style" docstrings.

The configuration is stored in [docs/conf.py](https://github.com/log2timeline/plaso/blob/master/docs/conf.py).

The HTML documentation is built and stored with readthedocs.org.

A GitHub webhook triggers [sphinx-apidoc](http://sphinx-doc.org/man/sphinx-apidoc.html).
This will generate reStructured text (.rst) files which readthedocs will use to
generate HTML files (.html).

Note that to generate the API documentation readthedocs needs to `import` each
Python file. This will fail if it cannot import all dependencies, and it is not
possible to install native dependencies on readthedocs. The Sphinx configuration
tries to take care of this by automatically mocking the dependencies in
[dependencies.py](https://github.com/log2timeline/plaso/blob/master/plaso/dependencies.py)
but it may be necessary on occasion to add a dependency explicitly to the
sphinx config.

To test building the HTML file locally run:
```
tox -edocs
```

The generated documentation can be found in dist/docs

### Readthedocs Markdown compatibility

Define links as:

```
[description](URL)
```

Note that having a space between `]` and `(` breaks on readthedocs.

## Updating the Plaso's image on Docker's Hub to the latest version in PPA

We have a repository on Docker's hub: [https://hub.docker.com/r/log2timeline/plaso](https://hub.docker.com/r/log2timeline/plaso).

```
cd config/docker/
docker build --no-cache --force-rm -t log2timeline/plaso .
<... wait ... wait ...>
Successfully built f0edcb57611b
Successfully tagged log2timeline/plaso:latest
```

Your new image is `f0edcb57611b`.

If the output also states:

```
Successfully tagged log2timeline/plaso:latest
```

Your new image was tagged as `log2timeline/plaso:latest`.

```
$ docker run log2timeline/plaso log2timeline --version
plaso - log2timeline version 20180930
```

Mark your new image with this version, and set it as being the latest.

```
docker tag f0edcb57611b log2timeline/plaso:20180930
docker tag f0edcb57611b log2timeline/plaso:latest
```

Then push the updates to Docker Hub.

```
docker login   # Ask log2timeline-maintainers@googlegroups.com for the credentials
docker push log2timeline/plaso:20180930
docker push log2timeline/plaso:latest
```
