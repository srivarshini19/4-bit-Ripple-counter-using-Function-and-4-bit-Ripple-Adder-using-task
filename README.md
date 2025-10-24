# 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task

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
module Ripple_adder (input  [3:0] a,input  [3:0] b,input cin,output reg [3:0] sum,output reg cout
);
integer i;
reg c;
    task full_adder;
        input a, b, cin;
        output s, cout;
        begin
            s    = a ^ b ^ cin;
            cout = (a & b) | (b & cin) | (a & cin);
        end
    endtask
    always @(*) begin
    c = cin;
    for (i = 0; i < 4; i = i + 1) begin
        full_adder(a[i], b[i], c, sum[i], c);
    end
    cout = c;
    end
endmodule
```
# Test Bench
```
module Ripple_adder_tb;
    reg  [3:0] a, b;
    reg        cin;
    wire [3:0] sum;
    wire       cout;

    Ripple_adder uut (a, b, cin, sum, cout);

    initial begin
        $monitor("Time=%0t | a=%b b=%b cin=%b | sum=%b cout=%b",
                  $time, a, b, cin, sum, cout);

        a=4'b0000; b=4'b0000; cin=0;
        #10 a=4'b0101; b=4'b0011; cin=0;
        #10 a=4'b1111; b=4'b0001; cin=0;
        #10 a=4'b1010; b=4'b0101; cin=1;
        #10 a=4'b1111; b=4'b1111; cin=1;
        #10 $finish;
    end
endmodule
```
# Output Waveform
<img width="1919" height="1079" alt="Ripple adder" src="https://github.com/user-attachments/assets/e6df7989-69c9-4cff-b65f-4ac9ea6970bc" />


# 4 bit Ripple counter using Function
// 4-bit Ripple Counter using Function
```
module Ripple_counter (
    input clk, rst,
    output reg [3:0] Q
);
    function [3:0] count;
        input [3:0] x;
        begin
            count = x + 1;   
        end
    endfunction
    always @(posedge clk or posedge rst) begin
     if (rst)
           Q <= 4'b0000;     
       else
            Q <= count(Q);    
    end
endmodule
```

# Test Bench
```
module Ripple_counter_tb;
    reg clk, rst;
    wire [3:0] Q;
    Ripple_counter uut (
        .clk(clk),
        .rst(rst),
        .Q(Q)
    );
    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end
    initial begin
        rst = 1;
        #12;
        rst = 0;
        #200;
        rst = 1;
        #10;
        rst = 0;
        #100;
        $finish;
    end
endmodule
```


# Output Waveform 
<img width="1919" height="1079" alt="Ripple counter" src="https://github.com/user-attachments/assets/41f16d1a-86d1-4fe6-b358-957f1086ebf1" />


# Conclusion
In this experiment, a 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task was successfully designed and simulated using Verilog HDL.
