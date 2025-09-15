# #R-format_instruction 

![[Pasted image 20250915091005.png]]

- **rd**:destination
- **rs1,2**:source
- Both rd and rs have 5bit as there are 32 registers
- **opcodet+funct3+funct7**:operation
# #I-format_instruction

![[Pasted image 20250915091613.png]]
- **rs2 and funct7**:transformed to an immediate(-2048~+2047)
- **opcode** tells us instruction_format(R or I)
# #S-format_instruction

![[Pasted image 20250915092911.png]]
## Examples:
- add, sub: R-type
- addi, lw: I-type
- sw: S-type