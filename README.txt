CS349 - TFTP client server implementation 
Author: Chetan Anand
Roll No:11010117

################# Manual Instruction #####################

Installation:	make

Uninstallation:	make clean

##########################################################
Client Help Command : ./tftpc 		(Following menu will be displayed)


Usage: Client
./tftpc server [-h] [-d] [-P port] [-g] | [-p] [file-name] [-w size] [-l length] [-o] [-n]
Options:
-h (help; this message)
-d (Debug mode)
-P port(Port number default is 69)
-g (get a file from the server)
-p (send a file to the server)
-w size (set window size, default is 1)
-l len (set max packet length, default is 512 bytes)
-o for octet file transfer (default).
-n for netascii file transfer.

#############################################################
Server Help Command : ./tftpd -h    (Following menu will be display)

Usage: Server
./tftpd [options] [path]
Options:
-p (Specify the path mode)
-d (debug mode)
-h (help; this message)
-P <port>
-a <ack freqency. Default 1>
-s <data chunk size in bytes. Default 512>

#############################################################
#############################################################
Sample command-
(For Client setup):
./tftpc 127.0.0.1 -d -p sendfile.txt  (for sending sendfile.txt to server)

./tftpc 127.0.0.1 -d -g rcvfile.txt  (for getting rcvfile.txt from server)


Sample command-
(For Server setup):
./tftpd -d -p filepath       Default server path is /home/

like mine is  ./tftpd -d -p /home/codefire/server/


For further query I have also included the pics of usage. Please see that for any clarification or else you can contact me.
