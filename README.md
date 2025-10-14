# EXPERIMENT 3: Simulation of All Flip-Flops using Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **blocking assignment (`=`)** inside the `always` block.  
Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Blocking)
```verilog
## VERILOG CODE

### SR Flip-Flop (Blocking)
verilog
module srff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always @ (posedge clk)
begin
if (rst==1)
q=0;
else if(s==0 && r==0)
q=q;
else if(s==0 && r==1)
q=1'b0;
else if(s==1 && r==0)
q=1'b1;
else
q=1'bx;
end
endmodule
```

### SR Flip-Flop Test bench 
```verilog
module srff_tb;
reg s,r,clk,rst;
wire q;
srff uut(s,r,clk,rst,q);
always #5 clk=~clk;
initial
begin
clk=0;
s=0;r=0;
rst=1;
#10 rst=0;
#10 s=1;r=0; 
#10 s=0;r=0; 
#10 s=0;r=1; 
#10 s=1;r=1; 
#10 s=1;r=0; 
#20 $finish;
end
endmodule
```
#### SIMULATION OUTPUT

### JK Flip-Flop (Blocking)
```verilog
module jkflipflop(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always @ (posedge clk)
begin
if (rst==1)
q=0;
else if(j==0 && k==0)
q=q;
else if(j==0 && k==1)
q=1'b0;
else if(j==1 && k==0)
q=1'b1;
else
q=~q;
end
endmodule
```

### JK Flip-Flop Test bench 
```verilog
module jkfliplflop_tb;
reg j,k,clk,rst;
wire q;
jkflipflop uut(j,k,clk,rst,q);
always #5 clk=~clk;
initial
begin
clk=0;
j=0;k=0;
rst=1;
#10 rst=0;
#10 j=1;k=0; //set
#10 j=0;k=0; //hold
#10 j=0;k=1; //reset
#10 j=1;k=1; //invalid condition
#10 j=1;k=0; //hold
#20 $finish;
end
endmodule

```
#### SIMULATION OUTPUT


### D Flip-Flop (Blocking)
```verilog
module d_ff (
    input wire d,clk,
    output reg Q
);
    always @(posedge clk) begin



endmodule

```
### D Flip-Flop Test bench 
```verilog
module tb_dff;
reg D, clk, reset;
wire Q;
Dflipflop UUT (D, clk, reset, Q);
  always #5 clk = ~clk;

initial begin
clk = 0; D = 0; reset = 1;
#10 reset = 0;
#10 D = 1;   
#10 D = 0;   
#10 D = 1;   
#10 D = 1;   
#10 D = 0;   
#10 D = 1;   

#20 $finish;
end
endmodule

```
#### SIMULATION OUTPUT


### T Flip-Flop (Blocking)
```verilog
module d_ff (
    input wire d,clk,
    output reg Q
);
    always @(posedge clk) begin



endmodule

```
### T Flip-Flop Test bench 
```verilog
module tfliplflop_tb;
reg t,clk,rst;
wire q;
tflipflop uut(t,clk,rst,q);
always #5 clk=~clk;
initial
begin
clk=0;
t=0;
rst=1;
#10 rst=0;t=0;
#10 t=1;
#20 $finish;
end
endmodule

```
#### SIMULATION OUTPUT



### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
