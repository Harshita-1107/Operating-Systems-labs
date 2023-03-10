 FOR Question 1 :
 Run :  gcc diskScheduling.c -o scheduling
Run : ./scheduling

NOTE : we need to know the number of requests and number of cyclinders before hand
For ith request : space separated input should be given as:   cyclinderNumber arrivaltime 
 
	REPORT (FAT)
 
To run create and run the executable :
	First go to The Alternative1FAT directory 
                 create the executable using : Run:  make
                 Run executable : ./a.out

This report discusses the strategy that we have used in the linked list based FAT implementation of file system.


1. User function must enter the file sie, block size and initialize the file system by calling the function 'init'.

2. The file system contains a fixed number of blocks, that depends on the file size and block size. The first block is the super block that contains necessary information about the file system and a bit vector that denotes the free blocks.

3. The first block contains the FAT table, second block contains the directory information and the other blocks are data blocks.

4. We also maintain a file descriptor table that indicated the file descriptors that are valid and maintains the pointers for reading and writing to the file.

5. my_open() function opens a file and returns a file descriptor. It initializes the read and write pointers for that file descriptor. It creates a new file and enters the data in the directory if it is already not there.

6. my_read() function takes input as the file descriptor, a character buffer where the data is to be read and the number of bytes that is to be read. It first goes to the current block maintained in the file descriptor table and then reads from the file.

7. my_write() function takes input parameters as the file descriptor, a character buffer that is to be written into the file and the number of bytes of data that needs to be written. Operation is similar to my_read() function.

8. my_cat() function prints the contents of the file.

9. my_copy() takes as input the file descriptor(1st argument), a linux file descriptor(2nd argument) and a flag that would denote the sorce and the destination of the copied file. If flag is 0, then copy from linux fd to FAT fd. If flag is 1, just the opposite.

10. my_close() function invalidates the file descriptor.

11. The functions can be used as an API call from the user program. A library called "alt.h" is to be included that would contain the functions. The user must use Makefile to run the program.

12. 'alt1.h' is the header file while function definitions are written in 'alt1.cpp'. 'assn6_grp_14.cpp' is the user program.


 










 

 
	REPORT (INODE)
To run create and run the executable :
	First go to The Alternative2INODE directory 
                 create the executable using : Run:  make
                 Run executable : ./a.out 


This is a report that describes the procedure we followed for the i-node representation of file system.

1. All the structures and the API fucntion prototype are defined in the header file. The file system is represented as a structure of blocks where the first block is the super block that contains the necessary inofrmation, free inode list and the pointer to the first free block. The next two blocks contains th inodes, and then the remaining blocks will store the data.

2. We first initialize the file system by calling init(), that fills in appropriate values in the fiels and creates memory.

3. my_mkdir() takes a string as input. It then searches through the blocks pointed by the inode to find a match. If match is found, -1 is returned. Else, a new entry is made to the block by writing the name of the directory in the appropriate block pointed either by DP, SIP, or DIP. An inode is also chosen that will contain the information of the new directory which is initialised.

3. my_rmdir() takes a string as an input and first searches to find out the inode number of the requested directory. If it is found, the inode is made empty and all the subsequent directories and files the chosen directory contains. Appropriate changes are made to the free inode list and free blocks.

5. my_chdir() takes a string as input and checks whether it is the parent directory. It makes appropriate changes. If the directory is found, then a proper chamge is made by changing the current directory pointer.

6. my_open() takes a string filename as input and check within the current directory if the file already exists. If yes, make a new entry to the FD list that will open another stream. Initialize the FD table. If the file is not found, then make an entry in the inode of the current directory. An inode is chosen for the new file and then the inode is initialized. A new entry in the FD table is maintianed and initialized that would correspond to the specific file.

7. my_read() takes a file descriptor, a buffer, and a count as input and reads count number of bytes from the file and writes it to buffer.

8. my_write() takes a file descriptor, a buffer, and a count as input and writes count number of bytes to the file after reading them from the buffer.

9. my_close() closes the file descriptor, that is makes it invalid.
