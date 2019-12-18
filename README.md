# useful unix command


## Signals (IPC), kill and annoying processes

### Quick
* <kbd>Ctrl</kbd>+<kbd>z</kbd> suspends process execution
* <kbd>Ctrl</kbd>+<kbd>c</kbd> politely asks the process to terminate
* <kbd>Ctrl</kbd>+<kbd>\\</kbd> mercilessly kill (terminate and dump core) the process that is currently in the foreground.
* <kbd>Ctrl</kbd>+<kbd>T</kbd> ask OS operating system to show information about the running command

To kill zombie processes using [process ID][1] (find PID using `pgrep`][2] or `ps`[3]) and [`kill`][4]:

     % kill -9 PID

### Terse

* **SIGTSTP** suspension      thru terminal (ctrl-z)                  can be caught
* **SIGINT** termination      thru terminal (ctrl-c) with grace       can be caught
* **SIGQUIT** kill            thru terminal (ctrl-\) with dump core   can be caught
* **SIGSTOP** suspension      thru shell                              cannot be caught
* **SIGTERM** termination     thru shell with grace first if not kill can be caught
* **SIGKILL** kill            thru shell immediately                  cannot be caught

### Verbose:

* **SIGTSTP** is the termial pause signal. The default behavior is to pause the process; the signal cannot be caught or ignored. The shell uses pausing (and its counterpart, resuming via SIGCONT/'fg') to implement job control.

* **SIGINT** is the interrupt signal. The terminal sends it to the foreground process when the user presses ctrl-c. The *default* behavior is to terminate the process, but it can be caught or ignored. The intention is to provide a mechanism for an orderly, graceful shutdown.

* **SIGQUIT** is the dump core signal. The terminal sends it to the foreground process when the user presses ctrl-\. The *default* behavior is to terminate the process and dump core, but it can be caught or ignored. The intention is to provide a mechanism for the user to abort the process. You can look at SIGINT as "user-initiated happy termination" and SIGQUIT as "user-initiated unhappy termination."

* **SIGSTOP** is the pause signal. The *only* behavior is to pause the process; the signal cannot be caught or ignored. The shell uses pausing (and its counterpart, resuming via SIGCONT) to implement job control.

* **SIGTERM** is the termination signal. The *default* behavior is to terminate the process, but it also can be caught or ignored. The intention is to kill the process, gracefully or not, but to first allow it a chance to cleanup. (You can look at SIGINT as SIGTERM where intended specifically for requests from the terminal: particular input characters can be assigned to generate these signals)

* **SIGKILL** is the kill signal. The *only* behavior is to kill the process, immediately. As the process cannot catch the signal, it cannot cleanup, and thus this is a signal of last resort.

You can send these signals via the [kill][4] command. 


### Reminders
* Shell is a program which processes commands and returns output, like bash in Linux. Exteremly roughly speaking, shell is an OS thing! Since the kernel is really low-level a shell is provided - a program that let's the user interact with the kernel in an easy way. 
* Terminal is a physical program for handling text input/output. It also runs a shell to execute commands. (In the past it was a physical device (teletypes) with monitors, keyboards and then its concept was transferred into software, like Gnome-Terminal.

### References
To develop this page I heavily used [man signal][5] and borrowed tons of knowledge from many fruitful discussions and posts on [askubuntu][6], [stackoverflow][7], [wikipedia][8], [quora][9] and etc.

  [1]: http://en.wikipedia.org/wiki/Process_identifier
  [2]: https://man.cx/pgrep
  [3]: https://man.cx/ps
  [4]: http://man.cx/kill
  [5]: http://man.cx/signal(7)
  [6]: https://askubuntu.com/
  [7]: https://stackoverflow.com/
  [8]: https://en.wikipedia.org/wiki/Signal_(IPC)
  [9]: https://www.quora.com/
  
  
