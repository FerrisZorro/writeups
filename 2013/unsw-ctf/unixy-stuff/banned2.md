### banned2
> there's a flag somewhere else on the banned box

We didn't actually solve this, but we were pretty close.

You needed to look at `/root/backup_encrypted.sh`.  You would find that:

* a large portion of the script is run in `sudo` regularly; and
* a backup is stored at `/var/log/bak`, which was world readable.

The simple way to do this is to just make a while loop `while true; do ps -ef | grep [s]udo; sleep 1; done`, which will grep the process listing looking for a command with sudo (the `[s]udo` stops grep finding itself in the process listing). You then found the key is `when you call my name, its like a little prayer`. So you just `scp ctf2@<ip>:/var/log/bak .` that bad boy and `luksOpen` it, and you have the filesystem mounted. The key is just a small `sudo cat flags` away.
