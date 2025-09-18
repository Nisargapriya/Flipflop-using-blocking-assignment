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
module sr_ff(S,R,clk,rst,Q);
input S,R,clk,rst;
output reg Q;
always @(posedge clk)
begin
if (rst==1)
    Q=0;
else    
    begin
        case({S,R})
            2'b00: Q= Q;
            2'b01: Q= 1'b0;
            2'b10: Q= 1'b1;
            2'b11: Q= 1'bX;
        endcase
     end
end
endmodule
### SR Flip-Flop (Blocking)

module sr_ff_tb;
reg S,R,clk,rst;
wire Q;
sr_ff uut(S,R,clk,rst,Q);
always #5 clk = ~clk;
initial
begin
clk=0;S=0;R=0;rst=1;
#10;
rst=0;
#10;
S=0;R=0;
#10;
S=0;R=1;
#10;
S=1;R=0;
#10;
S=1;R=1;
#10;
$finish;
end
endmodule
#### SIMULATION OUTPUT
<img width="1202" height="572" alt="image" src="https://github.com/user-attachments/assets/62016a59-7523-4676-8f5f-156522b91f24" />


### JK Flip-Flop (Blocking)
module jk_ff(J,K,clk,rst,Q);
input J,K,clk,rst;
output reg Q;
always @(posedge clk)
begin
if (rst==0)
    Q = 0;
else
    begin
        case({J,K})
            2'b00: Q = Q;
            2'b01: Q = 0;
            2'b10: Q = 1;
            2'b01: Q = ~Q;
        endcase
    end
end
endmodule
### JK Flip-Flop Test bench 

module jk_ff_tb;
reg J,K,clk,rst;
wire Q;
jk_ff uut (J,K,clk,rst,Q);
always #5 clk = ~clk;
initial 
begin
J=0;K=0;clk=0;rst=1;
#10;
rst=0;
#10;
J=0;K=0;
#10;
J=0;K=1;
#10;
J=1;K=0;
#10;
J=1;K=1;
#10;
$finish;
end
endmodule
#### SIMULATION OUTPUT
<img width="1204" height="591" alt="image" src="https://github.com/user-attachments/assets/a5736f24-58b8-42e9-af01-e2dbfaeafe69" />

### D Flip-Flop (Blocking)
module d_ff(D,clk,rst,Q);
input D,clk,rst;
output reg Q;
always @(posedge clk)
begin
if (rst==1)
    Q=0;
else
    Q=D;
end
endmodule
### D Flip-Flop Test bench 
module d_ff_tb;
reg D,rst,clk;
wire Q;
d_ff uut(D,clk,rst,Q);
always #5 clk= ~clk;
initial
begin
D=0;clk=0;rst=1;#10;
rst=0;D=0;#10;
D=1;#20;
$finish;
end
endmodule
#### SIMULATION OUTPUT
<img width="1096" height="579" alt="image" src="https://github.com/user-attachments/assets/b0526f47-b977-44b9-9e29-dcd51555f5bc" />

### T Flip-Flop (Blocking)
module t_ff(T,clk,rst,Q);
input T,clk,rst;
output reg Q;
always @(posedge clk)
begin
if (rst==1)
    Q = 0;
else if (T==0)
    Q = Q;
else
    Q = ~Q;
end
endmodule
### T Flip-Flop Test bench 
module t_ff_tb;
reg T,rst,clk;
wire Q;
t_ff uut(T,clk,rst,Q);
always #5 clk = ~clk;
initial
begin
T=0; clk=0; rst=1; #10;
rst=0; #10;
T=0;#10;
T=1; #10;
$finish;
end
endmodule

#### SIMULATION OUTPUT

<img width="1091" height="574" alt="image" src="https://github.com/user-attachments/assets/32b4523c-f318-454d-9a99-72b5d7886dff" />

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
