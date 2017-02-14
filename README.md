# lsi
ls command alternative. Output is either cleanly formatted table or string of null terminated file names parseable by xargs command. Default behaviour is to show only non-hidden files and directories of directory passed or current directory if no directory is given, in table format.  
Written in Python version 3 for UNIX like OS  
Version 1.1.0  

## Usage

    usage: lsi [-h] [-t | -1 | -x] [-n | -i | -a] [-d | -f] [-v] [FILE [FILE ...]]

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
      -t                    output in table format; this is default
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
      -v, --version         output version information and exit


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


[You should not parse the output of `ls` command,](http://www.mywiki.wooledge.org/ParsingLs) but **you can safely parse the output of `lsi`**

    # move all hidden files to hidden-files directory
    $ lsi -ifx | xargs -r0 mv -t hidden-files
