# 数据通路

---

- ### [目录](index.MD)
    
---

### **逻辑设计**

- 二进制表示信息
  - 低电压=0 高电压=1
  - 1bit一条线路
  - 多个bit的数据编码成多条线路
- 组合单元
  - 处理数据值的单元
  - 输出只与输入相关 输入相同则输出也相同
- 状态单元
  - 存储信号
  - 时钟信号
  
### **时钟方法**

组合单元在时钟周期内对数据进行处理

- 时钟边沿之间进行
- 输入来自状态单元，输出给状态单元

```mermaid
graph LR
    StateElement1-->cl(Conbiantional logic)
    cl-->StateElement2
```

- 最长延迟决定时钟周期

---

### **ALU控制信号**

由2bits ALUOP和6bits funct字段生成ALU控制信号

采用多级译码

- 主控单元生成ALUOP
- ALU控制单元生成ALUControl

|指令操作码|ALUOP|指令操作|funct字段|ALU操作|ALUControl|
|:-:|:-:|:-:|:-:|:-:|:-:|
|lw|00|lw|any|add|0010|
|sw|00|sw|any|add|0010|
|beq|01|beq|any|subtract|0110|
|R型|10|add|100000|add|0010|
|R型|10|sub|100010|subtract|0110|
|R型|10|and|100100|and|0000|
|R型|10|or|100101|or|0001|
|R型|10|slt|101010|slt|0111|

### **主控单元**

- `RegDst`= `R-format`
- `ALUSrc`=`lw`+`sw`
- `MemtoReg`=`lw`
- `RegWrite`=`R-format`+`lw`
- `MemRead`=`lw`
- `MemWrite`=`sw`
- `Branch`=`beq`
- `ALUOp1`=`R-format`
- `ALUOp0`=`beq`
