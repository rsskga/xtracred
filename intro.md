# Intro to system & environment maintenance

* hardware
  * main memory = storage for 0s and 1s
    * each 0 or 1 = bit
    * all input/output from peripheral devices flows through main memory
    * state = particular arrangement of bits
    * image = a particular physical arrangement of bits
  * processor (CPU)
    * operates i/o on memory
  * disks
  * network interfaces/ports
* kernel = big collection of bits
  * core of the operating system
  * software residing in memory that instructs the CPU
  * manages hardware - interfaces between the hardware and running programs
  * runs in `kernel mode`
  * unrestricted access to `kernel space` (CPU and RAM)
  * parts
  *  process management
    * sets which processes are allowed to use CPU
    * handles starting, pausing, resuming, terminating processes
    * handles context switching amongst cores and processes
    * multitasking appears as simultaneous running processes
    * actually, time slices
  * memory management
    * which is allocated, shared, and free
    * quarantines memory space for itself
    * allocates to each process
    * shares amongst processes except for private memory
    * memory management unit (MMU) enables virtual memory
  * device drivers
  * system calls a.k.a. syscalls
    * perform specific tasks that a user process alone cannot
      * i.e., opening, reading, and writing files
      * fork()
      * exec(program)
* (user) processes = big collection of bits
  * runs in `user mode`
  * access restricted to `user space` (safe CPU ops and a subset of RAM)
  * parts
    * graphical user interface (GUI)
    * servers
    * shell
  * groups
    * sets of users with common file access and permissions
  * users
    * root = superuser with unlimited permissions
      * with great power comes great responsibility
      * use with caution and only when absolutely necessary
    * root access = administrator who can operate as root

# CLI - Useful Commands

## Unix/Linux
* keyboard shortcuts
  * `q` (quit or exit)
  * `cmd+k` or `clear` (clear shell screen)
* navigation & orientation
  * `pwd` (print working directory = where am i?)
  * `open .` (open working directory in finder)
  * `whoami` (which user am i logged in as?)
  * `cd` (change directory)
  * `cd ..` (go up to parent directory)
  * `cd ~` (go to users home directory)
  * `cd /` (go to root directory)
  * `cd -` (go to previous location)
  * `cd /Users/rainagustafson` (absolute path example)
  * `cd Users/rainagustafson` (relative path example)
  * `ls` (list contents of current directory)
  * `ls -la` (list contents of current directory including invisibles)
* working with applications
  * `echo $PATH` (print the PATH var = known locations of executables)
  * `man open` (show documentation)
  * `which conda` (location of executable)
  * `conda --version` (print version - this flag varies by application)
* working with files & streams
  * `mkdir project` (create a directory called 'project')
  * `touch file.txt` (create a file called 'file.txt')
  * `cat file.txt` (print file contents)
  * `mv file.txt project` (move file to project directory)
  * `cp project/file.txt .` (copy from project to working directory)
  * `diff file.txt project/file.txt` (compare two files)
  * `rm file.txt` (delete 'file.txt')
  * `rm -rf project` (delete 'project' directory)
* working with permissions
  * chmod
* misc
  * symlinks
* `pipenv install twine` vs. `pipenv install -d twine`

> TODO: Amer, put these in any order you like
## Windows
* help
* where
* cd / chdir
* dir
* mkdir
* copy
* move
* del
* cd
* ren file or folder
* cls
* $APP --version
* rmdir myFolder
* more thisfile.txt
* echo some-text > fileName(.txt)
* fc

# Future Lessons

* More commands & shell text editors
* More on Github work flows
  * [Code review](https://github.com/features/code-review/)
  * Branch management
  * Git hooks
* SQL
  * TablePlus alternative
* Docker
