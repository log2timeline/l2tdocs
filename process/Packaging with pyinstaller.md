To create a Windows packaged release from the development release you also need:

* PyInstaller

## PyInstaller

Download the latest source from:
```
git clone -b master git://github.com/pyinstaller/pyinstaller.git
```

**Note that setup.py build and install is currently disabled, so we need to run
PyInstaller from its download directory.**

### Rebuilding the PyInstaller bootloader

By default PyInstaller is code compatible with Windows XP SP2 (5.1). If you
need to support a Windows version earlier you'll need to recompile the
PyInstaller "bootloader" with Visual Studio 2008. Note that Visual Studio 2010
is not compatible with Windows 2000.

```
cd PyInstaller\bootloader
C:\Python27\python.exe waf configure build install
```

### Microsoft Visual C++ 2010 Redistributable Package

If you're building with Visual Studio note that for some reason PyInstaller
does not include the Microsoft Visual C++ 2010 run-time DLLs you can find them
here:

* [Microsoft Visual C++ 2010 Redistributable Package (x86)](http://www.microsoft.com/en-us/download/details.aspx?id=5555)
* [Microsoft Visual C++ 2010 Redistributable Package (x64)](http://www.microsoft.com/en-us/download/details.aspx?id=14632)

## Preparations

If you are intending to distribute the packaged release make sure to do the following steps:

`1`. Make sure the dependencies are up to date.

`2`. Remove code that cannot be redistributed due to a license restriction, by running:
```
sh utils/prep_dist.sh
```

**Note that you'll need to run this under Cygwin or equivalent.**

`3`. Distribute a copy of:
```
AUTHORS
ACKNOWLEDGEMENT
LICENSE
config\licenses\*
```

**Note that make_release.ps1 will handle steps 2 and 3.**

## Packaging

First check if the PyInstaller build script: config\windows\make_release.ps1 is
configured correctly for your build environment.

From the plaso source directory run the following commands:

Install dependencies with l2tdevtools:
```
PYTHONPATH=. tools\update.py
```

Build plaso with PyInstaller:
```
config\windows\make_release.ps1
```

This will create: `plaso-<version>-<architecture>.zip`

To do a very rudimentary test to see if the packaged binaries work run:
```
config\windows\make_check.bat
```

### Packaging win32 on amd64

```
PYTHONPATH=. tools\update.py --machine-type x86
```

```
config\windows\make_release.ps1 -Architecture win32
```
