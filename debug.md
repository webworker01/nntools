Decker
More detailed instruction how you can help to solve the komodod hang problem. If you faced with deadlock / hang, plz do the following:

0. compile your komodod using following command CPPFLAGS="-DDEBUG_LOCKCONTENTION" zcutil/build.sh -j$(nproc) and run it as usually.
1. when you will faced with hang -> open new text file on your PC and mentione in it - did you used wallet filter (-whitelistaddress), did you have opened p2p (7770/tcp) port for komodod on your node.
2. run sudo gdb
3. type attach <pid> , where the pid is a pid of your KMD komodod
4. type info threads and copy & paste full information from output in text file (you should have ~20-30 thread lines, one line per thread)
5. make the following for each thread (this means, if you have 30 threads in output of (4) you should repeat this step 30 times):
    type thread n, where n is number of thread , then type bt and copy info to text file.
6. copy the last lines of stdout + stderr (komodod on-screen output) to text file.
7. copy the last lines of debug.log to text file.
8. post your text file on gist.github.com or pastebin and share the link here or DM me.
