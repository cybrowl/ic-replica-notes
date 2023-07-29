This page contain a list of prerequisites for building the ic replica as well as links to helpful information about how to install the apps. You can build the ic replica on Mac, Linux, or WSL2 (Windows)

# Minimum PC Specifications:

x86-64 based system 8 CPU cores
16 GB MEM
100 GB available disk space

## Software

- Git
- Podman

## Repo

- ic replica

## CodeGov script

Create a directory and file called:
~/codegov/codegov.sh

This codegov.sh file should contain the line:

```
echo -n "$1:$2" | sha256sum | sed -e "s/-/DSCVR username: $1   Replica version: $2/"
```

When you run the IC-OS Verification script, make sure to include this command at the end of the script:

```
bash ~/codegov/codegov.sh <DSCVR Username> <Replica Version>
```

## IC-OS Verification

The script below is usually included in each Bless Replica Version proposal, but it is included here for convenience. This version includes the required CodeGov script. Make sure to substitute relevant information for <Replica_Version> and <DSCVR_Username> before you run the script in your command line terminal. Also, the script sometimes changes between what you see here and what may be present in the proposal, so pay attention to the details. For example, if the update-img.tar.gz file is not found in the artifacts folder, then check to see if the file path is correct.

# From https://github.com/dfinity/ic#building-the-code

# Instructions

```
git clone https://github.com/dfinity/ic

cd ic

git fetch origin

git checkout <Replica_Version>

if ./gitlab-ci/container/build-ic.sh -i ; then

    curl -LO https://download.dfinity.systems/ic/<Replica_Version>/guest-os/update-img/update-img.tar.gz

    shasum -a 256 artifacts/icos/update-img.tar.gz update-img.tar.gz

else

    echo "IC-OS build failed. Verification unsuccessful." >&2

fi

bash ~/codegov/codegov.sh <DSCVR_Username> <Replica_Version>
```
