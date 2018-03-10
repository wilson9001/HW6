

Please do the following on a Linux system.

1. Setup
1a. Download hw6.tar.gz and un-tar/gzip it to a directory:
 
hw6.tar.gz  Download

$ tar -zxvf hw6.tar.gz

Note: LearningSuite has issues with file uploads, and you might have to do the following instead:

$ gzip -cd hw6.tar.gz | tar -zxvf -

2. Run "make" to build four servers: echoserveri, echoserverp, echoservert, and echoservert_pre.  These are versions of the echo server that use no concurrency, process-based (using fork()) concurrency, simple thread-based concurrency (threads created on the fly), and thread-based concurrency using a thread-pool.

3 through 6. For each server (i.e., echoserveri, echoserverp, echoservert, and echoservert_pre), do the following:

Start the server:
./echoserver 5888

(Please replace "echoserver" with the appropriate name of the binary for the server you are running.  The port is arbitrary - it can be anything above 1023).

Open three other windows *on the same machine*.  In each one, run the following:
$ nc localhost 5888

After all three are running, type some text in the first of the three windows running "nc", and press enter.  Repeat with the second and third.

3a/4a/5a/6a. What do you observe?  Is the server responsive?

    In each case the server is responing by echoing back my input and reporting how many bytes were received on the terminal where I started them all.

In a new fifth window, run the following:
$ ps -Lo user,pid,ppid,nlwp,lwp,vsz,rss,state,ucmd -C echoserver | grep casey

(Note: use your own username in place of "casey", and use the actual name of the binary in place of "echoserver")
The "ps" command lists information about processes that current exist on the system.  The -L option tells us to show threads as if they were processes.  We have selected to show only several fields:
user: the username of the user running the process (should be your CS username)
pid: the process ID of the process
ppid: the process ID of the parent process
nlwp: the number of threads (light-weight processes) being run
lwp: the thread ID of the thread
vsz: the number of bytes of memory potentially used by the process
rss: the number of bytes of memory currently being used by the process
state: the state of the process, e.g., Running, Sleep, Zombie
ucmd: the command executed.

3b/4b/5b/6b. Show the output from the ps command.

    alex@alex-Mint ~/Documents/HW6/hw6 $ ps -Lo user,pid,ppid,nlwp,lwp,vsz,rss,state,ucmd -C echoserveri | grep alex
    alex      9543  3695    1  9543   8656  1928 S echoserveri

    alex@alex-Mint ~/Documents/HW6/hw6 $ ps -Lo user,pid,ppid,nlwp,lwp,vsz,rss,state,ucmd -C echoserverp | grep alex
    alex      9610  3695    1  9610   6536   740 S echoserverp
    alex      9958  9610    1  9958   6536   112 S echoserverp

    alex@alex-Mint ~/Documents/HW6/hw6 $ ps -Lo user,pid,ppid,nlwp,lwp,vsz,rss,state,ucmd -C echoservert | grep alex
    alex      9640  3695    2  9640  80268   884 S echoservert
    alex      9640  3695    2  9972  80268   884 S echoservert

    alex@alex-Mint ~/Documents/HW6/hw6 $ ps -Lo user,pid,ppid,nlwp,lwp,vsz,rss,state,ucmd -C echoservert_pre | grep alex
    alex      9654  3695   81  9654 662220  1948 S echoservert_pre
    alex      9654  3695   81  9655 662220  1948 S echoservert_pre
    alex      9654  3695   81  9656 662220  1948 S echoservert_pre
    alex      9654  3695   81  9657 662220  1948 S echoservert_pre
    alex      9654  3695   81  9658 662220  1948 S echoservert_pre
    alex      9654  3695   81  9659 662220  1948 S echoservert_pre
    alex      9654  3695   81  9660 662220  1948 S echoservert_pre
    alex      9654  3695   81  9661 662220  1948 S echoservert_pre
    alex      9654  3695   81  9662 662220  1948 S echoservert_pre
    alex      9654  3695   81  9663 662220  1948 S echoservert_pre
    alex      9654  3695   81  9664 662220  1948 S echoservert_pre
    alex      9654  3695   81  9665 662220  1948 S echoservert_pre
    alex      9654  3695   81  9666 662220  1948 S echoservert_pre
    alex      9654  3695   81  9667 662220  1948 S echoservert_pre
    alex      9654  3695   81  9668 662220  1948 S echoservert_pre
    alex      9654  3695   81  9669 662220  1948 S echoservert_pre
    alex      9654  3695   81  9670 662220  1948 S echoservert_pre
    alex      9654  3695   81  9671 662220  1948 S echoservert_pre
    alex      9654  3695   81  9672 662220  1948 S echoservert_pre
    alex      9654  3695   81  9673 662220  1948 S echoservert_pre
    alex      9654  3695   81  9674 662220  1948 S echoservert_pre
    alex      9654  3695   81  9675 662220  1948 S echoservert_pre
    alex      9654  3695   81  9676 662220  1948 S echoservert_pre
    alex      9654  3695   81  9677 662220  1948 S echoservert_pre
    alex      9654  3695   81  9678 662220  1948 S echoservert_pre
    alex      9654  3695   81  9679 662220  1948 S echoservert_pre
    alex      9654  3695   81  9680 662220  1948 S echoservert_pre
    alex      9654  3695   81  9681 662220  1948 S echoservert_pre
    alex      9654  3695   81  9682 662220  1948 S echoservert_pre
    alex      9654  3695   81  9683 662220  1948 S echoservert_pre
    alex      9654  3695   81  9684 662220  1948 S echoservert_pre
    alex      9654  3695   81  9685 662220  1948 S echoservert_pre
    alex      9654  3695   81  9686 662220  1948 S echoservert_pre
    alex      9654  3695   81  9687 662220  1948 S echoservert_pre
    alex      9654  3695   81  9688 662220  1948 S echoservert_pre
    alex      9654  3695   81  9689 662220  1948 S echoservert_pre
    alex      9654  3695   81  9690 662220  1948 S echoservert_pre
    alex      9654  3695   81  9691 662220  1948 S echoservert_pre
    alex      9654  3695   81  9692 662220  1948 S echoservert_pre
    alex      9654  3695   81  9693 662220  1948 S echoservert_pre
    alex      9654  3695   81  9694 662220  1948 S echoservert_pre
    alex      9654  3695   81  9695 662220  1948 S echoservert_pre
    alex      9654  3695   81  9696 662220  1948 S echoservert_pre
    alex      9654  3695   81  9697 662220  1948 S echoservert_pre
    alex      9654  3695   81  9698 662220  1948 S echoservert_pre
    alex      9654  3695   81  9699 662220  1948 S echoservert_pre
    alex      9654  3695   81  9700 662220  1948 S echoservert_pre
    alex      9654  3695   81  9701 662220  1948 S echoservert_pre
    alex      9654  3695   81  9702 662220  1948 S echoservert_pre
    alex      9654  3695   81  9703 662220  1948 S echoservert_pre
    alex      9654  3695   81  9704 662220  1948 S echoservert_pre
    alex      9654  3695   81  9705 662220  1948 S echoservert_pre
    alex      9654  3695   81  9706 662220  1948 S echoservert_pre
    alex      9654  3695   81  9707 662220  1948 S echoservert_pre
    alex      9654  3695   81  9708 662220  1948 S echoservert_pre
    alex      9654  3695   81  9709 662220  1948 S echoservert_pre
    alex      9654  3695   81  9710 662220  1948 S echoservert_pre
    alex      9654  3695   81  9711 662220  1948 S echoservert_pre
    alex      9654  3695   81  9712 662220  1948 S echoservert_pre
    alex      9654  3695   81  9713 662220  1948 S echoservert_pre
    alex      9654  3695   81  9714 662220  1948 S echoservert_pre
    alex      9654  3695   81  9715 662220  1948 S echoservert_pre
    alex      9654  3695   81  9716 662220  1948 S echoservert_pre
    alex      9654  3695   81  9717 662220  1948 S echoservert_pre
    alex      9654  3695   81  9718 662220  1948 S echoservert_pre
    alex      9654  3695   81  9719 662220  1948 S echoservert_pre
    alex      9654  3695   81  9720 662220  1948 S echoservert_pre
    alex      9654  3695   81  9721 662220  1948 S echoservert_pre
    alex      9654  3695   81  9722 662220  1948 S echoservert_pre
    alex      9654  3695   81  9723 662220  1948 S echoservert_pre
    alex      9654  3695   81  9724 662220  1948 S echoservert_pre
    alex      9654  3695   81  9725 662220  1948 S echoservert_pre
    alex      9654  3695   81  9726 662220  1948 S echoservert_pre
    alex      9654  3695   81  9727 662220  1948 S echoservert_pre
    alex      9654  3695   81  9728 662220  1948 S echoservert_pre
    alex      9654  3695   81  9729 662220  1948 S echoservert_pre
    alex      9654  3695   81  9730 662220  1948 S echoservert_pre
    alex      9654  3695   81  9731 662220  1948 S echoservert_pre
    alex      9654  3695   81  9732 662220  1948 S echoservert_pre
    alex      9654  3695   81  9733 662220  1948 S echoservert_pre
    alex      9654  3695   81  9734 662220  1948 S echoservert_pre

3c/4c/5c/6c. From the ps output, how many processes and how many threads are running, and why?  Use the PID and LWP to identify different threads or processes.

    Well it looks like echoserveri has one process with one thread, echoserverp has two processes with one thread each (this is the one that uses fork()), echoservert has one process with 2 threads running, and echoservert_pre has a whopping 81 threads already running under just one process. Echoserverp and echoservert have each spun off a process and thread respectively to handle my ncat connections to them. Echoservert_pre has created a pool of threads before they are needed and they are just sleeping.

3d/4d/5d/6d. From the ps output, how much resident memory are they collectively (i.e., total) using on the system?  Note that memory for a given process should only be counted once, not once for each of its threads.

    1928 + (740 + 112) + 884 + 1948 = 5612 bytes

3e (echoserveri only). Enter "Ctrl-C" on the window in which "nc" was first executed to interrupt it.  What happens to the "nc" processes in the other windows?

    Umm nothing? Was something supposed to happen? They all still echo my input... Killing the ncat process didn't stop any of the servers from running or to report anything...

Stop the server by using "Ctrl-C".

7. Name at least one pro and one con to each of the four programming paradigms in this assignment.  You can use your own observations, as well as the book chapter.
a. echoserveri
    * Pro: Simple to write, debug, and understand.
    * Con: Can only handle one client at a time, serious loss of potential performance gains from concurrency.
b. echoserverp
    * Pro: Allows for concurrency to handle multiple clients at once without introducing the risks of shared data structures caused by threads.
    * Con: Consumes a lot of resources and cannot effectively scale.
c. echoservert
    * Pro: Handles multiple clients effectively through concurrency but is also more scalable than creating new processes for each client.
    * Con: Introduces concurrency bugs in critical sections of code if they are not adequately protected through semaphores.
d. echoservert_pre
    * Pro: Same pro as echoservert but is even more scalable as the overhead of creating the threads is taken care of before a client connects to the server.
    * Con: There are times, potentially a lot of times, where the process has most of the threads sitting there uselessly.

8. Consider the code in echoservert_pre.c for the following questions:
a. Which line of code represents the producer role?  How many producer threads are there?

    The only producer thread is the main thread which spawned all the others, and it produces data for the buffer in line 35:
    sbuf_insert(&sbuf, connfd); /* Insert connfd in buffer */

b. Which line of code represents the consumer role?  How many consumer threads are there?

    All 80 of the spawned threads are consumers because they wait until there is data in the buffer for them to take out and then echo back to the client. This consumption from the buffer is done on line 43:
    int connfd = sbuf_remove(&sbuf); /* Remove connfd from buffer */ //line:conc:pre:removeconnfd

9. Consider the code in sbuf.c for the following questions (P() is equivalent to sem_wait() and V() is equivalent to sem_post()):
a. On line 30, what happens when the slots member is zero?

    The calling thread waits until the sempahore increments to a non-zero value and the thread is able to consume the semaphore and run. Until then it isn't even scheduled by the kernel. This means that the producer thread cannot add another value to the buffer because the buffer is completely full.

b. In the case that a single consumer thread is sleeping at line 43, waiting for a non-zero value of items, what line of code will be executed by a producer to wake that thread up?
 
    Line 34:
    V(&sp->items);

Submission
Please upload. your writeup as a document of type txt, pdf, or docx to LearningSuite.
