# OS_device_driver
Operating systems

In this mini-project I learned about kernel programing (Linux) and drivers.

I implemented a kernel module that provides a new IPC (inter-process communication) mechanism, called message slot.
A message slot is a character device file through which processes communicate.
The device has multiple message channels active concurrently, which can be used by multiple processes.
After opening a message slot device file, a process uses ioctl() to specify the
id of the message channel it wants to use. It subsequently uses read()/write() to receive/send
messages on the channel. In contrast to pipes, a message channel preserves a message until it
is overwritten, so the same message can be read multiple times.

Run this to compile:
1. make
2. sudo insmod message_slot.ko
3. mknod /dev/slot_name_of_your_choice c 235 1 (1 is an example - this is seriel integer for the device, of your choice)
4. gcc -O3 -Wall -std=c11 message_sender.c (or message_reader.c)

Arguments for message_reader.c:
1. Message slot file path
2. The target message channel ID: a non-negative integer
3. The message to pass

Arguments for message_sender.c: (prints to standard output)
1. Message slot file path
2. The target message channel ID: a non-negative integer
