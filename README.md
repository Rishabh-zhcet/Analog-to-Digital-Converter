# Design of a 4-bit Counter Type/Ramp Type Analog to Digital converter (ADC)
This repository presents the mixed signal design of a Counter Type/Ramp Type ADC. The Digital part of the circuit i.e 4- bit counter is simulated on Makerchip tool. All the Simulations are done using Esim and Makerchip tool only. Since the counter used is taken to be 4-Bit, the input voltage that can be converted to analog is limited to 0-15V. A 4-Bit Digital to Analog Converter (DAC) is used as an internal part, having the step size of 1V. 

[Click here](#https://www.canva.com/design/DAE_ARAM0e0/3zj51QhXWdK71QGhxEL8Yw/view?utm_content=DAE_ARAM0e0&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink) to view the complete project presentation video.

# Table of Contents:
* [Introduction](#Introduction)
* [Tool Used](#Tool-Used)
    * [eSim](#eSim)
    * [NgSpice](#NgSpice)
    * [Makerchip](#Makerchip)
    * [Verilator](#Verilator)
* [Refrence Circuit Diagram](#Refrence-Circuit-Diagram)
* [Expected Waveform](#Expected-Waveform)
* [Methodology](#Methodology)
    * [Design of 4 Bit BWR (Binary Weighted Resistor) type DAC](#Design-of-4-Bit-BWR-(Binary-Weighted-Resistor)-type-DAC)
* [Schematic](#Schematic)
* [Verilog Code For Counter in Makerchip](#Verilog-Code-For-Counter-in-Makerchip)
* [Counter Simulation in Makerchip](#Counter-Simulation-in-Makerchip)
* [Project Simulation Plots](#Project-Simulation-Plots)
   * [NgSpice Plot](#NgSpice-Plot)
   * [Gaw Plot](#Gaw-Plot)
* [Explaination-Why taking negative polarity input](#Explaination-Why-taking-negative-polarity-input)
* [Generated Netlist](#Generated-Netlist)
* [Result](#Result)
* [Generation of Counter Model using Ngveri Tab](#Generation-of-Counter-Model-using-Ngveri-Tab)
* [Steps to Run Simulation of Project](#Steps-to-Run-Simulation-of-Project)
* [Reference](#Reference)
* [Acknowledgment](#Acknowledgment)
* [Author](#Author)

# Introduction

Analog to Digital Converter is an electronic device that converts the analog data into digital form. Due to various advantages of the digital signals over analog signals such as easy processing and storage. The analog signal are converted into digital signals and the processing is done, after processing the signal it is converted back to analog form to get the original output. In this conversion from Analog to Digital, ADCs plays a vital role. 

In this paper we will study about Counter type/ Ramp type ADC. It consists of following components such as: Counter, DAC, AND gate, Op-Amp. The block diagram of the Counter type/ Ramp type DAC is shown in the figure 1. 

In Counter/Ramp type ADC, the analog voltage to be converted is applied to non-inverting terminal of the Op-Amp based comparator Circuit and the inverting terminal of comparator is connected to the output of the DAC. For the conversion, the binary counter is initially RESET and hence the output of the output of the DAC is 0V. The analog input applied to comparator is continuously compared with the DAC output during the conversion. If the analog input is greater than the DAC output, the comparator output is High and the counter is incremented and so the output from the DAC. Now again the DAC output is compared with the applied input if again input voltage (VA) is greater than the
applied voltage, the counter is increment and so the DAC output. This process is repeated until the DAC output becomes greater than the applied input voltage by some threshold VT volts and the output of the comparator becomes Low.

# Tool Used

### eSim

eSim (previously known as Oscad / FreeEDA) is a free/libre and open source EDA tool for circuit design, simulation, analysis and PCB design. It is an integrated tool built using free/libre and open source software such as KiCad, Ngspice, Verilator, makerchip-app, sandpiper-saas and GHDL. eSim is released under GPL.

eSim offers similar capabilities and ease of use as any equivalent proprietary software for schematic creation, simulation and PCB design, without having to pay a huge amount of money to procure licenses. Hence it can be an affordable alternative to educational institutions and SMEs. It can serve as an alternative to commercially available/licensed software tools like OrCAD, Xpedition and HSPICE.

For more details refer:
https://esim.fossee.in/home

### NgSpice

NgSpice is the open source spice simulator for electric and electronic circuits. Such a circuit may comprise of JFETs, bipolar and MOS transistors, passive elements like R, L, or C, diodes, transmission lines and other devices, all interconnected in a netlist. Digital circuits are simulated as well, event driven and fast, from single gates to complex circuits. And you may enter the combination of both analog and digital as a mixed-signal circuit.

For more details refer:
http://ngspice.sourceforge.net/docs.html

### Makerchip

It is an Online Web Browser IDE for Verilog/System-verilog/TL-Verilog Simulation. 

For More Details Refer:
https://www.makerchip.com/

### Verilator

It is a tool which converts Verilog code to C++ objects. 

For More Details Refer:
https://www.veripool.org/verilator/

# Refrence Circuit Diagram

<p align="center" width="100%">

   <img width="70%" src="https://user-images.githubusercontent.com/65393666/157244403-f671f3cb-c73f-40b5-b94b-fdc5db8d8e6f.png">
   
</p>

<p align="center">
<b>Fig:1 Reference Circuit of Counter Type/ Ramp Type</b></br>
</p>

# Expected Waveform

<p align="center" width="100%">

   <img width="50%" src="https://user-images.githubusercontent.com/65393666/157245675-5bc4f9ef-db2a-44a0-b419-90cc7cafa69b.jpg">
   
</p>

<p align="center">
<b>Fig:2 Reference waveform of 4-Bit Counter Type ADC</b></br>
</p>

# Methodology

In counter-type ADC, a low signal on reset initiates the A/D conversion. As conversion begins, we get the digital equivalent output at the output of the counter The output of the counter is then applied to a DAC(Digital to Analog Converter). Furthur the DAC output is compared with the applied analog input voltage. The output of this comparator controls the clock signal of the counter. As long as the applied analog signal is greater than the DAC output, the output of the comparator remains High and the counter is incremented. A time is reached when the DAC output becomes greater than the applied voltage by a threshold voltage VT then the output of the comparator becomes Low and the clock to the counter is disabled. At this time the digital signal available on the output of the counter is the digital equivalent of applied analog input voltage. So as we need to design a DAC which is the internal part of this ADC.

### Design of 4 Bit BWR (Binary Weighted Resistor) type DAC

<p align="center" width="100%">

   <img width="100%" src="https://user-images.githubusercontent.com/65393666/157255307-2de4ddc0-0c17-49ff-9be2-38b43ebbb1c8.png">
   
</p>

<p align="center">
<b>Fig:3 Circuit Diagram of BWR Type DAC</b></br>
</p>
 
# Schematic

<p align="center" width="100%">

   <img width="100%" src="https://user-images.githubusercontent.com/65393666/157297123-edc82c82-b07a-4c4f-8ab8-fc30cb06ee61.png">
   
</p>

<p align="center">
<b>Fig:4 Schematic of Couter/Ramp Type ADC(Analog to Digital Converter)</b></br>
</p>

# Verilog Code For Counter in Makerchip

```
\TLV_version 1d: tl-x.org
\SV
/* verilator lint_off UNUSED*/  /* verilator lint_off DECLFILENAME*/  /* verilator lint_off BLKSEQ*/  /* verilator lint_off WIDTH*/  /* verilator lint_off SELRANGE*/  /* verilator lint_off PINCONNECTEMPTY*/  /* verilator lint_off DEFPARAM*/  /* verilator lint_off IMPLICIT*/  /* verilator lint_off COMBDLY*/  /* verilator lint_off SYNCASYNCNET*/  /* verilator lint_off UNOPTFLAT */  /* verilator lint_off UNSIGNED*/  /* verilator lint_off CASEINCOMPLETE*/  /* verilator lint_off UNDRIVEN*/  /* verilator lint_off VARHIDDEN*/  /* verilator lint_off CASEX*/  /* verilator lint_off CASEOVERLAP*/  /* verilator lint_off PINMISSING*/    /* verilator lint_off BLKANDNBLK*/  /* verilator lint_off MULTIDRIVEN*/   /* verilator lint_off WIDTHCONCAT*/  /* verilator lint_off ASSIGNDLY*/  /* verilator lint_off MODDUP*/  /* verilator lint_off STMTDLY*/  /* verilator lint_off LITENDIAN*/  /* verilator lint_off INITIALDLY*/    

//Your Verilog/System Verilog Code Starts Here:
module Rishabh_counter(
input clk,
   input rst,
   output reg [3:0] out
);      		
                   	          	
// student code here
always@(posedge clk) begin
if(rst) 
out<=0;
else
out<=out+1;
end
endmodule 

//Top Module Code Starts here:
	module top(input logic clk, input logic reset, input logic [31:0] cyc_cnt, output logic passed, output logic failed);
		logic  rst;//input
		logic  [3:0] out;//output
//The $random() can be replaced if user wants to assign values
		assign rst = 0;
		Rishabh_counter Rishabh_counter(.clk(clk), .rst(rst), .out(out));
	
\TLV
//Add \TLV here if desired                                     
\SV
endmodule
```

# Counter Simulation in Makerchip

<p align="center" width="100%">

   <img width="100%" src="https://user-images.githubusercontent.com/65393666/157283491-9b422b9a-11f5-4d52-982f-b1c82d46a595.png">
   
</p>

<p align="center">
<b>Fig:5 4-Bit Counter Simulation on Makerchip Platform  </b></br>
</p>

# Project Simulation Plots

### NgSpice Plot

<p align="center" width="100%">

   <img width="50%" src="https://user-images.githubusercontent.com/65393666/157292185-ca1e473b-9e0b-4f4a-9aa8-e616e73552d3.png">
   
</p>

<p align="center">
<b>Fig:6.1  Reset Signal Plot</b></br>
</p>

<p align="center" width="100%">

   <img width="50%" src="https://user-images.githubusercontent.com/65393666/157292387-b19b8252-5dd5-4898-aa66-96b8f6b7e69c.png">
   
</p>

<p align="center">
<b>Fig:6.2  Clock Signal Plot </b></br>
</p>

<p align="center" width="100%">

   <img width="50%" src="https://user-images.githubusercontent.com/65393666/157292573-af4313a6-c14e-402f-8f31-933289c04faa.png">
   
</p>

<p align="center">
<b>Fig:6.3 Analog Input and Staircase Output </b></br>
</p>

<p align="center" width="100%">

   <img width="50%" src="https://user-images.githubusercontent.com/65393666/157292672-53848402-4c53-4fa8-a2fd-0c575fb4a718.png">
   
</p>

<p align="center">
<b>Fig:6.4 Digital Output From Counter</b></br>
</p>



### Gaw Plot

<p align="center" width="100%">

   <img width="100%" src="https://user-images.githubusercontent.com/65393666/157295526-b164e999-4408-4958-882f-60562df43a3a.png">
   
</p>

<p align="center">
<b>Fig:7 Complete ADC waveform Containing All the Signals </b></br>
</p>

### Explaination-Why taking negative polarity input?

As we know that the output fromt the BWR DAC comes with negative polarity. So for comparision with the comparator, we have to apply the analog input voltage with the negative polarity. This is done for the simulation purpose. In physical circuit, we can connect input to the comparator with reversed polarity.

# Generated Netlist

```
* /home/vrishabh70086/Desktop/ADC/ADC.cir

* EESchema Netlist Version 1.1 (Spice format) creation date: Mon 07 Mar 2022 05:46:20 PM UTC

* To exclude a component from the Spice Netlist add [Spice_Netlist_Enabled] user FIELD set to: N
* To reorder the component spice node sequence add [Spice_Node_Sequence] user FIELD and define sequence: 2,1,0

* Sheet Name: /
U4  Net-_U4-Pad1_ Net-_U4-Pad2_ Net-_U4-Pad3_ Net-_U4-Pad4_ Net-_U4-Pad5_ Net-_U4-Pad6_ rishabh_counter		
U6  gated_clk Net-_U5-Pad5_ Net-_U4-Pad1_ d_and		
X1  ? Vin staircase_op Net-_X1-Pad4_ ? Comp Net-_X1-Pad7_ ? lm_741		
X2  ? Net-_R3-Pad2_ GND Net-_X1-Pad4_ ? staircase_op Net-_X1-Pad7_ ? lm_741		
R4  Net-_R3-Pad2_ o3 1k		
R5  Net-_R3-Pad2_ o2 2k		
R6  Net-_R3-Pad2_ o1 4k		
R7  Net-_R3-Pad2_ o0 8k		
R3  staircase_op Net-_R3-Pad2_ 1.6k		
U7  Net-_U4-Pad3_ Net-_U4-Pad4_ Net-_U4-Pad5_ Net-_U4-Pad6_ o3 o2 o1 o0 dac_bridge_4		
v4  GND Net-_X1-Pad4_ 15		
v5  Net-_X1-Pad7_ GND 15		
U5  Net-_R1-Pad2_ Comp reset gated_clk Net-_U5-Pad5_ Net-_U4-Pad2_ adc_bridge_3		
v1  clk GND pulse		
v2  reset GND pulse		
v3  GND Vin 9.8		
R1  clk Net-_R1-Pad2_ 1k		
R2  Net-_R1-Pad2_ GND 1k		
U1  clk plot_v1		
U2  reset plot_v1		
U3  Vin plot_v1		
U8  o3 plot_v1		
U9  o2 plot_v1		
U10  o1 plot_v1		
U11  o0 plot_v1		
U12  staircase_op plot_v1		
U13  Comp plot_v1		
U14  gated_clk plot_v1		

.end
```

# Generation of Counter Model using Ngveri Tab

1. Open eSim
2. Run NgVeri-Makerchip
3. Add top level verilog file in Makerchip Tab
4. Click on NgVeri tab
5. Add dependency files
6. Click on Run Verilog to NgSpice Converter
7. Debug if any errors
8. Model created successfully

# Steps to Run Simulation of Project

1. Open a new terminal
2. Clone this project using the following command:
3. git clone https://github.com/Rishabh-zhcet/Analog-to-Digital-Converter.git
4. Change directory:
5. cd ADC_project_files
6. Run ngspice:
7. ngspice ADC.cir.out
8. To run the project in eSim:
9. Run eSim
10. Load the project
11. Open eeSchema


# Reference

[1] https://www.elprocus.com/counter-type-adc-analog-to-digitalconverter/

[2] https://www.electronics-tutorial.net/analog-integrated-circuits/dataconverters/counter-type-adc/

# Acknowledgment

1. FOSSEE, IIT Bombay
2. Steve Hoover, Founder, Redwood EDA
3. Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd. - kunalpghosh@gmail.com
4. Sumanto Kar, eSim Team, FOSSEE

# Author

[Rishabh Verma](https://github.com/Rishabh-zhcet), B.Tech Electronics Engineering, Zakir Husain College of Engineering and Technology (ZHCET), Aligarh Muslim University(AMU).
