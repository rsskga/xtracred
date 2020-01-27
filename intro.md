# Intro to system and development environment maintenance

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
* man
* which
* whoami
* pwd
* $APP --version
* echo
* cat
* ls
* cp
* mv
* touch
* rm
* cd
* mkdir
* clear / cmd+k
* diff
* open
* symlinks
* chmod

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

