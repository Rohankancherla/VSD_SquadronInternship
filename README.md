# VSD_SquadronInternship
The program is based on the RISC-V architecture and uses open-source tools to teach people about VLSI chip design and RISC-V. The instructor for this internship is Kunal Ghosh Sir.

<details>
<summary><b>Task 1:</b> C based and RISC-V based programs for sum of n numbers</summary>   
<br>

C based
------------------------------------------

Install leafpad editor 

*Use the following command for installing leafpad*
```
sudo apt install leafpad
```
Now we need to write a program in c for sum of 1 to n numbers, and save the file as "sum1ton.c"

![c program sum1ton](https://github.com/user-attachments/assets/b180bdc1-1a9e-4b64-b215-1f6f199b9d8d)

Now after we compile this and run using the commands :

```
gcc sum1ton.c
./a.out
```
The output of the c code is :

![C sum1ton_output](https://github.com/user-attachments/assets/37f78ab9-44da-4f6a-ab16-8caafe2d0a61)

RISC-V based
------------------------------------------

We can view the sum code using the following command :
```
cat sum1ton.c
```
The terminal output of the above the commad :

![viewing_C_sumcode](https://github.com/user-attachments/assets/217bbee9-c294-48e4-9610-2883d24159fa)

For compiling the above code in RISC-V we use the command :
```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```

![o1_input](https://github.com/user-attachments/assets/c131b9bc-9874-49b2-91de-0706cc822201)


Now the file has been saved "sum1ton.o"
In the new tab we need to give the command ``` riscv64-unknown-elf-objdump -d sum1ton.o | less ```

Now the assembly language code for ```O1``` is :

![o1_output](https://github.com/user-attachments/assets/f21d9c9f-a1ed-42e7-b4d1-5ee00920266e)

Here if we calculate the number of instructions, we get the total instructions as 11.
It is calculated as 
``` 
101b0 - 10184 = 2c
2c/4 = b  => 11
```
Now similarly we need to execute the code for ``` Ofast ``` command

The input is shown as :

![Ofast_input](https://github.com/user-attachments/assets/540e85aa-e6cc-47ef-bdf0-20f368c8fa88)

The output of the ``` Ofast ``` command is :

![Ofast_output](https://github.com/user-attachments/assets/290aae34-f470-4972-ba2e-4a1d87828e40)

Again if we calculate the number of instructions , we get the instructions as 11.
It is calculated as 
``` 
100dc - 100b0 = 2c
2c/4 = b  => 11
```
</details>

------------------------------------

<details>
<summary><b>Task 2:</b> C </summary>

In the previous task we have seen the contents of the assembly language program for the program ```sum1ton.o``` .
Now if we debug the code we get the output of sum of 1 to n numbers. 
Now the same thing should be outputed in a RISC-V compiler. We can show this using the spike command.
Spike is a RISC-V simulator. 
It is used for running and testing codes for RISC-V based processors.
Now using the below command we can simulate the ```sum1ton.o``` code and verify the instructions.

*Use the following command*
```
spike pk sum1ton.o
```
Now we can see the output:
![spike_output_sum1ton](https://github.com/user-attachments/assets/ac115a02-d36c-4765-8b8b-5901d3f3c90a)





</details>
