# Exp 4 Comparative Study of 32-Bit ALU Implementations Using Case and If-Else Constructs

## Aim: 
Write a Verilog code for 32 32-bit ALU supporting four logical and four arithmetic operations, use case statement and if statement for ALU behavioral modeling. 

To verify the Functionality using Test Bench 

Synthesize and compare the results using if and case statements 

Identify Critical Path and constraints

## Tool Required: 
 Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim) 

 Synthesis: Genus 

## Design Information and Block Diagram: 
The ALU will take in two 32-bit values and a control line. An Arithmetic unit does the following tasks like addition, subtraction, multiplication and logical operations. As the input is given in 32-bit, we get a 32-bit output. The arithmetic will show only one output at a time, so a selector is necessary to select one of the operators. 

<img width="830" height="511" alt="Screenshot 2025-11-21 203316" src="https://github.com/user-attachments/assets/6468c1df-2549-4fed-94f7-6d29dc7fbf4e" />
 
#### Figure No 1: Block Diagram of 32 Bit ALU 

## Creating a Workspace:
Create a folder in your name (Note: Give the folder name without any spaces) and create a new sub-directory named Exp4 or alu_bl_model for the design. Then, open a terminal from the Sub-Directory.

## Creating Source Codes
In the Terminal window, type gedit <filename>.v (ex: gedit alu_case.v).

A Blank Document opens up into which the following source code can be typed.

(Note: File name should be with HDL Extension)

To verify the Functionality using the Test Bench

#### Source Code – Using Case Statement :
module alu_case(y,a,b,f);

input [31:0]a;

input [31:0]b;

input [2:0]f;

output reg [31:0]y; 

always@(*)

begin 

case(f)

3'b000:y=a&b;	 

3'b001:y=a|b;	

3'b010:y=~(a&b);

3'b011:y=~(a|b);	

3'b100:y=a^b; 

3'b101:y=a+b;	 

3'b110:y=a-b;	

3'b111:y=a*b;	

default:y=32'bx;

endcase

end 

endmodule

Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Creating a Test Bench:
Similarly, create your test bench using gedit <filename_tb>.v to open a new blank document (alu_case_tb.v).

#### Test Bench :
module alu_case_tb; 

reg [31:0]a;

reg [31:0]b;

reg [2:0]f;

wire [31:0]y;

alu_case dut(.y(y),.a(a),.b(b),.f(f)); initial

begin a=32'h00000000;

b=32'h00110001;

#10 f=3'b000;

#10 f=3'b001;

#10 f=3'b010;

#10 f=3'b011;

#10 f=3'b100;

#10 f=3'b101;

#10 f=3'b110;

#10 f=3'b111;

end 

initial

#100 $finish; 

endmodule

Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Source Code - Using If Statement :
module alu_ifelseif(y,a,b,f);

input [31:0]a;

input [31:0]b;

input [2:0]f; 

output reg [31:0]y;

always@(*)

begin

if(f==3'b000)

y=a&b;	

else if (f==3'b001)

y=a|b;	

else if (f==3'b010)

y=~(a&b); 

else if (f==3'b011)

y=~(a|b);	

else if (f==3'b100)

y=a^b;	

else if (f==3'b101)

y=a+b;  

 else if (f==3'b110)
 
y=a-b;	

else if (f==3'b111)

y=a*b;

else

y=32'bx; 

end 

endmodule

#### Test Bench :
module alu_ifelseif_tb;

reg [31:0]a;

reg [31:0]b;

reg [2:0]f;

wire [31:0]y;

alu_ifelseif dut(.y(y),.a(a),.b(b),.f(f));

initial

begin 

a=32'h00000000; 

b=32'h00110001;

#10 f=3'b000;

#10 f=3'b001;

#10 f=3'b010;

#10 f=3'b011;

#10 f=3'b100;

#10 f=3'b101;

#10 f=3'b110;

#10 f=3'b111;

end initial

#100 $finish;

endmodule

Functional Simulation for each design

Invoke the cadence environment by typing the commands below

tcsh (Invokes C-Shell)

source /cadence/install/cshrc (mention the path of the tools)

(The path of cshrc could vary depending on the installation destination)

After this, you can see the window like below

To Launch the Simulation tool

•linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design

or

•linux:/> nclaunch& // On subsequent calls to NCVERILOG

It will invoke the nclaunch window for functional simulation. We can compile, elaborate and simulate it using Multiple Steps.

Setting Multi-step simulation

Select Multiple Step and then select “Create cds.lib File” as shown in the figure below

Click the .cds.lib file and save the file by clicking on the Save option

Fcds.lib file Creation

Save .lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used.

Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in the figure below.

We are simulating a verilog design without using any libraries

Click “OK” in the “nclaunch: Open Design Directory” window, as shown in the figure below

#### Fig 2: Selection of Don’t include any libraries
An ‘NCLaunch window’ appears as shown in the figure below

Left side, you can see the HDL files. The right side of the window has Worklib and snapshots directories listed.

Worklib is the directory where all the compiled codes are stored, while Snapshot will have the output of elaboration, which in turn goes for simulation.

To perform the function simulation, the following three steps are involved: Compilation, Elaboration and Simulation.
<img width="1919" height="1079" alt="Screenshot 2025-11-21 164857" src="https://github.com/user-attachments/assets/9777d688-3c9f-4f3b-86fc-e32664e97d1c" />


#### Fig 3: Nclaunch Window
<img width="1920" height="1080" alt="Screenshot 2025-11-21 165041" src="https://github.com/user-attachments/assets/320bcaa2-dc4e-41bd-8653-a0fa172b1360" />


#### Step 1: Compilation:
– Process to check the correct Verilog language syntax and usage

Inputs: Supplied are Verilog design and test bench codes

Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file

#####  Steps for compilation:
	Create work/library directory (most of the latest simulation tools creates automatically)
 
	Map the work to library created (most of the latest simulation tools creates automatically)
 
 Run the compile command with compile options
 
i.e Cadence IES command for compile: ncverilog +access+rwc -compile filename.v

Left side select the file and in Tools: launch verilog compiler with current selection will get enable. Click it to compile the code

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation

#### Fig 4: Compiled database in WorkLib
After compilation, it will come under worklib. You can see on the right side window

select the test bench and compile it. It will come under Worklib. Under Worklib, you can see the module and test bench.

The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib”

<img width="1920" height="1080" alt="Screenshot 2025-11-21 164925" src="https://github.com/user-attachments/assets/1fc24139-3507-41c0-ab0a-c0f8bdfabf54" />

#### Step 2: Elaboration:
To check the port connections in a hierarchical design

Inputs: Top-level design/test bench Verilog codes

Outputs: Elaborate database updated in the mapped library if successful, generates a report, else error reported in the log file

#####  Steps for elaboration

– Run the elaboration command with elaborate options

1.It builds the module hierarchy

2. Binds modules to module instances
   
3.Computes parameter values

4. Checks for hierarchical name conflicts
   
5.It also establishes net connectivity and prepares all of this for simulation

After elaboration, the file will come under snapshot. Select the test bench and simulate it.

#### Fig 5: Elaboration Launch Option
<img width="1920" height="1080" alt="Screenshot 2025-11-21 165209" src="https://github.com/user-attachments/assets/5be670b7-473f-46af-b283-ea6e90bddd01" />


#### Step 3: Simulation:
– Simulate with the given test vectors over a period of time to observe the output behaviour.

Inputs: Compiled and Elaborated top-level module name

Outputs: Simulation log file, waveforms for debugging

Simulations allow dumping design and test bench signals into a waveform

Steps for simulation – Run the simulation command with simulator options

#### Fig 6: Design Browser window for simulation
<img width="1920" height="1080" alt="Screenshot 2025-11-21 165209" src="https://github.com/user-attachments/assets/dac05322-11a4-4501-8b83-297eb80dd29a" />


#### Fig 7: Simulation Waveform Window

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)
<img width="1920" height="1080" alt="Screenshot 2025-11-21 165248" src="https://github.com/user-attachments/assets/a26c92ce-d9ad-4c9c-8277-a4b0595b9be2" />
<img width="1920" height="1080" alt="Screenshot 2025-11-21 173056" src="https://github.com/user-attachments/assets/f136a3a8-d79f-4853-85bf-30a12cfde8bc" />


##### Performing Synthesis

##### Synthesize Design

Run the synthesis Process one time for each code and make sure the output File names are changed accordingly

The Liberty files are present in the library path,

• The Available technology nodes are 180nm,90nm and 45nm.

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist. Or use source run.tcl command in the terminal window to view the netlist, and a log file will be created in the working folder.


#### Fig 8: Synthesis RTL Schematic using case and ifelseif construct
<img width="1920" height="1080" alt="Screenshot 2025-11-21 173533" src="https://github.com/user-attachments/assets/64c06d5e-5ad0-49f1-aa8a-2c3510896112" />
<img width="1920" height="1080" alt="Screenshot 2025-11-21 173600" src="https://github.com/user-attachments/assets/06665f65-3f5c-41da-a5b6-3fb72d59866e" />


#### Fig 9: Area report of case and ifelseif construct
<img width="1920" height="1080" alt="Screenshot 2025-11-21 173638" src="https://github.com/user-attachments/assets/dbe52c75-68b8-4a0e-8e88-913a26066c86" />
<img width="1920" height="1080" alt="Screenshot 2025-11-21 174844" src="https://github.com/user-attachments/assets/ca4a8ec7-93a7-432e-8d67-5f8e8c3a7dfb" />


#### Fig 10: Power Report of case and ifelseif construct
<img width="1920" height="1080" alt="Screenshot 2025-11-21 173653" src="https://github.com/user-attachments/assets/b0b40805-aea2-4c93-84f7-321e48cf6520" />
<img width="1920" height="1080" alt="Screenshot 2025-11-21 174856" src="https://github.com/user-attachments/assets/801d80fb-61d6-48c8-8085-fe7284def7d6" />


#### Fig 11: Timing Report of case and ifelseif construct

#### Fig 12: Tabulate Area,Power and Timing Report Comparision of ALU using case and ifelseif construct

