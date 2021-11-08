# Buffer-Overflow-Attack
The code show how a buffer overflow attack can be implemented to insert malicious code in a stack.
Total Files:
1. call_shellcode.c
2. stack.c
3. prog.c
4. exploit.py
5. setroot.c


For Task-1:

Use the file: call_shellcode.c for launching shell

To compile the file, use the following command:

gcc -z execstack -o call_shellcode call_shellcode.c

To compile with GDB, add -g in the arguments of the above command.

To run the generated call_shellcode, use the following command:

./call_shellcode

-----------------------------------------------------------------------------

For Task-2:

Use the following files:
1. stack.c //vulnerable file, updated the BUF_SIZE with 256
2. prog.c  //to check if the address randomization is successfully turned off
3. exploit.py //file used create the bad file which will be used by stack.c
4. setroot.c  //To set euid to ruid after the attack is sucessful

a) stack.c

First compile the stack.c file by using the following command:

	gcc -o stack -z execstack -fno-stack-protector stack.c

Change ownwership to root and Set-UID of the generated stack.c file by the following commands:

	sudo chown root stack
	sudo chmod 4755 stack

To run the generated stack.c file, use the following command:

	./stack.c

To compile the above command with GDB to retrieve ebp address, buffer starting address and distance between buffer start address and eip:

	gcc -z execstack -fno-stack-protector -g -o stack_dbg stack.c

To run the debugger, use the following command:

	gdb stack_dbg


b) prog.c:

To compile the prog.c file, use the following command:

	gcc prog.c -o prog

To run the generated prog file, use the following command multiple times and ensure that the output address does not change:

	./prog


c) exploit.py:

Use the following commands to create an executable exploit.py and run it:
	chmod u+x exploit.py
	stack$ exploit.py
	
d) setroot.c

Use th following commands to create an executable setroot and run it after getting the root shell:
	gcc setroot.c -o setroot
	./setroot



