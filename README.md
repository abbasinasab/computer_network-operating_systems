# useful unix command


## To kill annoying process: 
* <kbd>Ctrl</kbd>+<kbd>Z</kbd>: pause a process and give return conrol to terminal. 
* <kbd>Ctrl</kbd>+<kbd>C</kbd>: politely ask the process to shut down now.
* <kbd>Ctrl</kbd>+<kbd>\\</kbd>: mercilessly kill the process that is currently in the foreground.

### Quick:
* <kbd>Ctrl</kbd>+<kbd>z</kbd> suspends process execution
* <kbd>Ctrl</kbd>+<kbd>c</kbd> politely asks the process to terminate
* <kbd>Ctrl</kbd>+<kbd>\\</kbd> mercilessly kill (terminate and dump core) the process that is currently in the foreground.
* <kbd>Ctrl</kbd>+<kbd>T</kbd> (sends an INFO signal (SIGINFO); by default, and if supported by the command, this causes the operating system to show information about the running command.

### Terse:

* SIGTSTP suspension     thru terminal (ctrl-z)                  can be caught
* SIGINT: termination    thru terminal (ctrl-c) with grace       can be caught
* SIGQUIT kill           thru terminal (ctrl-\) with dump core   can be caught
* SIGSTOP suspension     thru shell                              cannot be caught
* SIGTERM termination    thru shell with grace first if not kill can be caught
* SIGKILL kill           thru shell immediately                  cannot be caught

### Verbose:

* SIGTSTP is the termial pause signal. The default behavior is to pause the process; the signal cannot be caught or ignored. The shell uses pausing (and its counterpart, resuming via SIGCONT 'fg') to implement job control.

* SIGINT is the interrupt signal. The terminal sends it to the foreground process when the user presses ctrl-c. The *default* behavior is to terminate the process, but it can be caught or ignored. The intention is to provide a mechanism for an orderly, graceful shutdown.

* SIGQUIT is the dump core signal. The terminal sends it to the foreground process when the user presses ctrl-\. The *default* behavior is to terminate the process and dump core, but it can be caught or ignored. The intention is to provide a mechanism for the user to abort the process. You can look at SIGINT as "user-initiated happy termination" and SIGQUIT as "user-initiated unhappy termination."

* SIGSTOP is the pause signal. The *only* behavior is to pause the process; the signal cannot be caught or ignored. The shell uses pausing (and its counterpart, resuming via SIGCONT) to implement job control.

* SIGTERM is the termination signal. The *default* behavior is to terminate the process, but it also can be caught or ignored. The intention is to kill the process, gracefully or not, but to first allow it a chance to cleanup. (You can look at SIGINT as SIGTERM where intended specifically for requests from the terminal: particular input characters can be assigned to generate these signals)

* SIGKILL is the kill signal. The *only* behavior is to kill the process, immediately. As the process cannot catch the signal, it cannot cleanup, and thus this is a signal of last resort.


Like KILL, STOP can’t be caught, blocked, or ignored: it always stops the receiving process. TSTP on the other hand can be ignored or handled in a different way; for example, shells, and Emacs, set up TSTP handlers to deal with CtrlZ themselves. This behaviour in shells ensures that pressing CtrlZ is always safe, and won’t get you stuck in a terminal with a stopped process and no way of resuming it.

a process by its controlling terminal ] for later resumption (until 'fg') and can be caught. 
Most shells bind <kbd>Ctrl</kbd> + <kbd>C</kbd> to "send a [SIGINT][1] signal to the program that currently runs in the foreground".
Programs can ignore [SIGINT][1] and [SIGTSTP][2] signals. There are, however, some signals which can not be ignored by the process such as [SIGKILL][3] and [SIGSTOP][4]. You can read about the different signals using [man signal][7]

You can send these signals via the [kill][6] command. So, to kill zombie processes, just find the [process ID][7] (PID). For example, use `pgrep` or `ps` and then `kill` it

     % kill -9 PID


  [1]: http://en.wikipedia.org/wiki/Unix_signal#SIGINT
  [2]: http://en.wikipedia.org/wiki/Unix_signal#SIGTSTP
  [3]: http://en.wikipedia.org/wiki/Unix_signal#SIGKILL
  [4]: http://en.wikipedia.org/wiki/Unix_signal#SIGSTOP
  [5]: http://man.cx/signal(7)
  [6]: http://man.cx/kill
  [7]: http://en.wikipedia.org/wiki/Process_identifier
  
Shell is a program which processes commands and returns output , like bash in Linux .Shell is an OS thing. On a computer you have the kernel which on Ubuntu for example is the Linux part. Now since the kernel is really low-level a shell is provided - a program that let's the user interact with the kernel in an easy way. That's what BASH is for example.

Terminal is a program that run a shell , in the past it was a physical device (Before terminals were monitors with keyboards, they were teletypes) and then its concept was transferred into software , like Gnome-Terminal .
Terminal is the end of something
