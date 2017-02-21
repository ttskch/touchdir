# touchdir

A CLI tool to update timestamp of directories to the same timestamp of the newest file in the directory recursively.

## Requirements

* PHP 5.4+

## Installation

```sh
$ git clone git@github.com:ttskch/touchdir.git
$ cd touchdir
$ composer install
$ chmod +x touchdir
$ ln -s $(pwd)/touchdir /usr/local/bin/
```

## Usage

```sh
$ touchdir -h
Usage:
  touchdir [options] [--] <dir>

Arguments:
  dir                   Target directory

Options:
  -N, --dry-run         Show what would be updated without actual updating
  -h, --help            Display this help message
  -q, --quiet           Do not output any message
  -V, --version         Display this application version
      --ansi            Force ANSI output
      --no-ansi         Disable ANSI output
  -n, --no-interaction  Do not ask any interactive question
  -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug

Help:
  Update timestamp of directories to the same timestamp of the newest file in the directory recursively
```

## Example

If you have a directory like following:

```sh
$ tree -D
.
├── [Feb 20  0:00]  dir1            # <- will be touched to 'Feb 12 12:00
│   ├── [Feb 20  0:00]  dir2        # <- will be touched to 'Feb 11 20:00
│   │   ├── [Feb 10  0:00]  file3   #
│   │   └── [Feb 11 20:00]  file4   # <- newest in dir2
│   ├── [Feb 12  0:00]  file1       #
│   └── [Feb 12 12:00]  file2       # <- newest in dir1
└── [Feb 20  0:00]  dir3            # <- will be touched to 'Feb 11 20:00
    └── [Feb 11 20:00]  file5       # <- newest in dir3

3 directories, 5 files

```

Then `touchdir` updates timestamps of 3 directories as below: 

```sh
$ touchdir .
 ./dir1/dir2 2017-02-11 20:00:00
 ./dir1      2017-02-12 12:00:00
 ./dir3      2017-02-11 20:00:00
```

Enjoy :smiley:
