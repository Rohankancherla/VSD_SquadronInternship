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
<summary><b>Task 2:</b> Simulating and Debugging C code with SPIKE </summary>   
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
spike -d pk modcount.o
```

![modcount_output_spike](https://github.com/user-attachments/assets/f99fda07-2678-4452-aa02-9fd8327e0d80)


</details>

------------------------------------

<details>
<summary><b>Task 3:</b> RISC-V instruction types </summary>   
<br>

# RISC-V Instruction Types Documentation
------------------------------------------

## Instruction Types Overview
The RISC-V ISA supports several instruction formats, each serving specific functionalities. Below are the instruction types included:

- **R-Type (Register-to-Register)**
- **I-Type (Immediate)**
- **S-Type (Store)**
- **B-Type (Branch)**
- **U-Type (Upper Immediate)**
- **J-Type (Jump)**

Each type includes details such as bit-field ranges, example instructions, operations, and opcode.

## Instruction Formats

### 1. R-Type (Register-to-Register)
**Bit Ranges:**
- `opcode`: [0:6] - Specifies the operation type (e.g., arithmetic, logical).
- `rd`: [7:11] - Destination register.
- `funct3`: [12:14] - Operation specification (e.g., ADD, SUB).
- `rs1`: [15:19] - First source register.
- `rs2`: [20:24] - Second source register.
- `funct7`: [25:31] - Further distinguishes operations (e.g., ADD vs. SUB).

**Example:** `ADD rd, rs1, rs2`

**Operation:** Adds the values in `rs1` and `rs2` and stores the result in `rd`.

**Opcode:** `0110011`

---

### 2. I-Type (Immediate)
**Bit Ranges:**
- `opcode`: [0:6] - Specifies the operation type.
- `rd`: [7:11] - Destination register.
- `funct3`: [12:14] - Operation specification (e.g., ADDI, LOAD).
- `rs1`: [15:19] - Source register.
- `imm`: [20:31] - Immediate value (12-bit).

**Example:** `ADDI rd, rs1, imm`

**Operation:** Adds the immediate value `imm` to `rs1` and stores the result in `rd`.

**Opcode:** `0010011`

---

### 3. S-Type (Store)
**Bit Ranges:**
- `opcode`: [0:6] - Specifies the operation type.
- `imm[4:0]`: [7:11] - Immediate value (lower bits).
- `funct3`: [12:14] - Operation specification (e.g., STORE).
- `rs1`: [15:19] - Base register.
- `rs2`: [20:24] - Source register.
- `imm[11:5]`: [25:31] - Immediate value (upper bits).

**Example:** `SW rs2, imm(rs1)`

**Operation:** Stores the value in `rs2` into the memory address computed as `rs1 + imm`.

**Opcode:** `0100011`

---

### 4. B-Type (Branch)
**Bit Ranges:**
- `opcode`: [0:6] - Specifies the operation type.
- `imm[11]`: [7] - Immediate bit.
- `imm[4:1]`: [8:11] - Immediate bits (lower).
- `funct3`: [12:14] - Branch operation specification (e.g., BEQ, BNE).
- `rs1`: [15:19] - First source register.
- `rs2`: [20:24] - Second source register.
- `imm[10:5]`: [25:30] - Immediate bits (middle).
- `imm[12]`: [31] - Immediate bit (upper).

**Example:** `BEQ rs1, rs2, imm`

**Operation:** Branches to the address `PC + imm` if `rs1` equals `rs2`.

**Opcode:** `1100011`

---

### 5. U-Type (Upper Immediate)
**Bit Ranges:**
- `opcode`: [0:6] - Specifies the operation type.
- `rd`: [7:11] - Destination register.
- `imm`: [12:31] - Immediate value.

**Example:** `LUI rd, imm`

**Operation:** Loads the immediate value `imm` shifted left by 12 bits into `rd`.

**Opcode:** `0110111`

---

### 6. J-Type (Jump)
**Bit Ranges:**
- `opcode`: [0:6] - Specifies the operation type.
- `rd`: [7:11] - Destination register.
- `imm[20]`: [12] - Immediate bit.
- `imm[10:1]`: [13:22] - Immediate bits (lower).
- `imm[11]`: [23] - Immediate bit.
- `imm[19:12]`: [24:31] - Immediate bits (upper).

**Example:** `JAL rd, imm`

**Operation:** Jumps to the address `PC + imm` and stores the return address in `rd`.

**Opcode:** `1101111`

---

The below image shows the various RISC-V instruction types

![image](https://github.com/user-attachments/assets/2ef09cf5-ad58-4fd0-ac5e-8f692e04ce34)


THe given below table illustrates the 15 differnt instruction used in the application ( **modulo counter**) :

| **Address** | **Instruction**     | **Explanation**                                                  |
| ----------- | ------------------- | ---------------------------------------------------------------- |
| `fc010113`  | `addi sp, sp, -64`  | Adjust the stack pointer (`sp`) to allocate 64 bytes on the stack. |
| `02913423`  | `sd s1, 40(sp)`     | Store the value of register `s1` into memory at `sp + 40`.        |
| `05f5e4b7`  | `lui s1, 0x5f5e`    | Load the upper 20 bits of register `s1` with the immediate value `0x5f5e`. |
| `00000413`  | `li s0, 0`          | Load the immediate value `0` into register `s0`.                  |
| `00040593`  | `mv a1, s0`         | Copy the value from register `s0` into register `a1`.             |
| `3a0000ef`  | `jal ra, 10484`     | Jump to address `10484` and store the return address in register `ra`. |
| `0014041b`  | `addiw s0, s0, 1`   | Add the immediate value `1` to `s0` and store the result in `s0`. |
| `00813783`  | `ld a5, 8(sp)`      | Load a 64-bit value from memory at address `sp + 8` into `a5`.     |
| `fe079ae3`  | `bnez a5, 100f0`    | Branch to address `100f0` if the value in `a5` is not zero.        |
| `fd241ee3`  | `bne s0, s2, 100dc` | Branch to address `100dc` if the value in `s0` is not equal to `s2`. |
| `ffff0797`  | `auipc a5, 0xffff0` | Add the 20-bit immediate value `0xffff0` to the program counter (PC) and store the result in `a5`. |
| `00078863`  | `beqz a5, 10148`    | Branch to address `10148` if the value in `a5` is zero.            |
| `0e80006f`  | `j`                 | Perform an unconditional jump to a computed address.               |
| `00012503`  | `lw a0, 0(sp)`      | Load a 32-bit word from memory at address `sp + 0` into `a0`.      |
| `78f18c23`  | `sb a5, 1944(gp)`   | Store the least significant byte of `a5` into memory at address `gp + 1944`. |



