# 🔷 2-bit ALU Design in Verilog

## 📌 Objective
To design and implement a **2-bit Arithmetic Logic Unit (ALU)** using **Verilog HDL** that performs basic arithmetic and logical operations.

---

## ⚙️ Features
✔️ Performs Arithmetic Operations:
- Addition
- Subtraction

✔️ Performs Logical Operations:
- AND
- OR
- XOR

✔️ Uses a 3-bit control signal (`op`) to select operations

✔️ Simulated using **ModelSim**

---

## 🧠 Operation Table

| op  | Operation | Description |
|-----|------------|-------------|
| 000 | AND        | Bitwise AND |
| 001 | OR         | Bitwise OR |
| 010 | XOR        | Bitwise XOR |
| 011 | ADD        | Addition |
| 100 | SUB        | Subtraction |


## 🧾 Verilog Code

### 🔹 ALU Module

```verilog
module alu_2bit (
    input  [1:0] A, B,
    input  [2:0] op,
    output reg [1:0] Y,
    output reg carry
);

always @(*) begin
    case(op)
        3'b000: begin Y = A & B; carry = 0; end
        3'b001: begin Y = A | B; carry = 0; end
        3'b010: begin Y = A ^ B; carry = 0; end
        3'b011: {carry, Y} = A + B;
        3'b100: {carry, Y} = A - B;
        default: begin Y = 2'b00; carry = 0; end
    endcase
end

endmodule
```

---

## 🧪 Testbench

```verilog
module tb_alu_2bit();

reg [1:0] A, B;
reg [2:0] op;
wire [1:0] Y;
wire carry;

alu_2bit uut (
    .A(A),
    .B(B),
    .op(op),
    .Y(Y),
    .carry(carry)
);

initial begin
    A=2'b11; B=2'b10; op=3'b000; #10;
    A=2'b10; B=2'b01; op=3'b001; #10;
    A=2'b11; B=2'b01; op=3'b010; #10;
    A=2'b11; B=2'b01; op=3'b011; #10;
    A=2'b11; B=2'b01; op=3'b100; #10;
    $finish;
end

endmodule
