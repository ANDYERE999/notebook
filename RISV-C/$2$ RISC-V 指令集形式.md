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
|   |   |   |   |   |
|---|---|---|---|---|
|指令 (Instruction)|格式 (Format)|语法示例 (Syntax Example)|释义 (Interpretation)|备注 (Notes)|
|整数运算指令|||||
|add|R-Type|add t0, t1, t2|t0 = t1 + t2|将两个寄存器的值相加。|
|addi|I-Type|addi t0, t1, 100|t0 = t1 + 100|将寄存器与一个立即数相加。非常常用。|
|sub|R-Type|sub t0, t1, t2|t0 = t1 - t2|将两个寄存器的值相减。|
|mul|R-Type|mul t0, t1, t2|t0 = t1 * t2|整数乘法。需要 M 扩展支持。|
|div|R-Type|div t0, t1, t2|t0 = t1 / t2|有符号整数除法。需要 M 扩展支持。|
|divu|R-Type|divu t0, t1, t2|t0 = t1 / t2|无符号整数除法。需要 M 扩展支持。|
|逻辑移位指令|||||
|sll|R-Type|sll t0, t1, t2|t0 = t1 << t2|逻辑左移，移动位数由 t2 决定。|
|slli|I-Type|slli t0, t1, 4|t0 = t1 << 4|逻辑左移，移动位数为立即数（此处为4）。|
|srl|R-Type|srl t0, t1, t2|t0 = t1 >> t2|逻辑右移，高位补 0。|
|srli|I-Type|srli t0, t1, 4|t0 = t1 >> 4|逻辑右移，移动位数为立即数。|
|sra|R-Type|sra t0, t1, t2|t0 = t1 >> t2|算术右移，高位补充符号位（保持正负）。|
|srai|I-Type|srai t0, t1, 4|t0 = t1 >> 4|算术右移，移动位数为立即数。|
|访存指令|||||
|lw|I-Type|lw t0, 12(sp)|t0 = Memory[sp + 12]|Load Word: 从内存地址 sp+12 读取一个字 (32位) 到 t0。|
|sw|S-Type|sw t1, 16(sp)|Memory[sp + 16] = t1|Store Word: 将 t1 中的一个字 (32位) 存储到内存地址 sp+16。|
|跳转与分支指令|||||
|jal|J-Type|jal ra, my_func|ra=PC+4, PC=my_func|Jump and Link: 主要用于函数调用。跳转到目标地址，同时将返回地址存入 ra 寄存器。|
|jalr|I-Type|jalr x0, 0(ra)|PC = ra + 0|Jump and Link Register: 跳转到寄存器中的地址。ret 返回指令就是它的一个伪指令。|
|beq|B-Type|beq t0, t1, label|if (t0 == t1) PC=label|Branch if Equal: 如果两个寄存器相等，则跳转到标签 label 处。|
|bne|B-Type|bne t0, t1, label|if (t0 != t1) PC=label|Branch if Not Equal: 如果两个寄存器不相等，则跳转到标签 label 处。|

