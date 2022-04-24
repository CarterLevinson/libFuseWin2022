# libFuseWin2022

# ntapfuse

ntapfuse is a FUSE filesystem that mirrors a directory.

## Dependencies

The following packages need to be installed using:

```bash
  $ sudo apt-get install <pkg-name>
```

* fuse
* libfuse-dev
* sqlite3
* libsqlite3-dev
* python3
* python3-pip

Please ensure that the version of python installed is >= 3.6.
Further please ensure that you have installed the pytest package:

Also be sure that the version of sqlite3 is >= 3.24
```bash
  $ pip install pytest
```

Alternatively, you can cd into the test directory and run the following
command:

```bash
  $ pip install -r requirements.txt
```

## Installation
You need to run the following commands to install ntapfuse:
```bash
  $ autoreconf --install
  $ ./configure
  $ sudo make install
  $ sudo chmod u+s /usr/local/bin/ntapfuse
```

## Configuration

In order for the test program to run correctly, please make the following
changes to your /etc/fuse.conf by uncommenting the "user_allow_other" option.

If you do not want your filesystem to work for multiple users, you can 
ensure it runs correctly by using the single user test-suite as described in 
the testing section.




## Usage
  
ntapfuse requires a base directory to be mirroed and a mount point:

```bash
  $ ntapfuse mount <base> <mount>
```

if you want to allow multiple users for the FUSE session and have set the 
option as described above, run:

```bash
  $ ntapfuse mount <base> <mount> -o allow_other
```

ntapfuse should be unmounted using the fusermount command to avoid transport
socket errors, like so:

```bash
  $ fusermount -u <mount>
```

## Testing

you can run the testing script from the repository root by typing 

```bash
  $ ./test/test.sh 
```

into your shell prompt. a copy of the database file in addition to the results
of the tests will be written to the test directory upon completion.

the script will do the instalttion and modification of the ntapfuse binary for
you, but please make sure you have at least created the auto tools files and ran
the configuration script before running the test script, as it assumes the Makefile 
already exists
