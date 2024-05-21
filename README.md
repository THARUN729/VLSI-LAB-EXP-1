# EXP.NO:01
# DATE:13/02/2024
# SIMULATION AND IMPLEMENTATION OF LOGIC GATES,ADDERS AND SUBTRACTOR
# AIM:
To simulate and synthesis Logic Gates,Adders and Subtractor using Xilinx ISE.

# APPARATUS REQUIRED:
Xilinx 14.7 Spartan6 FPGA

# PROCEDURE:
```
STEP:1 Start the Xilinx navigator, Select and Name the New project.
STEP:2 Select the device family, device, package and speed. 
STEP:3 Select new source in the New Project and select Verilog Module as the Source type.
STEP:4 Type the File Name and Click Next and then finish button. Type the code and save it.
STEP:5 Select the Behavioral Simulation in the Source Window and click the check syntax.
STEP:6 Click the simulation to simulate the program and give the inputs and verify the outputs as per the truth table.
STEP:7 Select the Implementation in the Sources Window and select the required file in the Processes Window.
STEP:8 Select Check Syntax from the Synthesize XST Process. Double Click in the Floorplan Area/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 
STEP:9 In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.
STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here. STEP:12 Load the Bit file into the SPARTAN 6 FPGA
STEP:11 On the board, by giving required input, the LEDs starts to glow light, indicating the output.
```

Logic Diagram :

Logic Gates:
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/ee17970c-3ac9-4603-881b-88e2825f41a4)


Half Adder:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/0e1ecb96-0c25-4556-832b-aeeedfdfe7b9)


Full adder:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/9bb3964c-438f-469d-a3de-c1cca6f323fb)


Half Subtractor:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/731470b7-eb4e-49f8-8bb7-2994052a7184)



Full Subtractor:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/d66f874b-c1f2-44b3-a035-7149b56430c1)



8 Bit Ripple Carry Adder

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/7385a408-40a5-4203-8050-b72818622d79)



VERILOG CODE:

# Logic Gates:
```
module logicgate (a,b,andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate);
input a,b;  
output andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate;
and(andgate,a,b);
or(orgate,a,b);
xor(xorgate,a,b);
nand(nandgate,a,b); 
nor(norgate,a,b);
xnor(xnorgate,a,b);
not(notgate,a);
endmodule
```

# Half Adder:
```
module halfadder(a,b,sum,carry);
input a,b;
output sum,carry;
xor g1(sum,a,b);
and g2(carry,a,b);
endmodule
```

# Half Subractor:
```
module halfsubtractor(a,b,diff,borrow);
input a,b;
output diff,borrow;
xor g1(diff,a,b);
and g2(borrow,~a,b);
endmodule
```

# Full Adder:
```
module fadd(a,b,c,sum,carry);
input a,b,c;
output sum,carry;
wire w1,w2,w3;
xor g1(w1,a,b);
and g2(w2,a,b);
xor g3(sum,w1,c);
and g4(w3,w1,c);
or g5(carry,w3,w2);
endmodule
```

# Full Subractor:
```
module fs(a,b,bin,d,bout);
input a,b,bin; 
output d,bout;
wire w1,w2,w3;
xor g1(w1,b,bin; 
xor g2(d,w1,a);
and g3(w2,a,~w1);
and g4(w3,~b,bin);
or g5(bout,w2,w3);
endmodule
```

# 4 bit ripple carry adder:
```

module rippe_adder(S,Cout,X,Y,Cin);
input [3:0] X,Y;
input Cin;
output [3:0] S;
output Cout;
wire w1,w2,w3;
fulladder u1(S[0],w1,X[0],Y[0],Cin);
fulladder u2(S[1],w2,X[1],Y[1],w1);
fulladder u3(S[2],w3,X[2],Y[2],w2);
fulladder u4(S[3],Cout,X[3],Y[3],w3);
endmodule

module fulladder(S,CO,X,Y,Ci);
input X,Y,Ci;
output S,CO;
wire w1,w2,w3;
xor G1(w1,X,Y);
xor G2(S,w1,Ci);
and G3(w2,X,Ci);
and G4(w3,X,Y);
or G5(CO,w3,w3);
endmodule
```

# 8 bit ripple carry adder:
```
module rippe_adder(S,Cout,X,Y,Cin);
input [7:0] X,Y;
input Cin;
output [7:0] S;
output Cout;
wire w1,w2,w3,w4,w5,w6,w7;
fulladder u1(S[0],w1,X[0],Y[0],Cin);
fulladder u2(S[1],w2,X[1],Y[1],w1);
fulladder u3(S[2],w3,X[2],Y[2],w2);
fulladder u4(S[3],w4,X[3],Y[3],w3);
fulladder u5(S[4],w5,X[4],Y[4],w4);
fulladder u6(S[5],w6,X[5],Y[5],w5);
fulladder u7(S[6],w7,X[6],Y[6],w6);
fulladder u8(S[7],Cout,X[7],Y[7],w7);
endmodule

module fulladder(S,CO,X,Y,Ci);
input X,Y,Ci;
output S,CO;
wire w1,w2,w3;
xor G1(w1,X,Y);
xor G2(S,w1,Ci);
and G3(w2,X,Ci);
and G4(w3,X,Y);
or G5(CO,w3,w3);
endmodule
```

OUTPUT:
# OR GATE:
![image](https://github.com/THARUN729/VLSI-LAB-EXP-1/assets/161407766/ac0a6cc3-0c75-487b-9b46-9e4ecee5a896)

# NOT GATE:
![image](https://github.com/THARUN729/VLSI-LAB-EXP-1/assets/161407766/f982114a-4ba1-4c5c-954a-a3ace2976b87)

# AND GATE:
![image](https://github.com/THARUN729/VLSI-LAB-EXP-1/assets/161407766/30d29087-a327-48d5-a893-b3b62e8f7dee)

# NAND GATE:
![image](https://github.com/THARUN729/VLSI-LAB-EXP-1/assets/161407766/8c002e62-b5ff-4a5b-8449-d2841fadf26d)

# NOR GATE:
![image](https://github.com/THARUN729/VLSI-LAB-EXP-1/assets/161407766/fd0deb65-98a1-4d59-9411-40342fada324)

# XNOR GATE:
![image](https://github.com/THARUN729/VLSI-LAB-EXP-1/assets/161407766/ed5eeefe-d669-42fc-9257-98e247c42aa4)

# XOR GATE:
![image](https://github.com/THARUN729/VLSI-LAB-EXP-1/assets/161407766/2c6f8a3b-f11d-40aa-8f1a-6fdaddd0f736)

# HALF ADDER:
![image](https://github.com/THARUN729/VLSI-LAB-EXP-1/assets/161407766/2526c894-3f22-45ff-8167-5c0a2f31627a)

# HALF SUBRACTOR:
![image](https://github.com/THARUN729/VLSI-LAB-EXP-1/assets/161407766/37350ed8-b67a-46d3-998d-6281d8009e81)

# FULL ADDER:
![image](https://github.com/THARUN729/VLSI-LAB-EXP-1/assets/161407766/6b673c60-8888-4644-871f-5c4558ca573c)

# FULL SUBRACTOR:
![image](https://github.com/THARUN729/VLSI-LAB-EXP-1/assets/161407766/ad5ae34d-a3ce-4a78-98f5-ed0e2df889c3)

# 4 BIT RIPPLE CARRY ADDER:
![image](https://github.com/THARUN729/VLSI-LAB-EXP-1/assets/161407766/346b42e8-9e86-4e2e-9773-5241f37c3304)

# 8 BIT RIPPLE CARRY ADDER:
![image](https://github.com/THARUN729/VLSI-LAB-EXP-1/assets/161407766/b483e3cc-c582-413e-96aa-7271961dc2e3)

















RESULT:
Hence Logic Gates,Adders and Subtractor are simulated and synthesised using Xilinx ISE.

