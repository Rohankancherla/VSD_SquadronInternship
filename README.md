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

-
</details>

------------------------------------

<details>
<summary><b>Task 2:</b> C based and RISC-V based programs for sum of n numbers</summary>   
<br>

Spike simulation
------------------------------------------
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
Now we can give the input as follows:

![tsak2_spike_pk_sum1ton](https://github.com/user-attachments/assets/874bef71-58fc-4e10-83f4-f7db94558673)

The assembly langguage program for ```Ofast``` compiler is :


![new_task1_12instr](https://github.com/user-attachments/assets/56d2ec70-05cc-4ea6-ac71-ca8d580f2949)


Now let us debug this code:

![Task2_Ofast_output](https://github.com/user-attachments/assets/949c04ad-a5dd-4735-8378-8465036c514e)

* We debug the assembly language program using the command ```spike -d pk sum1ton.o``` .
* In this debugger we debug the code for each instruction (or till the required instruction) 
* At the address of ```100b4``` the value of the stack pointer is ```0x0000003ffffffb50``` and after the executing the next instruction we get the value of the stackl pointer as ```0x0000003ffffffb40```.

The next instruction is executed using the command ```  addi    sp, sp, -16 ``` . So if we subtract 16 in decimal it is equivalent to 10 in hexadecimal which is shown below in the calculator :

![task2_Ofast_calculator](https://github.com/user-attachments/assets/454bee73-e31d-4338-8c1a-d828e46f799e)

* As we have seen in the command ```  addi    sp, sp, -16 ```, the instruction addi adds the immediate offset to the source register(sp in this case) and stores in the destination register(sp in this case, hence it is overwriting the same register ).
* Now after executing all the instructions we get the output of the ```Ofast``` assembly code.

![Task2_output_Ofast](https://github.com/user-attachments/assets/8b5f5ad9-127f-4e8f-92a2-a875a30d55ae)

Now similarily if we execute the code for ```O1``` compiler:

![task2_O1_output](https://github.com/user-attachments/assets/47e86de5-c4a7-4e33-9dcf-b4e3e7ff6ad0)

* We can see that the command used is ```riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c``` , hence ```O1``` compiler is used.
* Now if we see the assembly language for ```O1``` is

![new_task1_15instr](https://github.com/user-attachments/assets/b0fe01cb-7e90-4f19-8b29-4dfe1ecf5624)

* Again after debugging each instruction we get the same values for the stack pointer as in the ```Ofast``` case.
* At the end of the code, at the address of ```101b4``` the value of the sum is stored.

### Application
--------------------------------

### Modulo Counter -
-------------------------------

A Modulo Counter is a simple digital or software-based counter that increments its value within a fixed range and resets to zero once it reaches a specified maximum. This behavior is widely used in digital systems, embedded applications, and simulation environments to handle cyclic or repetitive operations efficiently.

* The counter starts at an initial value, typically 0
* It increments by a fixed step (usually 1) with each iteration.
* When the counter reaches a predefined maximum value (MODULO), it resets back to 0.
* This cycling behavior ensures the counter remains bounded within a range of 0 to (MODULO - 1).

### C program for the modulo counter (using leafpad)
------------------------------------------------

![c_code_modcount](https://github.com/user-attachments/assets/3c30a03a-080f-4e41-824d-def2cb466d60)

### Output of the C Code in GCC
------------------------------------------------

![modcount_c](https://github.com/user-attachments/assets/810a9d7b-1302-4cc8-8f9c-50dcfce63437)

### Compiling using RISC-V GCC:
------------------------------------------------

![RISC-V_GCC_O1_Ofast](https://github.com/user-attachments/assets/16271517-8739-4918-95da-f05c4fd8fe53)


### Assembly language code for ```O1```:
------------------------------------------------

![modcount_O1_ass_code](https://github.com/user-attachments/assets/7b6c4889-b106-4a66-bdcd-60fa661b46b7)


### Assembly language code for ```Ofast```:
------------------------------------------------

![modcount_Ofast_ass_code](https://github.com/user-attachments/assets/72806583-f8e3-4b46-9299-1238ba4758bc)

### Modulo Counter OUTPUT using ```SPIKE```:
------------------------------------------------

The debugging has been done using the command 
```
spike -d modcount.o
```

![modcount_output_spike](https://github.com/user-attachments/assets/f99fda07-2678-4452-aa02-9fd8327e0d80)


</details>
