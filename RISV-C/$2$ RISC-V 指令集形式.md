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
# #U-format_instruction

![[Pasted image 20250924111152.png]]
lui其中immediate分别是\[20]\[10:1]\[11]\[19:12]\[31:21], 会把前31-12位放到rd的前31-12位。并且把rd的后11位清空，之后使用aadi加回低11位
**由于加法符号拓展的特性，如果后11位的最高位是1，那么lui的时候要把最低位+1**
## Examples:
- add, sub: R-type
- addi, lw: I-type
- sw: S-type

---
# #过程调用
**寄存器**：
- x10-x17用于存放参数和返回值
- x1是栈顶指针，用于存放返回的地址
**跳转指令**：
- jal x1, ProcedureAddress  把function的地址保存在x1并且跳转
- jalr x0, 0(x1) 把取出x1中的值并跳转回来
![[Pasted image 20250922091247.png]]
- temperary register:被调用者可以随意修改，由调用者保存
- save register:调用者可以随意修改，由被调用者保存
---
注意：RISV-C只有在lw和sw可以访存，不能在汇编语言中用A(B,C,D)直接访存

---
