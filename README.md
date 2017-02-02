# lsi
ls command alternative. Output is either cleanly formatted table or string of null terminated file names parseable by xargs command. Default behaviour is to show only non-hidden files (no directories) of directory passed or current directory if no directory is given in table format.

## Usage

     usage: lsi [-h] [-x] [-n | -i | -a] [-d | -w] [-v] [FILE [FILE ...]]
     
     ls command alternative. Output is either cleanly formatted table or string of
     null terminated file names parseable by xargs command. Default behaviour is to
     show only non-hidden files (no directories) of directory passed or current
     directory if no directory is given in table format.
     
     positional arguments:
       FILE                  space separated list of any numbers of files and/or
                             directories. If not given current directory will be
                             assumed
     
     optional arguments:
       -h, --help            show this help message and exit
       -x, --xargs           output will be string of null terminated file
                             names.Can be used as input to other commands like
                             xargs. Absense of this option makes output to be a
                             table, which is default
       -n, --non-hidden      show files (and directories with -w) with names that
                             does not start with a dot. This is default
       -i, --hidden          show files (and directories with -w) with names
                             starting with a dot
       -a, --include-hidden  show all files (and directories with -w), including
                             hidden ones
       -d, --only-dir        show directories only and not regular file
       -w, --include-dir     show directories along with files. Can be used with
                             option -n, -i or -a
       -v, --version         output version information and exit


## Examples

    $  lsi
    'file20'  'file19'  'file18'  'file17'  'file16'  'file15'  'file14'  'file13'  'file12'  
    'file11'  'file10'  'file9'   'file8'   'file7'   'file6'   'file5'   'file4'   'file3'   
    'file2'   'file1'   
    $  lsi -d
    'dir20/'  'dir19/'  'dir18/'  'dir17/'  'dir16/'  'dir15/'  'dir14/'  'dir13/'  'dir12/'  
    'dir11/'  'dir10/'  'dir9/'   'dir8/'   'dir7/'   'dir6/'   'dir5/'   'dir4/'   'dir3/'   
    'dir2/'   'dir1/'   
    $  lsi -w
    'file20'  'file19'  'file18'  'file17'  'file16'  'file15'  'file14'  'file13'  'file12'  
    'file11'  'file10'  'file9'   'file8'   'file7'   'file6'   'file5'   'file4'   'file3'   
    'file2'   'file1'   'dir20/'  'dir19/'  'dir18/'  'dir17/'  'dir16/'  'dir15/'  'dir14/'  
    'dir13/'  'dir12/'  'dir11/'  'dir10/'  'dir9/'   'dir8/'   'dir7/'   'dir6/'   'dir5/'   
    'dir4/'   'dir3/'   'dir2/'   'dir1/'  
    
[You should not parse the output of `ls` command, but **you can safely parse the output of `lsi`**](http://www.mywiki.wooledge.org/ParsingLs)

    $  lsi -x | xargs -r0 cat
