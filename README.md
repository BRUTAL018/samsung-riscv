# samsung-riscv
this program is based on RISC-V architecture and uses open source tools to teach people about VLSI chipdesign and RISC-V<br>

**Name:** Yashas.B.R <br>
**College:** SJB Institue Of Technology <br>
**Email ID:** yashasksy@gmail.com <br>
**GitHub Profile:** [BRUTAL018](https://github.com/BRUTAL018) <br>  

-------------------------------------------------
<details>
<summary><b>Task 1:</b> Task is to refer to C based and RISCV based lab videos and execute the task of compiling the C code using gcc and riscv compiler</summary>

### C Language based LAB
We have to follow the given steps to compile any **.c** file in our machine:  
1. Open the terminal and access the leafpad file in which we code the c program. To open leapad run the following command:

	```
	leafpad sumn.c
	```  
2. This will open the editor and allows you to write into the file that you have created. You have to write the C code of printing the sum of n numbers. Once you are done with your code, press ```Ctrl + S``` to save your file, and then press ```Ctrl + W``` to close the editor.   
3. To the C code on your terminal, run the following command:

	```
	gcc sumn.c
	./a.out
	```
![C Code compiled on gcc Compiler](https://github.com/BRUTAL018/samsung-riscv/blob/main/task1/1.png)

### RISCV based LAB
We have to do the same compilation of our code but this time using RISCV gcc compiler. Follow the given steps:  
1. Open the terminal and run the given command:  

	```
	cat sumn.c
	```
![cat Command](https://github.com/BRUTAL018/samsung-riscv/blob/main/task1/2.png)

2. Using the **cat** command, the entire C code will be displayed on the terminal. Now run the following command to compile the code in riscv64 gcc compiler:  

	```
	riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sumn.o sumn.c
	```
3. Open a new terminal and run the given command:    

	```
	riscv64-unknown-elf-objdump -d sumn.o
	```
![Objdump using -O1 format](https://github.com/BRUTAL018/samsung-riscv/blob/main/task1/3.png)

4. The Assembly Language code of our C code will be displayed on the terminal. Type ```/main``` to locate the main section of our code.  

### *Descriptions of the keyword used in above command*  
* **-mabi=lp64:** This option specifies the ABI (Application Binary Interface) to use ```lp64```, which is for 64-bit integer, long and pointer size. This ABI is used for 64-bit RISCV architecture.  
* **-march=rv64i:** This option specifies the architecture that we use, which is rv64i, indicates the 64-bit RISCV base integer instruction set. This also confirms the targeting of 64-bit architecture.  
* **riscv-objdump:** A tool for disassembling RISC-V binaries, providing insights into the code structure and helping in debugging.  
* **-Ofast:** The option -Ofast in the command ```riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sumn.o sumn.c``` is a compiler optimization flag used with the GNU Compiler Collection (GCC). This flag is used to instruct the compiler to optimize the generated code for maximum speed. The use of ```-Ofast``` is typically chosen for applications where execution speed is critical and where deviations from standard behavior are acceptable. However, it's important to test thoroughly, as this level of optimization can introduce subtle bugs, especially in complex calculations or when strict compliance with external standards is required.  
* **-O1:** This options is an optimization level that tells the compiler to optimize the generated code but without greatly increasing compilation time. -O1 aims to reduce code size and execution time while keeping the compilation process relatively quick.  

#### *Other common options are as follows:*  
> 1. **-O0:** No optimization, the default level if no -O option is specified.  
> 2. **-O2:** More aggressive optimizations that might increase compilation time but typically provide faster and sometimes smaller code.  
> 3. **-O3:** Maximizes optimization more aggressively than -O2.  
> 4. **-Os:** Optimizes code for size. It enables all -O2 optimizations that do not typically increase code size.

Here, the term **more aggressive optimization** in the context of compilers like GCC refers to a deeper and more complex set of transformations applied to the code in order to improve its performance and possibly reduce its size. The compiler uses more complex techniques that aims to generate faster executing code or code that occupies less memory. However, these optimizations typically increase the compilation time and can sometimes introduce bugs, making it harder to debug.
</details>

-------------------------------------------------
<details>
<summary><b>Task 2:</b> Performing SPIKE Simulation and Debugging the C code </summary> 

### What is SPIKE in RISCV?
> * A RISC-V ISA is a simulator, enabling the testing and analysis of RISC-V programs without the need for actual hardware.  
> * Spike is a free, open-source C++ simulator for the RISC-V ISA that models a RISC-V core and cache system. It can be used to run programs and a Linux kernel, and can be a starting point for running software on a RISC-V target.  
  
### What is pk (Proxy Kernel)?  
> * The RISC-V Proxy Kernel, pk , is a lightweight application execution environment that can host statically-linked RISC-V ELF binaries.  
> * A Proxy Kernel in the RISC-V ecosystem simplifies the interaction between complex hardware and the software running on it, making it easier to manage, test, and develop software and hardware projects.  


### Testing the SPIKE Simulator  
The target is to run the ```sumn.c``` code using both ```gcc compiler``` and ```riscv compiler```, and both of the compiler must display the same output on the terminal. So to compile the code using **gcc compiler**, use the following command:  
```
gcc sumn.c  
./a.out
```
And to compile the code using **riscv compiler**, use the following command:  
```
spike pk sumn.o
```  
![Spike Simulation](https://github.com/BRUTAL018/samsung-riscv/blob/main/task2/2.11.png)

#### Following are the snapshots of RISCV Objdump with **-O1** and **-Ofast** options  
RISCV Objdump with -O1 option  

![Objdump in -O1](https://github.com/BRUTAL018/samsung-riscv/blob/main/task2/2.3o.png)

RISCV Objdump with -Ofast option  

![Objdump in -Ofast](https://github.com/BRUTAL018/samsung-riscv/blob/main/task2/2.2ofast.png)

### Debugging the Assembly Language Program of  ```sumn.c```  
* Open the **Objdump** of code by using the following command  
```
$ riscv64-unknown-elf-objdump -d sumn.o | less  
```
* Open the debugger in another terminal by using the following command  
```
$ spike -d pk sumn.o
```
* The debugger will be opened in the terminal. Now, debugging operations can be performed as shown in the following snapshot.

![Debugging](https://github.com/BRUTAL018/samsung-riscv/blob/main/task2/2.4.png) 
</details>

-------------------------------------------------

<details>
<summary><b>Task 3:</b> Task is to identify instruction type of all the given instructions with its exact 32 bits instruction code in the desired instruction type format</summary>

1. #### Instruction: `addi sp, sp, -128`
- **Opcode:** 0010011 (7 bits)
- **Immediate:** -128 (12 bits, two's complement)
- **Source Register (rs1):** sp (x2, 5 bits)
- **Destination Register (rd):** sp (x2, 5 bits)
- **Function (funct3):** 000 (3 bits)
#### Breakdown:
- **Immediate (-128):** `111111110000`
- **rs1 (sp = x2):** `00010`
- **funct3:** `000`
- **rd (sp = x2):** `00010`
- **Opcode:** `0010011`
- **32 bits instruction :** ```0000000_00001_00010_000_00110_0110011```
- 
### Machine Code Breakdown for `addi sp, sp, -128`
| Immediate (12 bits) | rs1 (5 bits) | funct3 (3 bits) | rd (5 bits) | Opcode (7 bits) |
|---------------------|--------------|-----------------|-------------|-----------------|
| 111111110000        | 00010        | 000             | 00010       | 0010011         |
![image](https://github.com/user-attachments/assets/51869d32-1bc8-45b6-b559-9682c34ed699)
2. ### `sd s0, 112(sp)`
*sd (Store Doubleword):* This instruction stores a 64-bit value from a source register into memory.
#### Instruction: `sd s0, 112(sp)`
- **Opcode:** 0100011 (7 bits)
- **Immediate:** 112 (12 bits, split into two parts: imm[11:5] and imm[4:0])
- **Source Register (rs2):** s0 (x8, 5 bits)
- **Base Register (rs1):** sp (x2, 5 bits)
- **Function (funct3):** 011 (3 bits)
#### Breakdown:
- **Immediate (112):** `000001110000` (split into imm[11:5] = `0000011` and imm[4:0] = `10000`)
- **rs2 (s0 = x8):** `01000`
- **rs1 (sp = x2):** `00010`
- **funct3:** `011`
- **Opcode:** `0100011`
#### Binary Representation:
- imm[11:5] (7 bits): `0000011`
- rs2 (5 bits): `01000`
- rs1 (5 bits): `00010`
- funct3 (3 bits): `011`
- imm[4:0] (5 bits): `10000`
- Opcode (7 bits): `0100011`
- **32 bits instruction :** ```0000000_00001_00010_000_00110_0110011```   
### Machine Code Breakdown for `sd s0, 112(sp)`
| imm[11:5] (7 bits) | rs2 (5 bits) | rs1 (5 bits) | funct3 (3 bits) | imm[4:0] (5 bits) | Opcode (7 bits) |
|--------------------|--------------|--------------|-----------------|-------------------|-----------------|
| 0000011            | 01000        | 00010        | 011             | 10000             | 0100011         |
![image](https://github.com/user-attachments/assets/ac5766fd-7b6d-4b2f-afdb-a66c8fb92b70)
**mv a5, a0**
3. ### Machine Code for `mv a5, a0`
#### Instruction: `mv a5, a0`
- **Opcode:** 0010011 (7 bits)
- **Immediate:** 0 (12 bits)
- **Source Register (rs1):** a0 (x10, 5 bits)
- **Destination Register (rd):** a5 (x15, 5 bits)
- **Function (funct3):** 000 (3 bits)
#### Breakdown:
- **Immediate (0):** `000000000000`
- **rs1 (a0 = x10):** `01010`
- **funct3:** `000`
- **rd (a5 = x15):** `01111`
- **Opcode:** `0010011`
     ```
     imm[11:0]  | rs1  | funct3 | rd   | opcode
     000000000000 | 01000 | 000   | 10111 | 0010011
     ```


  
4.   ### Machine Code for `ld a0, -32(s0)`

#### Instruction: `ld a0, -32(s0)`
- **Opcode:** 0000011 (7 bits)
- **Immediate:** -32 (12 bits, two's complement)
- **Source Register (rs1):** s0 (x8, 5 bits)
- **Destination Register (rd):** a0 (x10, 5 bits)
- **Function (funct3):** 011 (3 bits)

#### Breakdown:
- **Immediate (-32):** `111111000000`
- **rs1 (s0 = x8):** `01000`
- **funct3:** `011`
- **rd (a0 = x10):** `01010`
- **Opcode:** `0000011`
- 
     ```
      imm[11:5] | rs2   | rs1  | funct3 | imm[4:0] | opcode
      1111110  | 01010 | 01000 | 011   | 00000 | 0100011
      ```
       


5.  #### Instruction: `lui a5, 0x24`
- **Opcode:** 0110111 (7 bits)
- **Immediate:** 0x24 (20 bits)
- **Destination Register (rd):** a5 (x15, 5 bits)

#### Breakdown:
- **Immediate (20 bits):** `00000000000000000000 00100100`
- **rd (a5 = x15):** `01111`
- **Opcode:** `0110111`

#### Machine Code:
- **Binary:** `00000000000000000000 01111 0110111`
- **Hex:** `000247b7`

       ```
      imm[31:12] | rd   | opcode
      000000100010 | 10111 | 0110111
      ```

6. ### Machine Code for `sw a5, -116(s0)`

#### Instruction: `sw a5, -116(s0)`
- **Opcode:** 0100011 (7 bits)
- **Immediate:** -116 (split into 7 bits and 5 bits)
- **Source Register 1 (rs1):** s0 (x8, 5 bits)
- **Source Register 2 (rs2):** a5 (x15, 5 bits)
- **Function (funct3):** 010 (3 bits)

#### Breakdown:
- **Immediate [11:5] (-116):** `1111100`
- **rs2 (a5 = x15):** `01111`
- **rs1 (s0 = x8):** `01000`
- **funct3:** `010`
- **Immediate [4:0] (-116):** `00000`
- **Opcode:** `0100011`

#### Machine Code:
- **Binary:** `1111100 01111 01000 010 00000 0100011`
- **Hex:** `f8f42623`


7.  ### Machine Code for `ld a0, -32(s0)`

#### Instruction: `ld a0, -32(s0)`
- **Opcode:** 0000011 (7 bits)
- **Immediate:** -32 (12 bits, two's complement)
- **Source Register (rs1):** s0 (x8, 5 bits)
- **Destination Register (rd):** a0 (x10, 5 bits)
- **Function (funct3):** 011 (3 bits)

#### Breakdown:
- **Immediate (-32):** `111111000000`
- **rs1 (s0 = x8):** `01000`
- **funct3:** `011`
- **rd (a0 = x10):** `01010`
- **Opcode:** `0000011`

      ```
      imm[11:0]  | rs1  | funct3 | rd   | opcode
      111111000000 | 01000 | 011   | 01010 | 0000011
      ```

8.  ### Machine Code for `jal ra, 1038c <Layer_create>`

#### Instruction: `jal ra, 1038c <Layer_create>`
- **Opcode:** 1101111 (7 bits)
- **Immediate:** 0x1038c (20 bits)
- **Destination Register (rd):** ra (x1, 5 bits)

#### Breakdown:
- **Immediate (20 bits):** `0001000 0111000 1100` (splits into multiple parts for encoding)
- **rd (ra = x1):** `00001`
- **Opcode:** `1101111`

       ```
      imm[20|10:1|11|19:12] | rd   | opcode
      100001000000| 00001 | 1101111
      ```

9. **sd a0, -32(s0)**
    - **Machine Code:** `fea43023`
    - **Breakdown:**
      ```
      imm[11:5] | rs2   | rs1  | funct3 | imm[4:0] | opcode
      1111110  | 01010 | 01000 | 011   | 00000 | 0100011
      ```

10. **li a1, 2**
    - **Machine Code:** `00200593`
    - **Breakdown:**
      ```
      imm[11:0]  | rs1  | funct3 | rd   | opcode
      000000000010 | 00000 | 000   | 01011 | 0010011
      ```
11.  **jal ra, 13ba4 <srand>**
   - **Machine Code:** `065020ef`
   - **Breakdown:**
     ```
     imm[20|10:1|11|19:12] | rd   | opcode
     000001100101| 00010 | 1101111
     ```


12. **jal ra, 10740 <Layer_dump>**
    - **Machine Code:** `bbcff0ef`
    - **Breakdown:**
      ```
      imm[20|10:1|11|19:12] | rd   | opcode
      101111101111| 00001 | 1101111
      ```

13. **sd s0, 112(sp)**
   - **Machine Code:** `06813823`
   - **Breakdown:**
     ```
     imm[11:5] | rs2   | rs1  | funct3 | imm[4:0] | opcode
     0000011  | 01000 | 00010 | 011   | 10000 | 0100011
     ```
14.  **jal ra, 10740 <Layer_dump>**
    - **Machine Code:** `bbcff0ef`
    - **Breakdown:**
      ```
      imm[20|10:1|11|19:12] | rd   | opcode
      101111101111| 00001 | 1101111
      ```       

15.  ** jal  ra,11024 <Layer_learnOutputs>**
      - **Immediate (20 bits)**: `00101011 100000 0 0`
      - **rd (ra = x1)**: `00001`
      - **Opcode**: `1101111`
        ```
        imm[20|10:1|11|19:12] | rd | opcode
         0 0001000000 1 00101011 | 00001 | 1101111
        ```
        </details>
--------
<details>
<summary><b>Task 4:</b> To perform an experiment of Functional Simulation and observe the waveforms of the instructions with the help of RISCV CORE, Netlist and Testbench. </summary>
	
### About iverilog and gtkwave
- Icarus Verilog is an implementation of the Verilog hardware description language.
- GTKWave is a fully featured GTK+ v1. 2 based wave viewer for Unix and Win32 which reads Ver Structural Verilog Compiler generated AET files as well as standard Verilog VCD/EVCD files and allows their viewing.
---

### Installing iverilog and gtkwave

- **For Ubuntu**
 1. Open your terminal and type the following to install iverilog and GTKWave
 ```
 $   sudo apt update
 $   sudo apt install iverilog gtkwave
 ```
2. Create a new directory with your name ```mkdir <your_name>```
3. Create two files by using ```touch``` command as ```yashasbr_rv32i.v``` and ```yashasbr_rv32i_tb.v```  
4. Copy the code from the [FILE](https://github.com/vinayrayapati/rv32i) and paste it in your verilog netlist and testbench files 
  
  
5. To run and simulate the verilog code, enter the following command:  
	```
	$ iverilog -o chethas_rv32i.out yashasbr_rv32i_tb.v yashasbr_rv32i_tb.v
	$ vvp chethas_rv32i.out
	```
6. To see the output simulation waveform in GTKWave, enter the name of dump file in the command:
	```
	$ gtkwave iiitb_rv32i.vcd
	```
 
 ---

 
#### All the instructions in the given verilog file is hard-coded. Hard-coded means that instead of following the RISCV specifications bit pattern, the designer has hard-coded each instructions based on their own pattern. Hence the 32-bits instruction that we generated in Task-3 will not match with the given instruction.  
  
<img width="500" alt="Instructions" src="https://github.com/BRUTAL018/samsung-riscv/blob/main/task4/stdarchitecture/Instructions%20list.png">

  
#### Following are the differences between standard RISCV ISA and the Instruction Set given in the reference repository:  

|  **Operation**  |  **Standard RISCV ISA**  |  **Hardcoded ISA**  |  
|  :----:  |  :----:  |  :----:  |  
|  ADD R6, R2, R1  |  32'h00110333  |  32'h02208300  |  
|  SUB R7, R1, R2  |  32'h402083b3  |  32'h02209380  |  
|  AND R8, R1, R3  |  32'h0030f433  |  32'h0230a400  |  
|  OR R9, R2, R5  |  32'h005164b3  |  32'h02513480  |  
|  XOR R10, R1, R4  |  32'h0040c533  |  32'h0240c500  |  
|  SLT R1, R2, R4  |  32'h0045a0b3  |  32'h02415580  |  
|  ADDI R12, R4, 5  |  32'h004120b3  |  32'h00520600  |  
|  BEQ R0, R0, 15  |  32'h00000f63  |  32'h00f00002  |  
|  SW R3, R1, 2  |  32'h0030a123  |  32'h00209181  |  
|  LW R13, R1, 2  |  32'h0020a683  |  32'h00208681  |  
|  SRL R16, R14, R2  |  32'h0030a123  |  32'h00271803  |
|  SLL R15, R1, R2  |  32'h002097b3  |  32'h00208783  |  

  ---
  
## *Analysing the Output Waveform of various instructions that we have covered in TASK-3*  
**```Instruction 1: ADD R6, R2, R1```**  

![image](https://github.com/BRUTAL018/samsung-riscv/blob/main/task4/snapshots/ADD_R6%2CR2%2CR1.png)

**```Instruction 2: SUB R7, R1, R2```**  
  
![image](https://github.com/BRUTAL018/samsung-riscv/blob/main/task4/snapshots/SUB_R7%2CR1%2CR2.jpg)

**```Instruction 3: AND R8, R1, R3```**  

![image](https://github.com/BRUTAL018/samsung-riscv/blob/main/task4/snapshots/AND_R8%2CR1%2CR3.png)


**```Instruction 4: BNE R0, R0, R15```**  

![image](https://github.com/BRUTAL018/samsung-riscv/blob/main/task4/snapshots/BNE_R0%2CR0%2C15.png)


**```Instruction 5: XOR R10, R1, R4```**  

![image](https://github.com/BRUTAL018/samsung-riscv/blob/main/task4/snapshots/XOR_R10%2CR1%2CR4.jpg)


**```Instruction 6: SLT R1, R2, R4```**  

![image](https://github.com/BRUTAL018/samsung-riscv/blob/main/task4/snapshots/SLT_R1%2CR2%2CR4.jpg)


**```Instruction 7: ADDI R12, R4, 5```**  

![image](https://github.com/BRUTAL018/samsung-riscv/blob/main/task4/snapshots/ADDI_R12%2CR4%2C5.png)


**```Instruction 8: BEQ R0, R0, 15```**  
  
![image](https://github.com/BRUTAL018/samsung-riscv/blob/main/task4/snapshots/BEQ_R0%2CR0%2C15.png)

 
**```Instruction 9: SW R3, R1, 2```**

![image](https://github.com/BRUTAL018/samsung-riscv/blob/main/task4/snapshots/SW_R3%2CR1%2C2.jpg)

  
**```Instruction 10: LW R13, R1, 2```**  

![image](https://github.com/BRUTAL018/samsung-riscv/blob/main/task4/snapshots/LW_R13%2CR1%2C2.jpg)

 </details>
 
-------
<details>
<summary><b>Task 5: </b>Implementing a project using VSDSquadron Mini and check whether the building and uploading of C program file on RISCV processor works. </summary>

 ## Motion Detection System Using PIR Sensor and VSDSQuadron Mini

###**Overview**  
The project aims to create a motion detection system using a Passive Infrared (PIR) sensor and the VSDsquadron Mini Board. When motion is detected by the PIR sensor, the system activates an LED to indicate the presence of motion.
* **Detection** : The PIR sensor continuously monitors its surroundings for any movement. When it detects motion, it sends a signal to the VSDsquadron Mini Board.
* **Processing** : The VSDsquadron Mini Board receives the signal from the PIR sensor and processes it using its onboard microcontroller.
* **LED Activation** : Upon detecting motion, the microcontroller activates the LED connected to it, illuminating it to indicate the presence of motion.

### **Components Required**  
*PIR Sensor
*VSDSquadron Mini Board
*LED
*Jumper wire(Female to FEmale)
*VS Code for uploading the code in which PLATFORM IO installation should be there.

### **Hardware Connections**  
PIR CONNECTIONS
*Output Pin of PIR connected to PD2 Of VSDSquadron Mini Board.
*VCC Of PIR coonected to 5V Of VSDSquadron Mini Board.
*GND Pin of PIR connected to GND Of VSDSquadron Mini Board.

LED CONNECTION
*LED Anode Pin connected to PD6 Of VSDSquadron Mini Board.
*LED Cathode connected to GND Of VSDSquadron Mini Board.

### **code**
```
#include <ch32v00x.h>
#include <debug.h>

#define BLINKY_GPIO_PORT GPIOD
#define BLINKY_GPIO_PIN GPIO_Pin_6
#define PIR_GPIO_PIN GPIO_Pin_2 // PIR sensor output connected to GPIO Pin 2
#define BLINKY_CLOCK_ENABLE RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE)

void NMI_Handler(void) _attribute_((interrupt("WCH-Interrupt-fast")));
void HardFault_Handler(void) _attribute_((interrupt("WCH-Interrupt-fast")));
void Delay_Init(void);
void Delay_Ms(uint32_t n);

int main(void)
{
    NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);
    SystemCoreClockUpdate();
    Delay_Init();
    GPIO_InitTypeDef GPIO_InitStructure = {0};
    BLINKY_CLOCK_ENABLE;
    GPIO_InitStructure.GPIO_Pin = BLINKY_GPIO_PIN;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(BLINKY_GPIO_PORT, &GPIO_InitStructure);
    // Configure PIR sensor input pin
    GPIO_InitStructure.GPIO_Pin = PIR_GPIO_PIN;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU; // Input mode with pull-up
    GPIO_Init(GPIOD, &GPIO_InitStructure);
    while (1)
    {
        // Read PIR sensor status
        uint8_t pirStatus = GPIO_ReadInputDataBit(GPIOD, PIR_GPIO_PIN);
	// Control the LED based on PIR sensor output
        if (pirStatus == 1) // PIR sensor detected motion
        {
            GPIO_WriteBit(BLINKY_GPIO_PORT, BLINKY_GPIO_PIN, SET); // Turn on LED
        }
        else
        {
            GPIO_WriteBit(BLINKY_GPIO_PORT, BLINKY_GPIO_PIN, RESET); // Turn off LED
        }
	Delay_Ms(1000);
    }
}

void NMI_Handler(void) {}
void HardFault_Handler(void)
{
    while (1)
    {
    }
}
```
