---
title: Computer-Architecture-MIPS-verilog-Implementation
excerpt: 컴퓨터구조 MIPS 베릴로그 구현
tags: [컴퓨터구조, MIPS, Verilog]
comment: true
---

# Computer Architecture MIPS Implementation

## MIPS.v

```verilog
module MIPS(
	input CLK
	 );
```

CLK만을 input으로 가지는 MIPS 모듈 선언. MIPS의 전체 구조를 구현하며, Instruction Memory, Control, Register, ALU, Data Memory간의 관계 또는 처리 과정의 틀

```verilog
// IM
wire [31:0] Next_PC, Instr, Branch_addr;
reg [31:0] PC;

// Control
wire RegDst, RegWrite; // control signal
wire ALUSrc, MemWrite, MemRead, MemToReg; // control signal
wire [3:0] ALUOp;
wire PCSrc, JToPC, Branch; // mux control signal
wire [5:0] Opcode, Funct;

// Register
wire [31:0] Jump_addr;
wire [4:0] Read1, Read2, Reg_Write_addr;
wire [31:0] Branch_or_offset;
wire [31:0] Reg_Write_data, Read_data1, Read_data2;

// ALU
wire [31:0] ALU_B, ALU_result, Lw_Sw_offset;
wire zero;

// DM
wire [31:0] Read_or_Write_addr;
wire [31:0] DM_Write_data, DM_Read_data;
```

Instruction_Mem에 필요한 Next_PC, Instr, Branch_addr wire 선언, PC reg 선언.

Control에 필요한 RegDst, RegWrite, ALUStc, MemWrite, MemRead, MemToReg, ALUOp, JToPC, Branch, Opcode, Funct wire 선언

Register에 필요한 Jump_addr, Read1, Read2, Reg_Write_addr, Branch_or_offset, Reg_Write_data, Read_data1, Read_data2 wire 선언

ALU에 필요한 ALU_B, ALU_result, Lw_Sw_offset, zero wire 선언

Data_Mem에 필요한 Read_or_Write_addr, DM_Write_data, DM_Read_data wire 선언

```verilog
assign Next_PC = PC + 32'd4;
assign Branch_addr = {Branch_or_offset[29:0], 2'b00};
assign PCSrc = (Branch && zero);

assign Opcode = Instr[31:26];
assign Funct = Instr[5:0];

assign Jump_addr = {Next_PC[31:28], {Instr[25:0], 2'b00}};
assign Read1 = Instr[25:21];
assign Read2 = Instr[20:16];
assign Reg_Write_addr = (RegDst) ? Instr[15:11] : Instr[20:16];
assign Branch_or_offset = (Instr[15] == 1) ? {16'hFFFF, Instr[15:0]} : {16'h0000, Instr[15:0]}; // sign extend.

assign Lw_Sw_offset = (Branch_or_offset[31] == 1) ? {2'b11, Branch_or_offset[31:2]} : {2'b00, Branch_or_offset[31:2]};
// if instruction is lw or sw, divide the offset by 4.
assign ALU_B = (Opcode == 6'b100011 || Opcode == 6'b101011) ? Lw_Sw_offset : ((ALUSrc) ? Branch_or_offset : Read_data2);
// if instruction is lw or sw, ALU_B is Lw_Sw_offset.

assign DM_Write_data = Read_data2;
assign Read_or_Write_addr = ALU_result;
assign Reg_Write_data = (MemToReg) ? DM_Read_data : ALU_result;
```

전 코드에서 wire로 변수들을 이어줄 준비를 했으니 이제 할당할 차례임.

`assign Next_PC = PC + 32'd4;` PC값에 32비트 10진수 4를 더해줌 -> PC = PC + 4

`assign Branch_addr = {Branch_or_offset[29:0], 2'b00};` {a, b}: 결합 연산

branch 할 때의 주소를 할당. Branch_or_offset의 상위 29비트를 2비트 shift함

`assign PCSrc = (Branch && zero);` PCSrc control을 결정함. Branch AND zero

``assign Opcode = Instr[31:26];` R-Type에서 Opcode를 결정. Instruction의 상위 6비트

`assign Funct = Instr[5:0];` R-Type에서 Funct를 결정. Instruction의 하위 6비트

`assign Jump_addr = {Next_PC[31:28], {Instr[25:0], 2'b00}};`

Jump 할 주소를 결정. Opcode를 제외한 명령어의 26비트를 2비트 shift 후 Next_PC의 상위 4비트에 결합

`assign Read1 = Instr[25:21];` `assign Read2 = Instr[20:16];` Read register 결정

`assign Reg_Write_addr = (RegDst) ? Instr[15:11] : Instr[20:16];`

Reg_Write_addr 결정. RegDst가 1이면(R-Type) rd가 0이면(I-Type) rt가 Reg_write에 들어감

`assign Branch_or_offset = (Instr[15] == 1) ? {16'hFFFF, Instr[15:0]} : {16'h0000, Instr[15:0]};` Instr[15] == 1, 즉 2'complement일 때는 음수이므로 1로 sign extension, 아니면 0으로

`assign Lw_Sw_offset = (Branch_or_offset[31] == 1) ? {2'b11, Branch_or_offset[31:2]} : {2'b00, Branch_or_offset[31:2]};`  모르겟음

`assign ALU_B = (Opcode == 6'b100011 || Opcode == 6'b10101) ? Lw_Sw_offset : ((ALUSrc) ? Branch_or_offset : Read_data2);` 모르겟음

`assign DM_Write_data = Read_data2;` I-Type일 때 rt가 Write data로 결정

`assign Read_or_Write_addr = ALU_result;` Read address 와 Write address가 ALU_result로 결정

`assign Reg_Write_data = (MemToReg) ? DM_Read_data : ALU_result;`

MemToReg가 1이면 Register에 저장할 data를 메모리에서 가져온 값인 DM_Read_data이고 0이면 ALU에서 계산된 값인 ALU_result로 결정

```verilog
Instruction_Mem Instr_mem(PC[8:2], Instr); // Asynchronous module.
/*
	[8:0]         [8:2]
0	000 0000 00   000 0000 => 0
4	000 0001 00   000 0001 => 1
8	000 0010 00   000 0010 => 2
12	000 0011 00   000 0011 => 3
16	000 0100 00   000 0100 => 4
20	000 0101 00   000 0101 => 5
24	000 0110 00   000 0110 => 6
28	000 0111 00   000 0111 => 7
*/
```

Instruction_Mem에서 input값으로 PC[8:2]와 Instr를 넣어줌. PC[8:2]는 4씩 끊어지는 PC값을 10진수로 1씩끊어지게 인코딩(?)하는 과정

```verilog
Control control(Opcode, Funct, RegDst, RegWrite, ALUSrc, MemWrite, MemRead, MemToReg, JToPC, Branch, ALUOp); // Asynchronous module.
Register Reg(CLK, RegWrite, Read1, Read2, Reg_Write_addr, Reg_Write_data, Read_data1, Read_data2); // Synchronous module.
ALU alu(ALUOp, Read_data1, ALU_B, ALU_result, zero); // Asynchronous module.
Data_Mem DM(CLK, MemWrite, MemRead, Read_or_Write_addr[6:0], DM_Write_data, DM_Read_data); // Synchronous module.
```

Control, Register, ALU, Data_Mem 모듈에 Input값 넣어줌

Asynchronous vs Synchronous 차이 모르겟음

```verilog
always @(posedge CLK)
begin
	PC <= (JToPC) ? Jump_addr : ((PCSrc) ? (Branch_addr + Next_PC) : Next_PC);
end

initial
begin
	PC = 32'd0;
end

endmodule
```

모르겟음... ㅡㅡ;;

## Instruction_Mem.v

```verilog
module Instruction_Mem(
	input wire [6:0] addr,
	output wire [31:0] data );
```

Instruction Memory 모듈 선언. Input으로 addr(주소)와 data(데이터)를 받음.

```verilog
//parameter NMEM = 128;   // Number of memory entries, not the same as the memory size
//parameter IM_DATA = "im_data.txt";  // file to read data from
reg [31:0] mem [0:127];  // 32-bit memory with 128 entries
```

128개의 entry를 가진 32비트 명령어 메모리 선언

```verilog
initial
begin
	// $readmemh(IM_DATA, mem, 0, NMEM-1);
	mem[0] = 32'b100011_00000_10000_00000_00000_000000; // lw s0 0($zero) , s0 = 1 
	mem[1] = 32'b100011_00000_10001_00000_00000_000100; // lw s1 4($zero) , s1 = 0
	mem[2] = 32'b000000_10000_10001_10010_00000_100000; // add s2 s0 s1 , s2 = 1 
	mem[3] = 32'b000000_10000_10001_10011_00000_100010; // sub s3 s0 s1 , s3 = 1
	mem[4] = 32'b000000_10010_10011_10100_00000_100100; // and s4 s2 s3 , s4 = 1
	mem[5] = 32'b000000_10010_10011_10101_00000_100110; // xor s5 s2 s3 , s5 = 0
	mem[6] = 32'b000000_10101_10100_10110_00000_101010; // slt s6 s5 s4 , s6 = 1
 	mem[7] = 32'b000100_10101_10001_00000_00000_000001; // beq s5 s1 1 , s5 = s1 = 0
	mem[8] = 32'b000010_00000_00000_00000_00000_001101; // j 13 , it is not executed at first, but is executed after the jump. (mem[12])
	mem[9] = 32'b100011_00000_10111_00000_00000_001000; // lw s7 8($zero) , s7 = 0
	mem[10]= 32'b101011_10111_10101_00000_00000_010000; // sw s5 16(s7) , mem[4] = 0
	mem[11]= 32'b100011_10111_10000_00000_00000_010000; // lw s0 16(s7) , s0 = mem[4] = 0
	mem[12]= 32'b000010_00000_00000_00000_00000_000011; // j 3
	mem[13]= 32'b000000_10000_00000_10111_00000_100111; // nor s7 s0 $zero , s7 = 32'b1111_1111_1111_1111_1111_1111_1111_1111;
	mem[14]= 32'b100011_00000_01000_00000_00000_101000; // lw t0 40($zero) , t0 = 32'b0101_0101_1010_1010_0101_0101_1010_1010;
	mem[15]= 32'b100011_00000_01001_00000_00000_101100; // lw t1 44($zero) , t1 = 32'b0111_0111_1000_1000_0111_0111_1000_1000;
	mem[16]= 32'b000000_01000_01001_01010_00000_100000; // add t2 t0 t1    , t2 = 32'b1100_1101_0011_0010_1100_1101_0011_0010; positive value (overflow)
	mem[17]= 32'b000000_01000_01001_01011_00000_100010; // sub t3 t0 t1    , t3 = 32'b1101_1110_0010_0001_1101_1110_0010_0010; negative value
	mem[18]= 32'b000000_01000_01001_01100_00000_100100; // and t4 t0 t1    , t4 = 32'b0101_0101_1000_1000_0101_0101_1000_1000;
	mem[19]= 32'b000000_01000_01001_01101_00000_100110; // xor t5 t0 t1    , t5 = 32'b0010_0010_0010_0010_0010_0010_0010_0010;
	mem[20]= 32'b000000_01010_01011_01110_00000_101010; // slt t6 t2 t3    , t6 = 32'd1;
end
```

simulation 할 때의 명령어를 instruction memory에 저장

```verilog
assign data = mem[addr][31:0];

endmodule
```

data에 addr번째 명령어 저장(?)

## Control.v

```verilog
module Control(
		input wire [5:0] Opcode, Funct,
		output reg RegDst, RegWrite, ALUSrc, MemWrite, MemRead, MemToReg, JToPC, Branch,
		output reg [3:0] ALUOp );
```

Control 모듈 선언. Input으로 Opcode, Funct를 가짐.

Output으로는 Control signal들인 RegDst, RegWrite, ALUSrc, MemWrite, MemRead, MemToReg, JToPC, Branch, ALUOp를 가짐.

```verilog
always @(*)
begin
	case (Opcode)
```

Opcode를 보고 control 설정

```verilog
6'b000000 : begin // R Type - add, sub, and, or, slt
			RegDst = 1; RegWrite = 1; ALUSrc = 0; MemWrite = 0; MemRead = 0; MemToReg = 0; JToPC = 0; Branch = 0;
			if(Funct == 6'b100000)	ALUOp = 4'b0010; // add
			else if(Funct == 6'b100010) ALUOp = 4'b0110; // sub
			else if(Funct == 6'b100100) ALUOp = 4'b0000; // and
			else if(Funct == 6'b100101) ALUOp = 4'b0001; // or
			else if(Funct == 6'b101010) ALUOp = 4'b0111; // slt
			else if(Funct == 6'b011000) ALUOp = 4'b1000; // mult
			else if(Funct == 6'b100110) ALUOp = 4'b1101; // xor 
			else if(Funct == 6'b100111) ALUOp = 4'b1100; // nor
			else ALUOp = 4'b0000; // To avoid creating a latch
		end
```

Opcode가 6'b000000일때, 즉 R-Type일때의 Control signal 설정. R-type일때는 Funct를 보고 어떤 기능을 하는지 알 수 있으므로 Funct에 따라 ALUOp 결정.

```verilog
6'b100011 : begin // Load Word
			RegDst = 0; RegWrite = 1; ALUSrc = 1; MemWrite = 0; MemRead = 1; MemToReg = 1; JToPC = 0; Branch = 0;
			ALUOp = 4'b0010; // add for lw
		end
		6'b101011 : begin // Store Word
			            RegWrite = 0; ALUSrc = 1; MemWrite = 1; MemRead = 0; 	       JToPC = 0; Branch = 0;
			ALUOp = 4'b0010; // add for sw
			RegDst = 0; MemToReg = 0; // To avoid creating a latch
		end
		6'b000100 : begin // Beq
				    RegWrite = 0; ALUSrc = 0; MemWrite = 0; MemRead = 0;	       JToPC = 0; Branch = 1;
			ALUOp = 4'b0110; // sub for beq
			RegDst = 0; MemToReg = 0; // To avoid creating a latch
		end
		6'b000010 : begin// Jump
				    RegWrite = 0;             MemWrite = 0; MemRead = 0;	       JToPC = 1; Branch = 0;
			RegDst = 0; ALUSrc = 0; MemToReg = 0; ALUOp = 4'b0000; // To avoid creating a latch
		end
```

Simulation할 때, Instruction memory에서 lw, sw, beq, j 명령어와 위에서 정의한 R-Type 명령어만을 사용하므로 이것들의 Opcode에 대한 Control Signal 설정

```verilog
default : begin // To avoid creating a latch
			RegDst = 0; RegWrite = 0; ALUSrc = 0; MemWrite = 0; MemRead = 0; MemToReg = 0; JToPC = 0; Branch = 0;
			ALUOp = 4'b0000; 
		end
	endcase
end
```

모르겟음

```verilog
initial
begin
	RegDst = 0; RegWrite = 0; ALUSrc = 0; MemWrite = 0; MemRead = 0; MemToReg = 0; JToPC = 0; Branch = 0;
	ALUOp = 4'b0000;
end
endmodule
```

Simulation할 때의 Control Signal 설정

## Register.v

```verilog
// `define DEBUG_CPU_REG 0
module Register(
		input wire CLK,
		input wire RegWrite, // control signal
		input wire [4:0] read1, read2,
		input wire [4:0] wrreg,
		input wire [31:0] wrdata,
		output reg [31:0] data1, data2 );
```

Register 모듈 선언. Input으로는 CLK, RegWrite, read1, read2, wrreg, wrdata를 가지고, Output으로는 data1, data2를 가짐.

```verilog
reg [31:0] mem [0:31];  // 32-bit memory with 32 entries
```

32개의 entry를 가지는 32비트 메모리 선언

```verilog
initial 
begin
	// $display("$v0, $v1, $t0, $t1, $t2, $t3, $t4, $t5, $t6, $t7");
	//$monitor("%b, %b, %b, %b, %b, %b, %b, %b, %b, %b",
		//mem[0][31:0],		/* $zero */
		//mem[16][31:0],	/* $s0 */
		//mem[17][31:0],	/* $s1 */
		//mem[18][31:0],	/* $s2 */
		//mem[19][31:0],	/* $s3 */
		//mem[20][31:0],	/* $s4 */
		//mem[21][31:0],	/* $s5 */
		//mem[22][31:0],	/* $s6 */
		//mem[23][31:0]		/* $s7 */
		//);
	mem[0] = 32'd0; // $zero = 0;
end
```

register memory 출력(?)

```verilog
always @(*) 
begin
	if (read1 == 5'd0) // $zero
		data1 = 32'd0;
	else if ((read1 == wrreg) && RegWrite)
		data1 = wrdata;
	else
		data1 = mem[read1][31:0];
end
```

- if 절: read1이 $0(zero)일 때 data1에 0을 넣어줌
- else if 절: read1이 write register이고 RegWrite가 1일때 data1에 wrdata를 넣어줌 (read1이 write register일 때가 있나??)
- else 절: 두 경우 모두 아닐 때 read1의 주소에 있는 값을 data1에 넣어줌

```verilog
always @(*)
begin
	if (read2 == 5'd0) // $zero
		data2 = 32'd0;
	else if ((read2 == wrreg) && RegWrite)
		data2 = wrdata;
	else
		data2 = mem[read2][31:0];
end
```

- if 절: read2가 $0(zero)일 때 data2에 0을 넣어줌
- else if 절: read2가 write register이고 RegWrite가 1일때 data2에 wrdata를 넣어줌
- else 절: 두 경우 모두 아닐 때 read2의 주소에 있는 값을 data2에 넣어줌

```verilog
always @(posedge CLK) 
begin
	if (RegWrite && wrreg != 5'd0) // $zero can not be changed.
	begin
		// write a non $zero register
		mem[wrreg] <= wrdata;
	end
end
endmodule
```

모르겟음

## ALU.v

```verilog
module ALU(
		input [3:0] ALUOp,
		input [31:0] a, b,
		output reg [31:0] out,
		output zero );
```

ALU 모듈 선언. Input으로 ALUOp, a, b를 가지고 Output으로 out, zero를 가짐.

```verilog
wire [31:0] sub_ab;
wire [31:0] add_ab;
wire [31:0] mult_ab;
wire oflow_add, oflow_sub, oflow, slt;
```

sub, add, mult, add overflow, sub overflow, overflow, slt wire 선언

```verilog
assign zero = (0 == out); // true or false
assign sub_ab = a - b;
assign add_ab = a + b;
assign mult_ab = a * b;
```

- out이 0이면 zero는 1, out이 1이면 zero는 0
- sub, add, mult 계산

```verilog
assign oflow_add = (a[31] == b[31] && add_ab[31] != a[31]) ? 1 : 0; // overflow
assign oflow_sub = (a[31] == b[31] && sub_ab[31] != a[31]) ? 1 : 0; // overflow, If the latter is greater in absolute value, oflow_sub is 1.
assign oflow = (ALUOp == 4'b0010) ? oflow_add : oflow_sub;
assign slt = oflow_sub ? ~(a[31]) : a[31];
```

overflow계산하는 과정. add와 sub 연산 시 overflow를 체크해 slt 연산 시 사용.

```verilog
always @(*) 
begin
	case (ALUOp)
		4'b0010  : out = add_ab;		/* add */
		4'b0000  : out = a & b;			/* and */
		4'b1000  : out = mult_ab;		/* mult */
		4'b1100  : out = ~(a | b);		/* nor */
		4'b0001  : out = a | b;			/* or */
		4'b0111  : out = {31'd0, slt};		/* slt */
		4'b0110  : out = sub_ab;		/* sub */
		4'b1101  : out = a ^ b;			/* xor */
		default  : out = 0;
	endcase
end
endmodule
```

Sumulation 할 때, ALUOp에 따른 연산을 수행해 out에 값을 넣어줌.

## Data_Mem.v

```verilog
module Data_Mem(
	input CLK,
	input wire MemWrite, MemRead, // control signal
	input wire [6:0] addr,
	input wire [31:0] Write_Data,
	output reg [31:0] Read_Data );
```

Data memory 모듈 선언. Input으로 CLK, MemWrite, MemRead, addr, Write_Data를 가지고, Output으로 Read_Data를 가짐

```verilog
reg [31:0] mem [0:127];  // 32-bit memory with 128 entries
```

128개의 entry를 가지는 32비트 메모리 선언

```verilog
always @(*)
begin
	if(MemWrite == 0 && MemRead == 1) // lw
		Read_Data = mem[addr][31:0]; 
	else
		Read_Data = Read_Data; // To avoid creating a latch
end
```

MemWrite가 0이고 MemRead가 1이면 lw 명령어를 수행할 때임

- if 절: Read_Data에 addr주소를 가진 값 넣어줌
- else절: latch 생성을 피한다(?)

```verilog
always @(posedge CLK)
begin
	if(MemWrite == 1 && MemRead == 0) // sw
		mem[addr][31:0] <= Write_Data;
end
```

MemWrite가 1이고 MemRead가 0이면 sw 명령어를 수행할 때임

- if 절: addr주소를 가진 메모리에 Write_Data값을 넣어줌

```verilog
integer i;
initial
begin
	mem[0] = 32'd1; // for s0 = 1
	mem[1] = 32'd0; // for s1 = 0
	mem[2] = 32'd0; // for s7 = 0
	mem[3] = 32'd0; // initialize
	// mem[4]	
	mem[5] = 32'd0; // initialize
	mem[6] = 32'd0; // initialize
	mem[7] = 32'd0; // initialize
	mem[8] = 32'd0; // initialize
	mem[9] = 32'd0; // initialize
	mem[10] = 32'b0101_0101_1010_1010_0101_0101_1010_1010; // 0x55aa_55aa
	mem[11] = 32'b0111_0111_1000_1000_0111_0111_1000_1000; // 0x7788_7788
	for (i=12; i<128; i = i+1) // initialize	
	begin
		mem[i] = 32'd0;
	end
end
endmodule
```

Simulation 할때 필요한 값들을 넣어줌



끗..

