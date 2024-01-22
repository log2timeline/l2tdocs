## Adding a new dependency

There are several steps involved for getting a new dependency added.

### Before you begin checklist

If the answer on any of the questions below is "no" the dependency is not suitable for our use cases.

* Is the license of the dependency compatible with that of the project?

For the log2timeline projects this implies the license of the dependency should be compatible with [Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0). Code licensed under a GPL, AGPL or BSD 4-clause cannot be integrated in a binary build, hence these licenses are deemed incompatible. Note that this could also apply to other source code licenses.

* Does the dependency support the operating systems supported by the project?

For the log2timeline projects this implies the dependency should support Linux, Mac OS X and Windows.

### Automated testing

The automated testing relies on having the dependencies available. We deliberately limit the usage of pip (or equivalent) in the automated testing scripts, mainly because pip distributed builds change continuously and pip does not provide multiple distribution tracks. We want to have a more stable set of dependencies on dependencies and limit the amount of troubleshooting due breakage caused by a dependency.

#### Getting a dependency in l2tdevtools

We use [l2tdevtools](https://github.com/log2timeline/l2tdevtools) to limit the amount of manual effort required in maintaining dependencies.

If the build process of the dependency is similar enough what is currently supported then adding a new dependency should be relative straight forward by adding it to [data/projects.ini](https://github.com/log2timeline/l2tdevtools/blob/master/data/projects.ini). If not reach out to discuss how we can get support into l2tdevtools for the specific dependency.

Make sure the dependency is added to the [dependencies preset](https://github.com/log2timeline/l2tdevtools/blob/master/data/presets.ini) for [update.py](https://github.com/log2timeline/l2tdevtools/blob/master/tools/update.py).

#### Getting a dependency in GIFT COPR

Once the dependency has been added to l2tdevtools it can be added to the [GIFT COPR](https://copr.fedorainfracloud.org/groups/g/gift/coprs/).

Ask one of the [log2timeline maintainers](https://github.com/orgs/log2timeline/teams/log2timeline-maintainers/members) to upload your package.

#### Getting a dependency in GIFT PPA

Once the dependency has been added to l2tdevtools it can be added to the [GIFT PPA](https://launchpad.net/~gift).

Ask one of the [log2timeline maintainers](https://github.com/orgs/log2timeline/teams/log2timeline-maintainers/members) to upload your package.

#### Getting a dependency in l2tbinaries

Once the dependency has been added to l2tdevtools it can be added to [l2tbinaries](https://github.com/log2timeline/l2tbinaries).

Ask one of the [log2timeline maintainers](https://github.com/orgs/log2timeline/teams/log2timeline-maintainers/members) to upload your package.

### Source changes

Dependencies are defined in multiple different configuration files and scripts in the source tree. To keep them consistent we use l2tdevtools update-dependencies.py to generate these configuration files and scripts based on [dependencies.ini](https://github.com/log2timeline/plaso/blob/master/dependencies.ini).

```
PYTHONPATH=../l2tdevtools ../l2tdevtools/tools/update-dependencies.py
```
