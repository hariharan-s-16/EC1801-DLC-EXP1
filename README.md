# EC1801-DLC-EXP1
### EXPERIMENT 1 
### MINIMIZATION AND IMPLEMENTATION OF BOOLEAN FUNCTION
## Aim
To minimize and implement a Boolean function using logic gates and verify the functionality using Synopsys VCS and DVE.
## Software Required
•	Synopsys VCS
•	Synopsys DVE
•	Linux Terminal
•	Verilog HDL
## Boolean Function
Consider the Boolean function:
F(A,B,C,D)=Σm(0,2,5,7,8,10,13,15)
The minimized Boolean expression is: F=B'D'+BD
The function is implemented using Verilog HDL.
## Files Used
File	Description
exp1_boolean_min.v	Verilog design file
exp1_boolean_min_tb.v	Verilog testbench
exp1_boolean_min.vcd	VCD waveform dump generated during simulation

## Verilog Program
```
`timescale 1ns/1ps
module boolean_function (
    input A, B, C, D,
    output F
);

assign F = (~B & ~D) | (B & D);

endmodule
```


## TestBench Program
```
`timescale 1ns/1ps

module tb_boolean_function;

reg A, B, C, D;
wire F;

boolean_function uut (
    .A(A),
    .B(B),
    .C(C),
    .D(D),
    .F(F)
);

initial begin
    $monitor("A=%b B=%b C=%b D=%b | F=%b",
              A, B, C, D, F);

    {A,B,C,D} = 4'b0000;
    repeat (16) begin
        #10;
        {A,B,C,D} = {A,B,C,D} + 1'b1;
    end

    #10;
    $finish;
end

endmodule
```
    
## Truth Table
 
<img width="622" height="675" alt="WhatsApp Image 2026-10-21 at 1 21 50 PM" src="https://github.com/user-attachments/assets/9df585dc-3f09-4846-b3d0-9e749528ebaf" />


## Simulation Procedure
STEP 1 – Open Terminal
Open a terminal in the experiment folder.
bash

STEP 2 – Load Synopsys Environment
source /synopsys/start.sh

STEP 3 – Compile Using VCS
vcs exp1_boolean_min.v exp1_boolean_min_tb.v -full64
 
If compilation is successful, VCS generates the simulation executable:
simv

STEP 4 – Run Simulation
./simv
The terminal displays the input combinations and corresponding output F.
A VCD waveform file is also generated:
exp1_boolean_min.vcd

STEP 5 – Open DVE
dve -full64
Other option
dve -full64 &
A DVE environment will open.

## DVE Waveform Verification
In DVE:
1.	Open the testbench hierarchy.
2.	Locate the signals:
o	A
o	B
o	C
o	D
o	F
3.	Add the signals to the waveform window.
4.	Run/inspect the waveform.
5.	Verify that F = 1 whenever B and D are equal.
6.	Verify that F = 0 whenever B and D are different.
The waveform should agree with the truth table.
 
### Expected Result
The Boolean function
F(A,B,C,D)=Σm(0,2,5,7,8,10,13,15), which simplifies to F=B'D'+BD.
was minimized to F=B'D'+BD.
and successfully implemented using Verilog HDL.
<img width="1920" height="1080" alt="Screenshot (21)" src="https://github.com/user-attachments/assets/66fdf5ee-a4ee-485b-b5a1-53e6d66a6a26" />


## OUTPUT
<img width="1366" height="1157" alt="WhatsApp Image 2026-10-21 at 1 24 46 PM (1)" src="https://github.com/user-attachments/assets/e433ef49-faf8-4910-a900-d234bb0621cd" />

The design was compiled and simulated using Synopsys VCS, and the functionality was verified using DVE waveform analysis.
Result
Thus, the Boolean function was minimized, implemented using Verilog HDL, successfully simulated using Synopsys VCS, and verified using Synopsys DVE.

