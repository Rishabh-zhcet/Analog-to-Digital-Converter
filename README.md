# Design of a 4-bit Counter Type/Ramp Type Analog to Digital converter (ADC)
This repository presents the mixed signal design of a Counter Type/Ramp Type ADC. The Digital part of the circuit i.e 4- bit counter is simulated on Makerchip tool. All the Simulations are done using Esim and Makerchip tool only. Since the counter used is taken to be 4-Bit, the input voltage that can be converted to analog is limited to 0-15V. A 4-Bit Digital to Analog Converter (DAC) is used as an internal part, having the step size of 1V. 

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
* [Verilog Code For Counter](#Verilog-Code-For-Counter)
* [Counter Simulation in Makerchip](#Counter-Simulation-in-Makerchip)
* [Generation of Counter Model using Ngveri Tab](#Generation-of-Counter-Model-using-Ngveri-Tab)
* [Steps to Run Simulation of Project](#Steps-to-Run-Simulation-of-Project)
* [Project Simulation Plots](#Project-Simulation-Plots)
   * [NgSpice Plot](#NgSpice-Plot)
   * [Gaw Plot](#Gaw-Plot)
* [Generated Netlist](#Generated-Netlist)
* [Result](#Result)
* [Reference](#Reference)
* [Acknowledgment](#Acknowledgment)
* [Author](#Author)

# Introduction

Analog to Digital Converter is an electronic device that converts the analog data into digital form. Due to various advantages of the digital signals over analog signals such as easy processing and storage. The analog signal are converted into digital signals and the processing is done, after processing the signal it is converted back to analog form to get the original output. In this conversion from Analog to Digital, ADCs plays a vital role. 

In this paper we will study about Counter type/ Ramp type DAC. It consists of following components such as: Counter, DAC, AND gate, Op-Amp. The block diagram of the Counter type/ Ramp type DAC is shown in the figure 1. 

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

   <img width="50%" src="https://user-images.githubusercontent.com/65393666/157244403-f671f3cb-c73f-40b5-b94b-fdc5db8d8e6f.png">
   
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

 
