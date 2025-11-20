# Modified Mano Basic Computer (VHDL)

**Course:** Computer Architecture
**Instructor:** Dr. Shariatmadar Mortazavi
**Institution:** Amirkabir University of Technology
**Semester:** 1401-1402 (Second Semester)

## 📖 Project Overview
[cite_start]This repository contains the VHDL implementation of "Project 1: Basic Computer"[cite: 2, 6]. This design is a modified version of the standard M. Morris Mano Basic Computer. [cite_start]Unlike the standard Von Neumann architecture, this implementation utilizes a modified architecture with separate memory units for instructions and data to simplify the design process[cite: 10, 11].

### Key Features
* **Split Memory Architecture:**
    * [cite_start]**ROM:** Stores program instructions (Read-Only)[cite: 11].
    * [cite_start]**RAM:** Stores data variables (Read/Write)[cite: 11].
* [cite_start]**4-State Control Logic:** Implements a Finite State Machine (FSM) synchronized by a system clock[cite: 15].
* [cite_start]**Custom ALU Modules:** Integrates custom hardware for Multiplication and Square Root operations[cite: 39].

---

## ⚙️ System Architecture

### 1. Block Diagram
The system follows a bus-oriented architecture connecting the Memory Units (RAM/ROM), the Register Set, and the ALU.



[Image of Morris Mano Basic Computer block diagram]

*Note: While the standard diagram above shows a single Memory unit, this project physically splits it into RAM and ROM components.*

### 2. Memory Organization
* [cite_start]**Instruction Word:** 16 bits total[cite: 34].
    * [cite_start]**Opcode:** 6 bits (Bits 15-10)[cite: 36].
    * [cite_start]**Address:** 10 bits (Bits 9-0)[cite: 35].
* **RAM Size:** Although the address bus supports 10 bits ($1024$ locations), the physical implementation utilizes a $64 \times 16$ block. [cite_start]Address inputs are padded with zeros to maintain structural integrity[cite: 48].

### 3. Registers
[cite_start]The design includes the following essential registers[cite: 28, 29, 22]:
* **AC (Accumulator):** 16-bit main processor register.
* **E (Extension):** 1-bit register to store Carry/Overflow.
* **PC (Program Counter):** Holds the address of the next instruction in ROM.
* **DR (Data Register):** Stores the operand read from RAM.

### 4. Finite State Machine (FSM)
[cite_start]The Control Unit operates on a 4-state cycle synchronized by the clock[cite: 15]:



1.  [cite_start]**Fetch:** Reads the instruction from ROM based on the PC value[cite: 23].
2.  [cite_start]**Decode:** Decodes the Opcode to determine the operation[cite: 24].
3.  [cite_start]**Read Operand:** If the instruction requires memory access, data is read from RAM into the DR[cite: 25].
4.  [cite_start]**Execute:** The ALU performs the operation (Logic, Arithmetic, Shift)[cite: 27].

---

## 📝 Instruction Set Architecture (ISA)

The computer supports 16 specific instructions.

| Instruction | Opcode (Binary) | Address Req? | Description |
| :--- | :--- | :--- | :--- |
| **AND** | `000001` | Yes | [cite_start]AC ← AC ∧ RAM[Addr] [cite: 38] |
| **STORE** | `000010` | Yes | [cite_start]RAM[Addr] ← AC [cite: 38] |
| **LOAD** | `000011` | Yes | [cite_start]AC ← RAM[Addr] [cite: 38] |
| **ADD** | `000100` | Yes | [cite_start]AC ← AC + RAM[Addr], E ← Carry [cite: 38] |
| **INC** | `000101` | No | [cite_start]AC ← AC + 1 [cite: 38] |
| **CLA** | `000110` | No | [cite_start]AC ← 0 [cite: 38] |
| **CLE** | `000111` | No | [cite_start]E ← 0 [cite: 38] |
| **CIR L** | `001000` | No | [cite_start]Circular Left Shift (AC & E) [cite: 38] |
| **CIR R** | `001001` | No | [cite_start]Circular Right Shift (AC & E) [cite: 38] |
| **SPA** | `001010` | No | [cite_start]Skip if AC is Positive [cite: 38] |
| **SNA** | `001011` | No | [cite_start]Skip if AC is Negative [cite: 38] |
| **SZE** | `001100` | No | [cite_start]Skip if E is Zero [cite: 38] |
| **SZA** | `001101` | No | [cite_start]Skip if AC is Zero [cite: 38] |
| **SHL** | `001110` | No | [cite_start]Linear Left Shift [cite: 38] |
| **SHR** | `001111` | No | [cite_start]Linear Right Shift [cite: 38] |
| **MUL** | `010000` | Yes | [cite_start]Multiply (Custom Module) [cite: 38] |
| **SQR** | `100000` | Yes | [cite_start]Square Root (Custom Module) [cite: 38] |

### Custom Instructions Details
* **Multiply:** Uses a 6-bit × 6-bit multiplier. [cite_start]The 12-bit output is zero-padded to 16 bits and stored in the AC[cite: 40].
* **SQR:** Uses a 16-bit input square root module. [cite_start]The 8-bit output is zero-padded to 16 bits[cite: 41].

---

## 📂 File Structure
* `RAM.vhd` - Data memory implementation (Read/Write).
* `ROM.vhd` - Instruction memory (Read-Only, pre-loaded with instructions).
* `ALU.vhd` - Arithmetic Logic Unit (Contains logic for AND, ADD, Shifts, MUL, SQR).
* `ControlUnit.vhd` - FSM implementation (Fetch, Decode, Read, Execute).
* `Computer.vhd` - Top-level entity connecting the bus, memory, and CPU.
* `Multiplier.vhd` - 6-bit multiplier component.
* `Sqrt.vhd` - 16-bit square root component.

## 🚀 Usage & Simulation
[cite_start]*(Note: No Testbench is required for final submission as RAM/ROM are modified directly to test sequences[cite: 44].)*

1.  [cite_start]**Load Instructions:** Manually modify the array content in `ROM.vhd` with your binary opcodes[cite: 11].
2.  **Simulation:** Open the project in your VHDL simulator (e.g., ModelSim, Vivado, ISE).
3.  **Observation:**
    * Run the simulation for the required clock cycles.
    * Observe the **AC** signal to see calculation results.
    * Observe the **State** signal to verify the 4-step transition cycle.

## 👥 Contributors
* **[Your Name]**: [List specific parts implemented]
* **[Partner Name]**: [List specific parts implemented]

---
*Project completed in accordance with the requirements set for Project 1, Spring 2023.*
To synthesise the VHDL code, add the following files to the project:
* `computer.vhd`
* `alu.vhd`
* `control.vhd`
* `register.vhd`
* `AC.vhd`
* `IR.vhd`
* `AR.vhd`
* `PC.vhd`
* `DR.vhd`
* `RAM.vhd`
* `ROM.vhd`
* `E.vhd`
* `arraymulty.vhd`
* `SC.vhd`
* `FA.vhd`
* `ripple_adder16bit.vhd` 
DO <span style="color:red">NOT</span> add `ripple_adder.vhd` to the project.
* `sqrt.vhd` (you also need to add all of the files in the `sqrtsub` folder to the project witch includes:
1. `case.vhd`
2. `fulladder.vhd`
3. `halfadder.vhd`
4. `x_mod.vhd`
5. `y_mod.vhd`

To simulate the VHDL code, do the following:
1. Reset the simulation.
2. After starting the simulation, force a clock signal to 
clk (it's better to have it start with a 0).
1. change the colour of the signal: <span style="color:cyan">AC_out</span> since it is the signal we need to monitor to see the functionality of the computer.
2. Run the simulation for  4 * "Number of instructions" 
3. $AC_{out}$ will show everyting as it's the main regester for every instruction.
