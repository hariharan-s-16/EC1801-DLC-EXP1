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
...
module boolean(
input wire A, 
input wire B, 
output wire F 
); 
assign F = (~A) | B ;    // F = A' + B 

endmodule
...
## TestBench Program
...
module tb;
    reg A, B;
    wire F;
    // Instantiate the design under test (DUT)
    fun uut (
        .A(A),
        .B(B),
        .F(F)
    );

    initial begin
        // ---- VCD dump setup ----
        $dumpfile("fun.vcd");   // name of the VCD file to be generated
        $dumpvars(0, tb);   // dump all signals in this testbench hierarchy

        // ---- Apply all 4 input combinations ----
        $monitor("Time=%0t A=%b B=%b | F=%b", $time, A, B, F);

        A = 0; B = 0; #10;
        A = 0; B = 1; #10;
        A = 1; B = 0; #10;
        A = 1; B = 1; #10;
        A = 0; B = 0; #10;


        #10 $finish;
    end

endmodule
...
## Truth Table

 <img width="637" height="249" alt="image" src="https://github.com/user-attachments/assets/da727d62-a1ae-4ba8-9c11-ca8c24077f33" />


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

<img width="1908" height="1015" alt="Screenshot (14)" src="https://github.com/user-attachments/assets/cb61bd1a-cb56-40e1-ad35-bfb37a3b5ef3" />

## OUTPUT

<img width="1920" height="1019" alt="Screenshot (13)" src="https://github.com/user-attachments/assets/829d3805-2449-46cd-b1e0-81305df91cf2" />




The design was compiled and simulated using Synopsys VCS, and the functionality was verified using DVE waveform analysis.
7. Viva-Voce Questions
1. What is Boolean function minimization?
Boolean function minimization is the process of simplifying a Boolean algebraic expression to use the minimum number of gates and literals while preserving the exact same logical output and functionality.
2. What is a minterm?
A minterm is a product (AND) of all the variables in a Boolean function, either in their complemented or uncomplemented form, such that the minterm evaluates to $1$ for exactly one combination of input values.
3. What is a Karnaugh map?
A Karnaugh map (K-map) is a graphical tool used to simplify Boolean expressions without having to use complex Boolean algebraic theorems. It arranges truth table outputs in a grid format using Gray code so that adjacent cells differ by only one variable bit.
4. Why is Boolean minimization required?
Boolean minimization is required to:Reduce hardware complexity, chip area, and manufacturing costs.Minimize propagation delay (signal delay) to increase circuit speed.Lower power consumption and heat dissipation.
5. What are universal gates?
Universal gates are logic gates that can be used to implement any Boolean function or standard logic gate (AND, OR, NOT) individually without needing any other gate type. The two primary universal gates are NAND and NOR.
6. What is the difference between SOP and POS?
SOP (Sum of Products): An expression formed by ANDing variables together (product terms) and then ORing those terms together (e.g., $AB + CD$).POS (Product of Sums): An expression formed by ORing variables together (sum terms) and then ANDing those terms together (e.g., $(A + B)(C + D)$).
7. What is the purpose of a Verilog testbench?
A Verilog testbench is a non-synthesizable simulation wrapper used to test and verify a hardware design. It applies stimulus (input vectors) to the Design Under Test (DUT) and monitors its outputs to check for correctness.
8. Why is a VCD file generated?
A VCD (Value Change Dump) file is generated during simulation to record all signal value changes over time. It is used by waveform viewer tools to visually inspect the behavior of the design.
9. What is the purpose of ./simv?
./simv executes the compiled simulation binary generated by Synopsys VCS. Running it executes the testbench code, runs the simulation, prints display messages to the terminal, and triggers the generation of waveform dump files.
10. What is the purpose of DVE?
DVE (Design Warehousing and Evaluation environment / VCS Simulator GUI) is a graphical waveform viewer used to visually debug and analyze hardware designs. It allows you to inspect signal transitions, trace hierarchies, and verify whether the design meets the truth table requirements.
11. What is the difference between simulation and synthesis?
Simulation: A software-based verification process that models the behavioral or structural timing and logic of a design to check functionality prior to hardware realization.Synthesis: The automated process of translating RTL (Verilog/VHDL) code into a target-specific netlist of actual physical logic gates and hardware components (like FPGA look-up tables or ASIC standard cells).
12. Why are A and C absent from the minimized expression?
Variables $A$ and $C$ are absent from the minimized expression because, within the grouped cells on the K-map, they undergo changes (both $0$ and $1$) while the output remains constant. Since they are redundant and do not affect the outcome, they are eliminated through logical adjacency.
13. What is the purpose of $dumpfile?
$dumpfile is a Verilog system task used to specify the filename (e.g., exp1_boolean_min.vcd) where the waveform change data will be saved.
14. What is the purpose of $dumpvars?
$dumpvars is a Verilog system task that enables the recording of variable changes into the VCD file specified by $dumpfile. It specifies the module level scope and hierarchy of signals to monitor during the simulation.
Result
Thus, the Boolean function was minimized, implemented using Verilog HDL, successfully simulated using Synopsys VCS, and verified using Synopsys DVE.

