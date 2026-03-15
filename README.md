# 4_bit_RCA_using_function
# EXP NP: 4. 4-bit Ripple Carry Adder using Task, and 4-bit Ripple Counter using Function with Testbench
# Aim
To design and simulate a 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 environment.

# Apparatus Required
Vivado 2023.1
# Procedure
1. Launch Vivado 2023.1
Open Vivado and create a new project.
2. Design the Verilog Code
Write the Verilog code for the seven-segment display, defining the logic that maps a 4-bit binary input to the corresponding segments (a to g) of the display.
3. Create the Testbench
Write a testbench to simulate the seven-segment display behavior. The testbench should apply various 4-bit input values and monitor the corresponding output.
4. Create the Verilog Files
Create both the design module and the testbench in the Vivado project.
5. Run Simulation
Run the behavioral simulation to verify the output. 
6. Observe the Waveforms
Analyze the output waveforms in the simulation window, and verify that the correct segments light up for each digit.
7. Save and Document Results
Capture screenshots of the waveform and save the simulation logs. These will be included in the lab report.

# Verilog Code
# 4 bit Ripple Adder using Task
// 4-bit Ripple Carry Adder using Task
```
module ripple_carry_adder_task(
    input  [3:0] A,
    input  [3:0] B,
    input  Cin,
    output reg [3:0] Sum,
    output reg Cout
);
reg c1, c2, c3;
task full_adder;
    input a,b,cin;
    output s,cout;
    begin
        {cout,s} = a + b + cin;
    end
endtask
always @(*) 
begin
    full_adder(A[0],B[0],Cin,  Sum[0],c1);
    full_adder(A[1],B[1],c1,   Sum[1],c2);
    full_adder(A[2],B[2],c2,   Sum[2],c3);
    full_adder(A[3],B[3],c3,   Sum[3],Cout);
end
endmodule
```
#Testbench
```
module tb_ripple_carry_adder_task;
reg [3:0] A,B;
reg Cin;
wire [3:0] Sum;
wire Cout;
ripple_carry_adder_task DUT(A,B,Cin,Sum,Cout);
initial 
begin
    A=4'b0000; B=4'b0000; Cin=0;
    #10 A=4'b0101; B=4'b0011; Cin=0;
    #10 A=4'b1111; B=4'b0001; Cin=0;
    #10 A=4'b1010; B=4'b0101; Cin=1;
    #10 $finish;
end

endmodule
```
# Output Waveform
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/5dcdda1f-669f-4837-932a-2514bd9a0eca" />

# 4 bit Ripple counter using Function
```
module ripple_counter_function(
    input clk,
    input rst,
    output reg [3:0] Q
);

function [3:0] next_count;
    input [3:0] val;
    begin
        next_count = val + 1;
    end
endfunction

always @(posedge clk or posedge rst)
begin
    if(rst)
        Q <= 4'b0000;
    else
        Q <= next_count(Q);
end

endmodule
```
# Test Bench
```
module tb_ripple_counter_function;
reg clk,rst;
wire [3:0] Q;
ripple_counter_function DUT(clk,rst,Q);

initial 
begin
    clk = 0;
    forever #5 clk = ~clk;   
end

initial 
begin
    rst = 1;
    #10 rst = 0;
    #100 $finish;
end
endmodule
```
# Output Waveform 
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/5a4e4c07-4cd4-47f7-a8fb-8c10fffc8be3" />

# Conclusion
In this experiment, a 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task was successfully designed and simulated using Verilog HDL.
