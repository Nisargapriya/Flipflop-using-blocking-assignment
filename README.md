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
module sr_ff (
    input wire S, R, clk,
    output reg Q
);
    always @(posedge clk) begin
        // Use non-blocking assignments for sequential logic
        case ({S, R})
            2'b00: Q <= Q;
            2'b01: Q <= 1'b0;
            2'b10: Q <= 1'b1;
            2'b11: Q <= 1'bx;
        endcase
    end
endmodule
```
### SR Flip-Flop Test bench 
module sr_ff_tb;
    reg S, R, clk;
    wire Q;
    sr_ff uut (
        .S(S), 
        .R(R), 
        .clk(clk), 
        .Q(Q)
    );
    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end
    initial begin
        S = 0; R = 0;
        #10;
        S = 0; R = 1;
        #10;
        S = 0; R = 0;
        #10;
        S = 1; R = 0;
        #10;
        S = 0; R = 0;
        #10;
        S = 1; R = 1;
        #10;
        $finish;
    end
endmodule
#### SIMULATION OUTPUT

<img width="1645" height="825" alt="image" src="https://github.com/user-attachments/assets/c8b3ea71-5196-460b-9be8-934310a7a763" />

### JK Flip-Flop (Blocking)
module jk_ff (
    input wire J, K, clk,
    output reg Q
);
    initial Q = 1'b0;

    always @(posedge clk) begin
        case ({J, K})
            2'b00: Q <= Q;      
            2'b01: Q <= 1'b0;   
            2'b10: Q <= 1'b1;   
            2'b11: Q <= ~Q;     
        endcase
    end
endmodule
### JK Flip-Flop Test bench 
module jk_ff_tb;
    reg J, K, clk;
    wire Q;

    jk_ff uut (
        .J(J), 
        .K(K), 
        .clk(clk), 
        .Q(Q)
    );

    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    initial begin
        J = 1; K = 0; 
        #10;
        J = 0; K = 0;
        #10;
        J = 0; K = 1; 
        #10;
        J = 1; K = 1;
        #10;
        J = 1; K = 1;
        #10;
        $finish;
    end
endmodule
#### SIMULATION OUTPUT
<img width="1636" height="894" alt="image" src="https://github.com/user-attachments/assets/e72c0df3-49ae-4874-bbe7-2d4b323ef8ea" />

### D Flip-Flop (Blocking)
module d_ff (
    input wire d, clk,
    output reg Q
);
    always @(posedge clk) begin
        Q <= d;
    end
endmodule
### D Flip-Flop Test bench 
module d_ff_tb;
    reg d, clk;
    wire Q;

    d_ff uut (
        .d(d), 
        .clk(clk), 
        .Q(Q)
    );

    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    initial begin
        d = 0;
        #10;
        d = 1;
        #10;
        d = 0;
        #10;
        d = 1;
        #10;
        $finish;
    end
endmodule
#### SIMULATION OUTPUT
<img width="1615" height="896" alt="image" src="https://github.com/user-attachments/assets/96b21bef-6d87-40ae-b4a9-efffef94f43b" />

### T Flip-Flop (Blocking)
module t_ff (
    input wire T, clk,
    output reg Q
);
    initial Q = 1'b0;

    
    always @(posedge clk) begin
        if (T == 1)
            Q <= ~Q;
        else
            Q <= Q;
    end
endmodule
### T Flip-Flop Test bench 
module t_ff_tb;
    reg T, clk;
    wire Q;

    t_ff uut (
        .T(T), 
        .clk(clk), 
        .Q(Q)
    );

    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    initial begin
        T = 0; 
        #10;
        T = 1; 
        #10;
        T = 1; 
        #10;
        T = 0; 
        #10;
        $finish;
    end
endmodule
#### SIMULATION OUTPUT

<img width="1413" height="899" alt="image" src="https://github.com/user-attachments/assets/70fb0e4f-0757-4bc7-9f2f-fca1b0eb6940" />

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
