# Unix / Linux / OS — Final Complete Theory

## 1. Operating System

An **Operating System (OS)** is system software that acts as an interface between applications/users and computer hardware.

### Main responsibilities

* Process management
* CPU scheduling
* Memory management
* File-system management
* Device management
* Networking
* Security

**Simple example:**
A Python program cannot normally directly control the disk. It requests the operating system to perform the operation.

---

# 2. Unix

**Unix** is a family of multi-user, multitasking operating systems originally developed at Bell Labs around 1969.

Important contributors include **Ken Thompson** and **Dennis Ritchie**.

### Characteristics

* Multi-user
* Multitasking
* Portable
* Secure permission system
* Hierarchical filesystem
* Shell-based interaction
* Strong networking capabilities

**Reviewer answer:**

> Unix is a multi-user, multitasking operating-system family designed around portability, security, and powerful command-line tools.

---

# 3. Linux

Linux is an **open-source, Unix-like kernel**.

A complete Linux operating system is normally provided as a **Linux distribution**, which combines the Linux kernel with system libraries, utilities, services, package-management tools, and applications.

Examples:

* Ubuntu
* Debian
* Fedora
* Arch Linux

---

# 4. Unix vs Linux

| Unix                                      | Linux                             |
| ----------------------------------------- | --------------------------------- |
| Unix is an operating-system family        | Linux is a Unix-like kernel       |
| Originated at Bell Labs                   | Created by Linus Torvalds in 1991 |
| Many Unix implementations are proprietary | Linux kernel is open-source       |
| Older operating-system family             | Modern Unix-like kernel           |

---

# 5. Linux Distribution

A **Linux distribution** is a complete operating system built around the Linux kernel.

It normally contains:

* Linux kernel
* System libraries
* Utilities
* Package manager
* Services
* Configuration tools
* Applications

**Example:**

> Ubuntu is a Linux distribution. Linux is the kernel.

---

# 6. Kernel

The **kernel** is the core part of an operating system responsible for managing hardware and system resources.

### Main roles

1. Process management
2. CPU scheduling
3. Memory management
4. File-system management
5. Device management
6. Networking
7. Security
8. System calls
9. Inter-process communication

**Simple example:**

A program requests memory → kernel manages the request → appropriate memory is provided.

---

# 7. Types of Kernels

## 7.1 Monolithic Kernel

Most operating-system services run in kernel space.

### Advantages

* High performance
* Direct communication between kernel components

### Disadvantage

A serious failure in kernel-level code can affect the whole system.

**Linux:** generally classified as a monolithic kernel with loadable modular support.

---

## 7.2 Microkernel

Only essential functionality runs in kernel space. Many other services run in user space.

### Advantages

* Better isolation
* Smaller kernel
* Fault isolation can be improved

### Disadvantage

Communication between components can introduce overhead.

---

## 7.3 Hybrid Kernel

A hybrid kernel combines design ideas from monolithic and microkernel architectures.

---

# 8. User Space

**User space** is the environment where normal applications execute.

Examples:

* Python programs
* Browsers
* Editors
* Shells

Applications normally cannot directly access protected kernel memory or hardware.

---

# 9. Kernel Space

**Kernel space** is the privileged environment where the kernel and kernel-level components execute.

Kernel space has access to critical system resources.

### User Space vs Kernel Space

**User space:**

> Normal applications execute here with restricted privileges.

**Kernel space:**

> The kernel executes here with privileged access to system resources.

---

# 10. Shell

A **shell** is a command interpreter that allows users to interact with the operating system.

The shell:

1. Receives input
2. Interprets it
3. Starts programs or performs shell operations
4. Displays results

**Simple flow:**

```text
User → Shell → Kernel → Hardware
```

---

# 11. Bash

**Bash** means **Bourne Again SHell**.

It is a widely used Unix/Linux shell.

It supports:

* Commands
* Variables
* Conditions
* Loops
* Functions
* Scripts
* Pipes
* Redirection

---

# 12. Types of Unix/Linux Shells

Common shells include:

* sh
* bash
* zsh
* ksh
* csh
* tcsh
* fish

---

# 13. Bash vs sh

### sh

Traditional Unix shell interface and shell language standard.

### Bash

A more feature-rich shell from the Bourne shell family that supports much of traditional `sh` syntax.

**Reviewer answer:**

> `sh` represents the traditional Bourne-shell interface, while Bash is a more feature-rich shell derived from that family.

---

# 14. Terminal

A **terminal** is an interface through which a user interacts with a shell.

Important distinction:

> Terminal provides the interface; shell interprets commands.

---

# 15. CLI

CLI means **Command Line Interface**.

It allows users to interact with a system using text commands.

### Advantages

* Fast
* Powerful
* Scriptable
* Easy to automate
* Low graphical overhead

---

# 16. GUI

GUI means **Graphical User Interface**.

It allows users to interact through:

* Windows
* Buttons
* Menus
* Icons
* Mouse

### CLI vs GUI

**CLI:** text-based interaction.

**GUI:** graphical interaction.

---

# 17. Unix/Linux Architecture

A simplified architecture is:

```text
User
 ↓
Applications
 ↓
Shell / Libraries
 ↓
System Calls
 ↓
Kernel
 ↓
Hardware
```

---

# 18. Unix Philosophy

Unix follows the philosophy of creating small, focused tools that can be combined.

Important ideas:

* Do one thing well
* Build reusable tools
* Combine tools
* Use text as a common interface
* Automate repetitive work

Pipes are an important example of this philosophy.

---

# 19. POSIX

POSIX means **Portable Operating System Interface**.

It defines standardized interfaces and behaviors for Unix-like systems.

### Purpose

To improve compatibility and portability of applications and scripts between Unix-like operating systems.

---

# 20. Filesystem

A filesystem organizes and stores files and directories.

Linux uses a **hierarchical filesystem**.

The top-level directory is:

```text
/
```

This is called the **root directory**.

---

# 21. Important Linux Directories

### `/`

Root of the filesystem.

### `/home`

Home directories of normal users.

### `/root`

Home directory of the root user.

### `/etc`

System configuration files.

### `/var`

Variable data such as logs and application data.

### `/tmp`

Temporary files.

### `/boot`

Boot-related files.

### `/dev`

Device interfaces.

### `/proc`

Virtual filesystem containing process and kernel information.

### `/sys`

Virtual filesystem exposing information about devices and the kernel.

### `/usr`

User-space programs, libraries, and shared data.

### `/bin`

Essential commands. On many modern systems this is integrated with `/usr/bin`.

### `/sbin`

Traditionally system-administration commands. On many modern systems this is integrated with `/usr/bin`.

---

# 22. System Files

Important system configuration files include:

### `/etc/passwd`

Basic user account information.

### `/etc/shadow`

Password hashes and password-related account information.

### `/etc/group`

Group information.

### `/etc/sudoers`

Rules controlling sudo privileges.

### `/etc/hosts`

Local hostname-to-address mappings.

### `/etc/fstab`

Filesystem mount configuration.

---

# 23. Absolute Path

An **absolute path** gives the complete location of a file or directory starting from the filesystem root.

Example:

```text
/home/user/project/app.py
```

It does not depend on the current directory.

---

# 24. Relative Path

A **relative path** describes a location relative to the current working directory.

Example:

```text
project/app.py
```

### Difference

**Absolute path:**

> Starts from `/`.

**Relative path:**

> Starts from the current directory.

---

# 25. File Types

Common Unix/Linux file types include:

* Regular file
* Directory
* Symbolic link
* Character device
* Block device
* Socket
* FIFO/named pipe

---

# 26. Inode

An **inode** is a filesystem data structure containing metadata about a file.

It can contain information such as:

* File type
* Permissions
* Owner
* Group
* File size
* Timestamps
* References to the file's data blocks

The filename itself is stored in a directory entry that references the inode.

---

# 27. Hard Link

A **hard link** is another directory entry referring to the same inode.

Therefore, multiple filenames can refer to the same underlying file.

If one filename is deleted, the data can still exist as long as another hard link references the inode.

---

# 28. Symbolic / Soft Link

A **symbolic link** is a separate filesystem object that stores a pathname referring to another file or directory.

It behaves somewhat like a shortcut.

---

# 29. Hard Link vs Soft Link

| Hard Link                                 | Soft Link                              |
| ----------------------------------------- | -------------------------------------- |
| Refers to same inode                      | Refers to a pathname                   |
| Same underlying file                      | Separate filesystem object             |
| Usually cannot cross filesystems          | Can cross filesystems                  |
| Usually cannot reference directories      | Can reference directories              |
| Can survive deletion of original filename | Can become broken if target disappears |

---

# 30. File Permissions

Linux uses permissions to control access to files and directories.

There are three categories:

* Owner
* Group
* Others

There are three basic permissions:

* Read
* Write
* Execute

---

# 31. File Permissions Meaning

### Regular files

**Read:** view contents.

**Write:** modify contents.

**Execute:** execute the file as a program, assuming other requirements are satisfied.

### Directories

**Read:** list directory entries.

**Write:** create/delete/rename directory entries, subject to other required permissions.

**Execute:** enter/traverse the directory and access entries when permitted.

---

# 32. Numeric Permissions

Permission values are:

```text
Read    = 4
Write   = 2
Execute = 1
```

Examples:

```text
7 = rwx
6 = rw-
5 = r-x
4 = r--
```

### 755

```text
Owner  → rwx
Group  → r-x
Others → r-x
```

---

# 33. chmod

`chmod` changes file or directory permissions.

**Reviewer answer:**

> chmod changes what permissions users have on a file or directory.

---

# 34. chown

`chown` changes ownership.

It can change:

* Owner
* Group ownership

---

# 35. chmod vs chown

**chmod:**

> Changes permissions.

**chown:**

> Changes ownership.

Easy memory:

> **chmod = what can you do?**

> **chown = who owns it?**

---

# 36. sudo

`sudo` allows an authorized user to execute a command with another user's privileges, commonly root privileges.

It supports the principle of least privilege because elevated privileges can be given only when needed.

---

# 37. su

`su` means **substitute user**.

It changes the effective user identity for a shell/session or command context.

It is commonly used to switch to another user, including root.

---

# 38. sudo vs su

**sudo:**

> Run a particular operation with another user's privileges.

**su:**

> Switch to another user identity/session.

---

# 39. Root User

The **root user** is the Unix/Linux superuser.

Root has extensive privileges over the system.

It can:

* Modify system files
* Manage users
* Change permissions
* Manage services
* Access protected resources

Because root has extensive power, unnecessary root access should be avoided.

---

# 40. umask

`umask` is the **user file-creation permission mask**.

It removes permission bits from the default permissions used when new files and directories are created.

Typical base modes:

```text
Files       → 666
Directories → 777
```

For a common umask of `022`:

```text
Files       → 644
Directories → 755
```

### Important

> umask does not directly assign the final permissions. It masks/removes permissions from the default creation mode.

---

# 41. Program

A **program** is a passive set of instructions stored on storage.

Example:

```text
calculator.py
```

is a program.

It does nothing until executed.

---

# 42. Process

A **process** is an instance of a program that is currently executing.

A process has resources such as:

* PID
* Memory
* CPU state
* File descriptors
* Environment
* Security credentials

---

# 43. Program vs Process

**Program:**

> Passive instructions.

**Process:**

> Active execution of those instructions.

### Analogy

Recipe = program.

Person actually cooking = process.

---

# 44. PID

PID means **Process ID**.

It is an identifier assigned to a process by the operating system.

---

# 45. PPID

PPID means **Parent Process ID**.

It identifies the parent process associated with a process.

---

# 46. Process States

Common process states include:

* Running
* Runnable/ready
* Sleeping/waiting
* Stopped
* Zombie

Exact state representations depend on the operating system.

---

# 47. Foreground Process

A foreground process is associated with the current terminal interaction.

The shell normally waits for the foreground job to finish before accepting another command.

---

# 48. Background Process

A background process runs without occupying the foreground interaction of the terminal.

This allows the user to continue interacting with the shell.

---

# 49. Backgrounding a Process

Backgrounding means allowing a process/job to continue running while the shell remains available for other work.

---

# 50. Signals

A **signal** is a software notification delivered to a process or thread to indicate an event or request an action.

Important signals include:

### SIGINT

Usually requests interruption, commonly associated with Ctrl+C.

### SIGTERM

Requests graceful termination.

### SIGKILL

Forces termination and cannot be caught, blocked, or ignored.

### SIGHUP

Historically indicates a terminal hangup; programs may assign additional behavior to it.

### SIGSTOP

Stops execution and cannot be caught or ignored.

### SIGCONT

Continues a stopped process.

---

# 51. SIGTERM vs SIGKILL

**SIGTERM:**

> "Please terminate gracefully."

The application can handle it and perform cleanup.

**SIGKILL:**

> "Terminate immediately."

The application cannot catch or handle it.

---

# 52. Exit Code

An **exit code** is a numeric status returned by a process when it terminates.

Conventionally:

```text
0       → success
non-zero → failure or another condition
```

The exact meaning of a non-zero value depends on the program.

---

# 53. Zombie Process

A **zombie process** is a child process that has finished execution but whose parent has not yet collected its termination status.

It does not continue normal execution but retains a process-table entry.

---

# 54. Orphan Process

An **orphan process** is a still-running child process whose original parent has terminated.

The operating system reparents it so it can continue to be managed.

### Zombie vs Orphan

**Zombie:**

> Finished child waiting for its status to be collected.

**Orphan:**

> Running child whose original parent has terminated.

---

# 55. Process Scheduling

**Process scheduling** is the mechanism used by the operating system to decide which runnable execution entity receives CPU time.

The kernel scheduler considers factors such as:

* Priority
* Scheduling policy
* Fairness
* CPU availability
* Process/thread state

---

# 56. Kernel-Space Scheduling

Kernel-space scheduling is scheduling performed by the **kernel scheduler**.

The kernel decides which kernel-schedulable execution entity, typically a thread, gets CPU time.

### Example

```text
Thread A ─┐
Thread B ─┤
Thread C ─┼──→ Kernel Scheduler ──→ CPU
Thread D ─┤
Thread E ─┘
```

### Reviewer answer

> Kernel-space scheduling is CPU scheduling performed by the operating-system kernel to decide which runnable processes or threads receive CPU time.

---

# 57. User-Space Scheduling

**User-space scheduling** is scheduling performed by a user-level runtime, library, or application.

It can manage higher-level tasks such as:

* User-level threads
* Green threads
* Coroutines
* Runtime-managed tasks

For example:

```text
Kernel Scheduler
       ↓
    Process
       ↓
User-space Runtime
   ↓    ↓    ↓
 Task A Task B Task C
```

The runtime decides which internal task should execute, while the kernel ultimately controls CPU allocation to kernel-schedulable threads.

### Important

User-space scheduling does **not** replace kernel CPU scheduling.

### Reviewer answer

> User-space scheduling is scheduling performed by a runtime or library to manage its own higher-level tasks, such as coroutines or user-level threads.

---

# 58. Kernel-Space vs User-Space Scheduling

| Kernel-Space Scheduling            | User-Space Scheduling                    |
| ---------------------------------- | ---------------------------------------- |
| Performed by kernel                | Performed by runtime/library/application |
| Controls CPU scheduling            | Manages higher-level tasks               |
| Schedules kernel-visible entities  | Schedules user-level tasks               |
| Uses OS scheduling policies        | Uses application/runtime logic           |
| Ultimately controls CPU allocation | Operates within CPU time available to it |

### Easy memory

> **Kernel scheduler → Who gets CPU time?**

> **User-space scheduler → Which internal task should use that execution opportunity?**

---

# 59. Process Priority / Niceness

Niceness influences scheduling priority in Unix/Linux scheduling.

Generally:

> Higher niceness = lower scheduling preference.

It allows processes to be given different scheduling priorities.

---

# 60. File Descriptor

A **file descriptor** is a small integer used by a process to refer to an open file or I/O resource.

Standard descriptors are:

```text
0 → stdin
1 → stdout
2 → stderr
```

---

# 61. stdin

**stdin** means Standard Input.

It is the default input stream of a process.

---

# 62. stdout

**stdout** means Standard Output.

It is the normal output stream of a process.

---

# 63. stderr

**stderr** means Standard Error.

It is normally used for errors and diagnostic messages.

### stdout vs stderr

**stdout:**

> Normal program output.

**stderr:**

> Error and diagnostic output.

They are separate streams so they can be handled independently.

---

# 64. Piping

A **pipe** connects the output of one process to the input of another.

Conceptually:

```text
Process A
   ↓ stdout
  Pipe
   ↓ stdin
Process B
```

This allows small Unix tools to be combined.

---

# 65. Redirection

**Redirection** changes where standard input, output, or error comes from or goes to.

For example:

* Input can come from a file.
* Output can go to a file.
* Errors can be separated from normal output.

---

# 66. grep

`grep` is a text-search utility.

It searches input for lines matching a specified pattern.

**Reviewer answer:**

> grep searches text for lines that match a pattern.

---

# 67. find

`find` searches the filesystem for files and directories based on conditions.

Conditions can include:

* Name
* Type
* Size
* Time
* Permissions

### grep vs find

**grep:**

> Searches text/content.

**find:**

> Searches filesystem objects.

---

# 68. Shell Variables

A shell variable stores a value that can be used by the shell.

Variables may contain:

* Strings
* Numbers
* Paths
* Configuration values

---

# 69. Environment Variables

Environment variables are variables provided through a process's environment.

Examples:

* PATH
* HOME
* USER

Child processes normally inherit the environment of their parent.

---

# 70. PATH

`PATH` is an environment variable containing directories in which the shell searches for executable programs.

It allows users to execute programs without specifying their complete path when the program is located in one of those directories.

---

# 71. Shell Script

A shell script is a file containing shell commands and shell logic.

It can contain:

* Variables
* Conditions
* Loops
* Functions
* Commands

### Purpose

Automation of repetitive tasks.

---

# 72. Command-Line Arguments

Command-line arguments are values passed to a program when it starts.

They allow the same program to receive different inputs without changing its source code.

---

# 73. System Call

A **system call** is the controlled interface through which a user-space program requests a service from the kernel.

Examples:

* File operations
* Process creation
* Memory operations
* Networking

### Flow

```text
Application
    ↓
System Call
    ↓
Kernel
    ↓
Hardware / Resource
```

---

# 74. fork()

`fork()` creates a new process based on the calling process.

The new process is called the child process.

---

# 75. exec()

The `exec` family replaces the current process's program image with another program.

A common process-creation pattern is:

```text
fork()
   ↓
Child process
   ↓
exec()
   ↓
New program
```

The process identity remains associated with that execution context while its program image is replaced.

---

# 76. Memory Management

Memory management is the kernel's responsibility for managing memory resources.

It includes:

* Allocation
* Deallocation
* Memory protection
* Virtual memory
* Address translation
* Process isolation

---

# 77. Virtual Memory

Virtual memory gives processes their own virtual address spaces.

It provides:

* Process isolation
* Memory protection
* Efficient memory management
* The ability to use storage as backing memory when necessary

---

# 78. Paging

Paging divides virtual memory into fixed-size **pages** and physical memory into **frames**.

The operating system maps virtual pages to physical frames.

---

# 79. Swap

Swap is storage space that can be used as backing for memory pages when physical RAM is under pressure.

Storage is much slower than RAM.

---

# 80. IPC

IPC means **Inter-Process Communication**.

It allows processes to communicate and synchronize.

Common IPC mechanisms:

* Pipes
* FIFOs
* Shared memory
* Message queues
* Semaphores
* Signals
* Sockets

---

# 81. Shared Memory

Shared memory allows multiple processes to access a common memory region.

It can be very fast because processes can communicate through shared data.

However, synchronization is necessary to avoid race conditions.

---

# 82. Message Queue

A message queue allows processes to communicate by sending and receiving messages.

Messages can be stored temporarily until another process receives them.

---

# 83. Semaphore

A semaphore is a synchronization mechanism used to control access to shared resources.

It helps coordinate concurrent processes or threads.

---

# 84. Socket

A socket is an endpoint used for communication.

Sockets can be used for:

* Local process communication
* Network communication

---

# 85. Networking

Networking allows computers and processes to communicate.

Important concepts include:

* IP address
* MAC address
* Port
* TCP
* UDP
* DNS
* Routing
* Gateway
* Firewall

---

# 86. IP Address

An IP address identifies a network-layer address associated with a network interface.

Examples:

```text
IPv4 → 192.168.1.10
IPv6 → 2001:db8::1
```

---

# 87. MAC Address

A MAC address is a link-layer address associated with a network interface.

It is commonly used for communication on local networks such as Ethernet.

---

# 88. Port

A port identifies a logical endpoint for network communication.

Examples:

```text
HTTP  → 80
HTTPS → 443
SSH   → 22
```

---

# 89. TCP

TCP is a connection-oriented transport protocol.

It provides:

* Reliable delivery
* Ordered data
* Retransmission
* Flow control
* Congestion control

---

# 90. UDP

UDP is a connectionless transport protocol.

It has lower overhead than TCP but does not provide TCP's guarantees of reliable, ordered delivery.

---

# 91. DNS

DNS means **Domain Name System**.

It translates domain names into IP addresses and provides other types of DNS information.

Example:

```text
example.com
     ↓
IP address
```

---

# 92. Ping

Ping checks basic IP-level reachability using ICMP Echo messages for IPv4 or ICMPv6 Echo messages for IPv6.

It can provide:

* Reachability information
* Round-trip time

### Important

Successful ping does not prove that a particular TCP or UDP service is working.

---

# 93. SSH

SSH means **Secure Shell**.

It is a secure protocol used for:

* Remote login
* Remote command execution
* Secure tunneling
* Secure communication

The default SSH port is **TCP 22**.

---

# 94. SSH Authentication

SSH can authenticate users using different methods.

### Password authentication

The user provides a password.

### Public-key authentication

The client has a private key and the server has the corresponding public key.

The private key must be kept secret.

---

# 95. SCP

SCP traditionally means **Secure Copy**.

It is used to securely transfer files between systems through SSH-based communication.

### SSH vs SCP

**SSH:**

> Secure remote access and command execution.

**SCP:**

> Secure file transfer.

---

# 96. rsync

`rsync` is a file synchronization tool.

It is efficient because it can transfer only changed files or changed portions when applicable.

Common uses:

* Backups
* Synchronization
* Deployment

---

# 97. Firewall

A firewall controls network traffic according to security rules.

Rules can consider:

* Source
* Destination
* Port
* Protocol
* Interface

---

# 98. `/proc`

`/proc` is a virtual filesystem that exposes information about:

* Processes
* Kernel
* System state

It is generated dynamically and is not simply a collection of ordinary files stored permanently on disk.

---

# 99. `/sys`

`/sys` is a virtual filesystem exposing information and interfaces related to:

* Kernel
* Devices
* Drivers
* Hardware relationships

---

# 100. `/dev`

`/dev` contains filesystem interfaces representing devices and other device-related resources.

Examples include:

* Disks
* Terminals
* Other hardware interfaces

---

# 101. Daemon

A **daemon** is a background process that usually provides a service without direct user interaction.

Examples:

* Web server daemon
* SSH service
* Logging service

---

# 102. systemd

`systemd` is a widely used Linux **system and service manager**.

It can manage:

* System startup
* Services
* Dependencies
* Service states
* Timers
* Logging integration
* Other system units

---

# 103. systemctl

`systemctl` is a management interface for interacting with systemd-managed units and services.

It can be used conceptually to:

* Start services
* Stop services
* Restart services
* Enable services
* Disable services
* Check service status

---

# 104. Journal

The **systemd journal** is a centralized logging system commonly provided by `journald`.

It stores system and service log information.

---

# 105. Cron Job

A **cron job** is a task scheduled to run automatically according to a specified time schedule.

Examples:

* Daily backups
* Periodic cleanup
* Scheduled reports

---

# 106. Package Manager

A package manager installs, updates, removes, and manages software packages and dependencies.

Examples:

* APT — Debian/Ubuntu
* DNF — Fedora/RHEL family
* Pacman — Arch Linux

---

# 107. Process Monitoring

Process monitoring means observing running processes and system-resource usage.

Information may include:

* PID
* CPU usage
* Memory usage
* Process state
* Runtime
* Resource consumption

Common Linux tools include process-listing and interactive monitoring utilities.

---

# 108. Profiling

**Profiling** means measuring a program's runtime behavior to identify performance bottlenecks.

It can identify:

* Slow functions
* CPU-heavy operations
* Memory usage
* Time-consuming operations

### Profiling vs Debugging

**Debugging:**

> Finds and fixes correctness problems.

**Profiling:**

> Finds performance bottlenecks.

---

# 109. Linter

A **linter** is a static-analysis tool that examines source code without executing it.

It can identify:

* Style issues
* Possible bugs
* Unused variables
* Bad practices

Python examples:

* Ruff
* Pylint
* Flake8

---

# 110. Debugger

A **debugger** is a tool used to inspect and control a program while it is executing.

It can help you:

* Pause execution
* Inspect variables
* Step through code
* Inspect the call stack
* Find where problems occur

---

# 111. Breakpoint

A **breakpoint** tells a debugger to pause program execution at a particular point.

Once paused, you can inspect:

* Variables
* Call stack
* Program state
* Execution flow

---

# 112. pdb

`pdb` is Python's built-in debugger.

It allows developers to:

* Set breakpoints
* Step through code
* Inspect variables
* Continue execution
* Understand program flow

---

# 113. Boot Process

A simplified Linux boot process is:

```text
BIOS / UEFI
     ↓
Bootloader
     ↓
Linux Kernel
     ↓
Init / System Manager
     ↓
System Services
     ↓
Login
```

---

# 114. BIOS

BIOS is traditional firmware that initializes hardware and starts the boot process.

---

# 115. UEFI

UEFI is modern firmware that replaced traditional BIOS in many systems.

It initializes hardware and loads the bootloader.

---

# 116. GRUB

GRUB is a commonly used Linux bootloader.

It can:

* Select a kernel
* Select an operating system
* Pass boot parameters
* Load the Linux kernel

---

# 117. "Everything Is a File"

Unix/Linux commonly provides file-like interfaces for many types of resources.

Examples:

* Regular files
* Devices
* Pipes
* Sockets
* Virtual filesystem interfaces

However:

> "Everything is a file" is a useful Unix abstraction, not a literal statement that every object is an ordinary disk file.

---

# 118. Least Privilege

The **principle of least privilege** means giving a user, process, or application only the permissions required to perform its task.

### Example

A web application that only needs to read application files should not automatically run as root.

---

# 119. Linux Security

Linux security involves multiple mechanisms:

* Users
* Groups
* Permissions
* Ownership
* Authentication
* sudo
* Process isolation
* Least privilege
* Firewall rules
* Security policies

No single mechanism provides complete security by itself.

---

# 120. User → Kernel → Hardware Flow

When an application needs a privileged operation:

```text
Application
     ↓
System Call
     ↓
Kernel
     ↓
Hardware / System Resource
     ↓
Kernel
     ↓
Application
```

The application normally does not directly control protected hardware resources.

---

# 121. Program → Process → Kernel Relationship

```text
Program
   ↓
Execution
   ↓
Process
   ↓
System Calls
   ↓
Kernel
   ↓
CPU / Memory / Disk / Network
```

A program becomes a process when it is executed, and the process uses kernel services to access system resources.

---

# 122. Important Reviewer Comparisons

## Unix vs Linux

**Unix:**

> Operating-system family.

**Linux:**

> Open-source Unix-like kernel.

---

## Shell vs Kernel

**Shell:**

> Interprets commands.

**Kernel:**

> Manages system resources and hardware access.

---

## Terminal vs Shell

**Terminal:**

> Interface for interacting with the shell.

**Shell:**

> Program that interprets commands.

---

## Program vs Process

**Program:**

> Passive instructions.

**Process:**

> Running instance of a program.

---

## User Space vs Kernel Space

**User space:**

> Restricted environment for normal applications.

**Kernel space:**

> Privileged environment for the kernel.

---

## Hard Link vs Soft Link

**Hard link:**

> Another directory entry referring to the same inode.

**Soft link:**

> Separate object referring to a pathname.

---

## Foreground vs Background

**Foreground:**

> Associated with the current terminal interaction.

**Background:**

> Runs without occupying the foreground interaction.

---

## Zombie vs Orphan

**Zombie:**

> Finished child whose termination status has not yet been collected.

**Orphan:**

> Running child whose original parent has terminated.

---

## SIGTERM vs SIGKILL

**SIGTERM:**

> Graceful termination request.

**SIGKILL:**

> Forced termination that cannot be caught.

---

## stdout vs stderr

**stdout:**

> Normal output.

**stderr:**

> Error/diagnostic output.

---

## chmod vs chown

**chmod:**

> Changes permissions.

**chown:**

> Changes ownership.

---

## sudo vs su

**sudo:**

> Executes with another user's privileges.

**su:**

> Switches to another user identity.

---

## grep vs find

**grep:**

> Searches text content.

**find:**

> Searches filesystem objects.

---

## Debugging vs Profiling

**Debugging:**

> Finds correctness problems.

**Profiling:**

> Finds performance problems.

---

## Kernel vs User-Space Scheduling

**Kernel scheduling:**

> Kernel decides which kernel-schedulable execution entity receives CPU time.

**User-space scheduling:**

> A runtime/library decides which of its own higher-level tasks should execute.

---

# 123. Core Mental Model

Remember this entire flow:

```text
                    USER
                      ↓
                   TERMINAL
                      ↓
                    SHELL
                      ↓
               APPLICATION
                      ↓
                SYSTEM CALL
                      ↓
                   KERNEL
          ┌───────────┼───────────┐
          ↓           ↓           ↓
        CPU         MEMORY       DEVICES
                                  ↓
                            DISK / NETWORK
```

And the major Linux areas:

```text
Unix / Linux
│
├── Operating System
│
├── Kernel
│   ├── Process management
│   ├── CPU scheduling
│   ├── Memory management
│   ├── Filesystem management
│   ├── Device management
│   ├── Networking
│   └── Security
│
├── User Space
│   ├── Applications
│   ├── Shell
│   ├── Libraries
│   └── Runtime environments
│
├── Filesystem
│   ├── Files
│   ├── Directories
│   ├── Permissions
│   ├── Ownership
│   ├── Inodes
│   └── Links
│
├── Processes
│   ├── Program
│   ├── Process
│   ├── PID
│   ├── PPID
│   ├── States
│   ├── Scheduling
│   ├── Signals
│   ├── Foreground
│   ├── Background
│   └── Exit codes
│
├── Memory
│   ├── Virtual memory
│   ├── Paging
│   └── Swap
│
├── IPC
│   ├── Pipes
│   ├── Shared memory
│   ├── Message queues
│   ├── Semaphores
│   ├── Signals
│   └── Sockets
│
├── Networking
│   ├── IP
│   ├── MAC
│   ├── Port
│   ├── TCP
│   ├── UDP
│   ├── DNS
│   ├── Ping
│   ├── SSH
│   └── SCP
│
└── System Management
    ├── Daemons
    ├── systemd
    ├── Journal
    ├── Cron
    ├── Package managers
    ├── Boot process
    └── Security
```

# ⭐ Highest-Priority Reviewer Topics

Based on your repeated review questions, these deserve the strongest preparation:

### P0 — Must Master

1. What is Unix?
2. What is Linux?
3. What is a kernel?
4. Roles of kernel
5. Types of kernels
6. What is a shell?
7. Types of Unix/Linux shells
8. Bash vs sh
9. SSH
10. SCP
11. Process vs program
12. User space vs kernel space
13. Process scheduling
14. Kernel-space scheduling
15. User-space scheduling
16. umask

### P1 — Very Important

17. Exit code
18. Signals
19. SIGTERM vs SIGKILL
20. Hard link vs soft link
21. Inode
22. File permissions
23. chmod vs chown
24. sudo vs su
25. Root user
26. Foreground vs background process
27. Background process
28. Zombie process
29. stdout
30. stdin
31. stderr
32. Piping
33. grep
34. Ping
35. Profiling
36. Linters
37. Debuggers
38. Breakpoints
39. pdb
40. Daemons
41. systemd
42. Cron jobs
43. `/proc`
44. `/sys`
45. `/dev`
46. System calls
47. fork
48. exec
49. Virtual memory
50. IPC
51. Networking basics
52. Boot process
53. Least privilege

# 🎯 One-Line Reviewer Answers

### Unix

> Unix is a multi-user, multitasking operating-system family.

### Linux

> Linux is an open-source Unix-like kernel used as the core of many Linux distributions.

### Kernel

> The kernel is the core of the operating system that manages CPU, memory, processes, devices, filesystems, networking, and security.

### Shell

> A shell is a command interpreter that allows users to interact with the operating system.

### Process

> A process is an executing instance of a program.

### Program

> A program is a passive set of instructions stored on a system.

### Kernel scheduling

> Kernel scheduling is the process by which the kernel decides which runnable execution entity receives CPU time.

### User-space scheduling

> User-space scheduling is scheduling performed by a runtime or library to manage higher-level tasks such as coroutines or user-level threads.

### Signal

> A signal is a software notification delivered to a process or thread to indicate an event or request an action.

### Exit code

> An exit code is the numeric status returned by a process when it terminates.

### umask

> umask removes permission bits from the default permissions used when new files and directories are created.

### Inode

> An inode stores filesystem metadata and references the underlying data of a file.

### SSH

> SSH is a secure protocol mainly used for remote login and command execution.

### SCP

> SCP is used to securely transfer files between systems using SSH-based communication.

### Daemon

> A daemon is a background process that normally provides a system or network service.

### Cron job

> A cron job is a task scheduled to run automatically at specified times.

### Profiling

> Profiling measures runtime behavior to identify performance bottlenecks.

### Linter

> A linter statically analyzes source code to detect style problems, possible bugs, and bad practices.

### Zombie

> A zombie is a terminated child process whose parent has not yet collected its exit status.

### Root

> Root is the Unix/Linux superuser with extensive system privileges.

### Pipe

> A pipe connects the output of one process to the input of another process.

### stdout

> stdout is the standard output stream of a process.

### stderr

> stderr is the standard error and diagnostic stream of a process.

### chmod

> chmod changes file or directory permissions.

### chown

> chown changes file ownership.

### sudo

> sudo allows an authorized user to execute an operation with another user's privileges.
