# Comparison table13 and RPM/DEB/PIP

Compares output of various package managers (RPM, DEB, PIP) with OIN table 13
and prints which packages are missing with some metadata. This script has been
kept as simple as possible regarding dependencies so it can run on a wide range
of systems. The script does not have to run on the same machine as on which the
output of the package managers was generated.

## RPM

First run `rpm -qia` on the target system and redirect the output to a file,
for example:

```
$ rpm -qia > /tmp/rpm
```

Then copy the file to the system running the script and run:

```
$ python package_nominations.py -l /tmp/rpm -c table-13_2026-02-25.csv -t rpm
```

It might be needed to adapt paths to point to the right locations.

## DEB

```
$ apt list --installed  | cut -f 1 -d / | xargs -I% apt show % > /tmp/deb
```

```
$ python package_nominations.py -l /tmp/deb -c table-13_2026-02-25.csv -t deb
```

## Python pip

```
$ pip list | tail -n +3 | cut -f 1 -d " " | xargs -I% pip show % > /tmp/pip
```

```
$ python package_nominations.py -l /tmp/pip -c table-13_2026-02-25.csv -t pip
```


## Shortcomings

Some packages have been renamed (example: `pcre2`) so those are "false
positives". In the script there is a list of aliases.
