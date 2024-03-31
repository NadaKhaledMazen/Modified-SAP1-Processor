# Modified Simple-As-Possible (SAP1) Processor

## Summary

A Modified Simple-As-Possible (SAP1) Processor is implemented here. Its instruction size is 8 bits with a memory unit of size 16x8. The processor executes Memory instructions, including both Memory-Reference and Register-Reference instructions. The processor components include the Control Unit, Memory, Arithmetic Logic Unit (ALU), Bus, Program Counter (PC), Address Register (AR), Instruction Register (IR), Accumulator (AC), Data Register (DR), Temporary Register (TR), Input Register (INPR), and Output Register (OUTR).

## Methodology

- The code includes a main module containing the processor's outputs, component declarations, signal declarations, and port mappings.
- The Control Unit is a Finite State Machine (FSM) controlling the instruction cycle (Fetching – Decoding - Execution).
- Memory stores instructions and operands.
- ALU performs arithmetic and logical operations.
- Bus connects components.
- PC points to the next instruction.
- AR holds instruction addresses.
- IR stores the currently executed instruction.
- AC stores data for operations.
- DR holds data from memory.
- TR holds temporary data.
- INPR receives external data.
- OUTR stores data for output.

## Features

- 16x8 Memory unit.
- Memory-Reference Instruction Set:
  
  | Instruction | Opcode | Machine Language | Micro-operation                                   |
  |-------------|--------|------------------|---------------------------------------------------|
  | AND         | 000    | <Address Mode>000| T4: DR ← M[AR], T5: AC ← AC AND DR               |
  | ADD         | 001    | <Address Mode>001| T4: DR ← M[AR], T5: AC ← AC + DR                 |
  | LDA         | 010    | <Address Mode>010| T4: DR ← M[AR], T5: AC ← DR                      |
  | STA         | 011    | <Address Mode>011| T4: M[AR] ← AC                                    |
  | BUN         | 100    | <Address Mode>100| T4: PC ← AC                                       |
  | BSA         | 101    | <Address Mode>101| T4: M[AR] ← PC, AR ← AR + 1, T5: PC ← AR          |
  | ISZ         | 110    | <Address Mode>110| T4: DR ← M[AR], T5: DR ← DR + 1, T6: M[AR] ← DR, If (DR = 0) then (PC ← PC + 1) |

- Register-Reference Instruction Set:

  | Instruction | Opcode | Machine Language | Micro-operation                                   |
  |-------------|--------|------------------|---------------------------------------------------|
  | HLT         | 0001   | X111<Address "Opcode"> | T3: NextState ← PresentState            |
  | SZA         | 0010   | X111<Address "Opcode"> | T3: If (AC = 0) then (PC ← PC + 1)       |
  | SNA         | 0011   | X111<Address "Opcode"> | T3: If (AC(15) = 1) then (PC ← PC + 1)   |
  | SPA         | 0100   | X111<Address "Opcode"> | T3: If (AC(15) = 0) then (PC ← PC + 1)   |
  | INC         | 0101   | X111<Address "Opcode"> | T3: AC ← AC + 1                          |
  | CMA         | 0110   | X111<Address "Opcode"> | T3: AC ← AC'                             |
  | CLA         | 0111   | X111<Address "Opcode"> | T3: AC ← 0                               |

## Schematic

![image](https://github.com/NadaKhaledMazen/Modified-SAP1-Processor/assets/105931027/ffbe9062-770e-4c45-a93a-61169a9a2df6)

