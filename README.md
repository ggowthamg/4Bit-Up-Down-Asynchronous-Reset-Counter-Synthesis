# 4Bit-Up-Down-Asynchronous-Reset-Counter-Synthesis

## Aim:

Synthesize 4Bit-Up-Down-Asynchronous-Reset-Counter design using Constraints and analyse reports, Timing, area and Power.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

◦ SDC (Synopsis Design Constraint) File (.sdc)

 ### Step 2 : Creating an SDC File

•	In your terminal type “gedit input_constraints.sdc” to create an SDC File if you do not have one.

•	The SDC File must contain the following commands;

create_clock -name clk -period 2 -waveform {0 1} [get_ports "clk"]

set_clock_transition -rise 0.1 [get_clocks "clk"]

set_clock_transition -fall 0.1 [get_clocks "clk"]

set_clock_uncertainty 0.01 [get_ports "clk"]

set_input_delay -max 0.8 [get_ports "rst"] -clock [get_clocks "clk"]

set_output_delay -max 0.8 [get_ports "count"] -clock [get_clocks "clk"]

i→ Creates a Clock named “clk” with Time Period 2ns and On Time from t=0 to t=1.

ii, iii → Sets Clock Rise and Fall time to 100ps.

iv → Sets Clock Uncertainty to 10ps.

v, vi → Sets the maximum limit for I/O port delay to 1ps.

### Step 3 : Performing Synthesis

The Liberty files are present in the library path,

• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh

◦ source /cadence/install/cshrc

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.
          read_libs  <Library Path>
          read_hdl counter.v
          elaborate
          read_sdc input_constraints.sdc 				
          syn_generic
          report_area
          syn_map
          report_area
          syn_opt 
          report_area					
          report_timing > counter_timing.txt			
          report_area > counter_area.txt			
          report_power > counter_power.txt			
          write_hdl > counter_netlist.v 				
          write_sdc > counter_output_constraints.sdc		
          gui_show

#### Synthesis RTL Schematic :
![WhatsApp Image 2024-11-22 at 15 47 36_b9fe2014](https://github.com/user-attachments/assets/7ec95ea7-9422-421d-b5b6-0425c30e23a6)

#### Area report:
![WhatsApp Image 2024-11-22 at 12 37 48_d218f66c](https://github.com/user-attachments/assets/cd6e3aa5-998f-4dd4-9c79-f6fc4e2ab78a)

#### Power Report:
![WhatsApp Image 2024-11-22 at 12 37 48_b786b315](https://github.com/user-attachments/assets/656c39df-ac59-448c-96cc-e44a2322fab2)

#### Timing Report: 
![WhatsApp Image 2024-11-22 at 12 37 48_8cdbf6a3](https://github.com/user-attachments/assets/92d2eb32-fbdb-414a-8986-38b3357a196d)

#### Result: 

The generic netlist has been created, and area, power, and timing reports have been tabulated and generated using Genus.





