# Advanced_PD-Tool-OpenLANE-SKY130
This repository contains all the contents studied and created during the Advanced Physical Design Workshop using OpenLANE and SKY130 PDK

Table of Contents ::

Introduction 
Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK 

Day 2 - Good floorplan vs bad floorplan and introduction to library cells

Day 3 - Design library cell using Magic Layout and ngspice Characterization

Day 4 - Pre-layout timing analysis and importance of good clock tree 

Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA


Introduction to Openlane flow:

OpenLane is representation of a RTL to GDSII flow which uses many opensource EDA tools like OpenRoad, Yosys, ABC, Fault, Qflow, Magic and a number of custom scripts for design exploration and optimization. And SKY130 is PDK used here.

<img width="501" alt="image" src="https://user-images.githubusercontent.com/38167491/215576986-f393b6ca-4193-4410-88e1-3594d81b96c1.png">

About PicoRV32 - project

PicoRV32 is a CPU core that implements the RISC-V RV32IMC Instruction Set. It can be configured as RV32I, RV32IC, RV32IM, or RV32IMC core; where the suffixes stand for:

M - Multiply extension
I - Base Integer Instructions
C - Compressed Instructions
PicoRV32 is free and open hardware licensed under the ISC license. All features and data-sheet related to picoRV32 core can be obtained here.


prep -design:
![image](https://user-images.githubusercontent.com/38167491/215578224-cfc7fd7f-49eb-43ea-a1ca-e3f182dde9da.png)

Synthesis:
![image](https://user-images.githubusercontent.com/38167491/215578260-ff705ac7-fdb1-4ba6-b4fd-4a2563c981de.png)

Task 1:

Find the Flop Ratio :

Number of Cells = 14876

Number of D-FF(sky130_fd_sc_hd__dfxtp_2) = 1613

Hence, Flop Coount = 1613/14876 = 0.1084 :: 10.84%



Floorplan:
![image](https://user-images.githubusercontent.com/38167491/215578701-25f9cc6d-6f81-43b8-965f-1f56e763a2ff.png)

![image](https://user-images.githubusercontent.com/38167491/215578467-79f0120a-3928-4df2-bed1-4049e2414176.png)

![image](https://user-images.githubusercontent.com/38167491/215578577-33a2cfa0-2229-4159-919c-9f20556f115a.png)

![image](https://user-images.githubusercontent.com/38167491/215578729-71f440a4-2de0-4ab5-b094-c3083131dce7.png)

Placement:

![image](https://user-images.githubusercontent.com/38167491/215578777-54888796-f64b-4338-934e-436fc6a7b205.png)

![image](https://user-images.githubusercontent.com/38167491/215578811-8e287f40-a78a-48d2-8f5b-017a0f0b2268.png)

![image](https://user-images.githubusercontent.com/38167491/215578879-230799cb-2de0-48ae-8be2-e1267cbbacb4.png)


![image](https://user-images.githubusercontent.com/38167491/215579013-3bbfb23d-75e4-4a8b-a560-402d63d3a4f1.png)

![image](https://user-images.githubusercontent.com/38167491/215579036-e3d66c15-613d-4cda-80c7-3b88e175ac0b.png)


Cell Design flow & Characterization :

Step 1 : Read the models and tech files from the layout.

Step 2 : Read the extracted SPICE Netlist.

Step 3 : Define the behavior of the buffer.

Step 4 : Read the sub-circuits of the inverters.

Step 5 : Add the necessary power sources.

Step 6 : Apply the stimulus.

Step 7 : Provide necessary capacitances.

Step 8 : Provide the necessary simulation command.

![image](https://user-images.githubusercontent.com/38167491/215579165-d42eacd0-bb62-46bb-9d67-eb5bfd734340.png)


Git clone
 
![image](https://user-images.githubusercontent.com/38167491/215579590-fefd5a98-3760-4a20-9a90-5e9b10ce140c.png)

Magic invoking:
 
![image](https://user-images.githubusercontent.com/38167491/215579689-1c823091-e59a-4cca-8353-0261fe5e86c4.png)
![image](https://user-images.githubusercontent.com/38167491/215579708-9dcba95e-e2da-43a0-95d3-4b28884809ce.png)

 
Spice netlist extraction for given inverter:
 
![image](https://user-images.githubusercontent.com/38167491/215580134-6258edb1-ff9d-44c3-899a-6a4edca9a656.png)

Output files:
![image](https://user-images.githubusercontent.com/38167491/215580167-a50780d2-576b-4537-a117-3cddd9308176.png)

Propagation Delay:

Reasons:
1)The negative propagation delay value might be because of wrong choose of Threshold value.

2)Because circuit is not designed in proper way – delay between 1st cell n next cell connected inside the circuit is high(maybe due to large distance/gap between both) – eventually input and output delays of that particular block gives negative prop delay.

![image](https://user-images.githubusercontent.com/38167491/215579308-5c257e1f-9299-4bf3-8353-217f16724354.png)


![image](https://user-images.githubusercontent.com/38167491/215580276-19fa97b2-f80c-43de-8696-84ff038a8843.png)

![image](https://user-images.githubusercontent.com/38167491/215580308-62e9380d-cfc1-454d-a7d2-7af6815d369a.png)

![image](https://user-images.githubusercontent.com/38167491/215580333-4912144d-9378-4d62-b4f4-e90d40b8863b.png)

![image](https://user-images.githubusercontent.com/38167491/215580358-7a3f1cbe-b166-4476-9794-837044cd7eb4.png)


![image](https://user-images.githubusercontent.com/38167491/215580396-18bf2f4c-2ae9-4f6b-b4b1-ba56921b5b41.png)



![image](https://user-images.githubusercontent.com/38167491/215580439-df9c162c-9b90-4973-93df-e953f34a0f5d.png)

Lab steps to execute OpenSTA with right timing libraries and CTS

openroad

read_lef /openLANE_flow/designs/picorv32a/runs/28-01_15-09/tmp/merged.lef

read_def /openLANE_flow/designs/picorv32a/runs/28-01_15-09/results/cts/picorv32a.cts.def

write_db pico_cts.db

read_db pico_cts.db

read_verilog /openLANE_flow/designs/picorv32a/runs/28-01_15-09/results/synthesis/picorv32a.synthesis_cts.v

read_liberty -max $::env(LIB_SLOWEST)

read_liberty -min $::env(LIB_FASTEST)

read_liberty $::env(LIB_SYNTH_COMPLETE)

link_design picorv32a

read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

set_propagated_clock [all_clocks]    

report_checks -path_delay min_max -format full_clock_expanded -digits 4

report_checks -path_delay min_max -field {slew trans net cap input_pin} -format full_clock_expanded -digits 4


\n



Step-by-step all commands to run in openlane for above executed flow:

docker

./flow.tcl -interactive

package require openlane 0.9

prep -design picorv32a

echo $::env ([Varible]) // our case = SYNTH_STRATEGY
// change the STRATEGY

set ::env(SYNTH_STRATEGY) "DELAY 0"

run_synthesis

init_floorplan

place_io

global_placement_or

detailed_placement

tap_decap_or

detailed_placement

run_cts

gen_pdn

run_routing

run_magic




```console
Fall Transition Time [From 80% to 20%] : 2.24387e-09 - 2.18111e-09 = 0.06276e-09 second = 0.06276 nanosecond

Similarly,
Cell Rise Delay [50% of the rise]: Output - Input = 2.21073e-09 - 2.14994e-09 = 0.06079e-09 second = 0.06079 nanosecond

Cell Fall Delay [50% of the fall]: 4.07758e-09 - 4.04994e-09 = 0.02764e-09 second = 0.02764 nanosecond

```


