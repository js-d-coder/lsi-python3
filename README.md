# lsi (a command-line utility)

`ls` command alternative (not a replacement). Output is either cleanly formatted table or string of null terminated file names parseable by xargs command. Default behaviour is to show only non-hidden files and directories of directory passed or current directory if no directory is given, in table format.  
It attempts to solve some problems with traditional UNIX ls command:

* Output is in table format and not garbled like in traditional UNIX `ls` command. (See screen shot below)
* File names is _single qouted_ to help distinguish files with spaces in their names. (See screen shot below)
* You can safely parse its output. (See explanation below)

Any improvement or feature addition request is most welcome. I will be adding more features myself in future.

Written in Python for UNIX like OS  
Requires Python version 3.3 or later  
Version 2

## Usage

```
lsi [-h] [-1 | -x] [-n | -i | -a] [-d | -f] [-s | -u | -t | -c | -z]
           [-r] [-v]
           [FILE [FILE ...]]

ls command alternative. Output is either cleanly formatted table or string of
null terminated file names parseable by xargs command. Default behaviour is to
show only non-hidden files and directories of directory passed or current
directory if no directory is given, in table format.

positional arguments:
  FILE                  space separated list of any numbers of files and/or
                        directories; if not given, current directory will be
                        assumed

optional arguments:
  -h, --help            show this help message and exit
  -1                    output on file per line
  -x, --xargs           output will be string of null terminated file names;
                        can be used as input to other commands like xargs;
                        absense of this option makes output to be a table,
                        which is default
  -n, --non-hidden      show files and/or directories with names that does not
                        start with a dot; this is default
  -i, --hidden          show files and/or directories with names starting with
                        a dot
  -a, --include-hidden  show all files and/or directories
  -d, --only-dir        show directories only and not regular file
  -f, --only-files      show only regular files and not directories
  -f, --only-files      show only regular files and not directories
  -s                    sort contents of given directories alphabetically in
                        ascending order; this is default
  -u                    sort contents of given directories by access time,
                        newest first
  -t                    sort contents of given directories by modification
                        time, newest first
  -c                    sort contents of given directories by time of last
                        modification of file status information, newest first
  -z                    sort contents of given directories by their size,
                        largest first, note this works well only with regular
                        files
  -r                    reverse order while sorting; can be used in conjuction
                        with option -s, -u, -t or -c; in absense of these
                        options, sort alphabetically in descending order
  -v, --version         output version information and exit
```

## Examples

    # show all non-hidden files and directories
    $ lsi
    'very-long-name3'  'very-long-name2'  'very-long-name1'  'long-name5'
    'long-name4'       'long-name3'       'long-name2'       'long-name1'
    'file15'           'file14'           'file13'           'file12'
    'file11'           'file10'           'file9'            'file8'
    'file7'            'file6'            'file5'            'file4'
    'file3'            'file2'            'file1'            'directory5/'
    'directory4/'      'directory3/'      'directory2/'      'directory1/'
    'dir15/'           'dir14/'           'dir13/'           'dir12/'
    'dir11/'           'dir10/'           'dir9/'            'dir8/'
    'dir7/'            'dir6/'            'dir5/'            'dir4/'
    'dir3/'            'dir2/'            'dir1/'

    # show all directories
    $ lsi -da
    '.hidden-dir5/'  '.hidden-dir4/'  '.hidden-dir3/'  '.hidden-dir2/'  '.hidden-dir1/'
    'hidden-files/'  'directory5/'    'directory4/'    'directory3/'    'directory2/'
    'directory1/'    'dir15/'         'dir14/'         'dir13/'         'dir12/'
    'dir11/'         'dir10/'         'dir9/'          'dir8/'          'dir7/'
    'dir6/'          'dir5/'          'dir4/'          'dir3/'          'dir2/'
    'dir1/'

[You should not parse the output of `ls` command,](https://mywiki.wooledge.org/ParsingLs) but **you can safely parse the output of `lsi`**

    # move all hidden files to hidden-files directory
    $ lsi -ifx | xargs -r0 mv -t hidden-files

## Requirement

lsi requires Python version 3 installed before you run it

    # apt install python3 # Ubuntu, Linux Mint, Debian
    # pacman -S python    # Arch Linux
    # yum install python3 # Fedora
    # pkg install python3 # \*BSD

## Installation

(For Ubuntu, Fedora, Linux Mint, Debian, Arch Linux and other Linux distributions; \*BSD and other UNIX like OS)

    $ git clone https://github.com/js-d-coder/lsi-python3.git
    $ cd lsi-python3
    # cp lsi /usr/local/bin/
    # chmod +x /usr/local/bin/lsi

## Screenshot (lsi vs ls)

![lsi output](https://i.imgur.com/oUyiq0j.png)

## License

[MIT](https://mit-license.org/)  
Copyright (c) 2018 js-d-coder (www.github.com/js-d-coder)

## Contributing

This project makes use of PEP8 code style. Linter used is pycodestyle.
NOTE: Only exception is max-line-length which is set to 120.
