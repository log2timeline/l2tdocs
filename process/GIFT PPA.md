The log2timeline projects distribute binary packages for Ubuntu via the
[GIFT PPA](https://launchpad.net/~gift).

### Set up your build environment

Install the following packages to set up your build environment:
```
apt-get install autoconf automake autopoint build-essential byacc debhelper devscripts dh-autoreconf dh-python dput flex git libtool pkg-config python3-all python3-all-dev python3-setuptools quilt
```

**Note that these package names are for Ubuntu 24.04 and can differ on other versions of Ubuntu/Debian**

Create a local copy of the latest l2tdevtools:
```
git clone https://github.com/log2timeline/l2tdevtools.git
```

Set up a build directory:
```
mkdir -p l2tbuilds/dpkg-source
```

Create: `l2tbuilds/dpkg-source/prep-dpkg-source.sh`

```
export NAME="Joachim Metz";
export EMAIL="joachim.metz@gmail.com";

PROJECT=$1;
VERSION=$2;
VERSION_SUFFIX=$3;
DISTRIBUTION=$4;
ARCHITECTURE=$5;

dch --preserve -v ${VERSION}-1${VERSION_SUFFIX}~${DISTRIBUTION} --distribution ${DISTRIBUTION} --urgency low "Modifications for PPA release."
```

Also see: https://github.com/log2timeline/l2tdevtools/wiki/Build-script#build-target-dpkg-source

Configure gpg to use gpg-agent otherwise you'll have to provide your password for every run of debuild:

```
cat >${HOME}/gpg-agent.conf <<EOT
default-cache-ttl 1800
max-cache-ttl 1800
EOT
```

```
cat >${HOME}/.gnupg/gpg.conf <<EOT
use-agent
EOT
```

`killall -q gpg-agent && gpg-agent --daemon`

### Building source dpkg files

To build source dpkg files use [l2tdevtools](https://github.com/log2timeline/l2tdevtools)
with build target: [dpkg-source](https://github.com/log2timeline/l2tdevtools/wiki/Build-script#build-target-dpkg-source).

```
cd l2tdevtools
PYTHONPATH=. tools/build.py --build-directory ../l2tbuilds/dpkg-source --preset plaso dpkg-source
```

#### Troubleshooting failed builds

You can build a source dpkg file manually with:
```
debuild -S -sa
```

### Uploading source dpkg files to the GIFT PPA

**Always upload to the testing track first**

To upload to the testing track of GIFT:
```
dput ppa:gift/testing ../l2tbuilds/dpkg-source/plaso_20251027-1ppa1~noble_source.changes
```

Also see: https://help.launchpad.net/Packaging/PPA/Uploading
