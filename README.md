# VSD-HDP
> A repository containing a detailed documentation of my progress in the [VSD-HDP](https://www.vlsisystemdesign.com/hdp/) program

* VSD-HDP Status:
     1. [DAY 0](#day-0)
     2. [DAY 1](#day-1)
     3. [DAY 2](#day-2)
     4. [DAY 3](#day-3)
     5. [DAY 4](#day-4)
     6. [DAY 5](#day-5)
     7. [DAY 6](#day-6)
     8. [DAY 7](#day-7)
     9. [DAY 8](#day-8)
     10. [DAY 9](#day-9)
     11. [DAY 10](#day-10)
     12. [DAY 11](#day-11)
     13. [DAY 12](#day-12)
     14. [DAY 13](#day-13)
     15. [DAY 14](#day-14)
     16. [DAY 15](#day-15)
     17. [DAY 16](#day-16)
     18. [DAY 17](#day-17)
     19. [DAY 18](#day-18)
     20. [DAY 19](#day-19)
     21. [DAY 20](#day-20)
     22. [DAY 21](#day-21)

## DAY 0
> Enviroment Prep Guide
<details>
<summary> yosys </summary>

Installation of OpenSource RTL synthesis tool - Yosys
```bash
$ apt install yosys
```
![yosys](https://github.com/nutc4k3/vsd-hdp/assets/25620946/b184573f-9d18-4f45-9beb-8b75ac438a1e)

</details>
 <details>
<summary> opensta </summary>
Installation of OpenSource gate level static timing verifier - OpenSta
      
```bash
sudo apt install cmake clang gcctcl swig bison flex
git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake ..
make
apt install opensta
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/9a10a693-b5ba-4ae0-8fb5-ea41204b4305)

</details>
 <details>
 <summary> ngspice </summary>

Installation of OpenSource Spice (analog electronic circuit) simulator - NgSpice

```bash
wget https://sourceforge.net/projects/ngspice/files/ng-spice-rework/old-releases/37/ngspice-37.tar.gz/download -o ngspice-37.tar.gz
tar -zxvf ngspice-37.tar.gz
cd ngspice-37
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
make
sudo make install
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/ac6a5e67-57df-4f20-bf7f-271b0b7df33e)

</details>
 <details>
 <summary> iverilog </summary>


 Installation of OpenSource Icarus Verilog Compilation System - iverilog:
  ```bash
sudo apt install iverilog
 ```
![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/21a91871-c916-480d-9b18-aadc9665ddb2)

</details>

 <details>
 <summary> gtkwave </summary>


Installation of OpenSource Electronic waveform viewer - gtkwave:
  ```bash
sudo apt install gtkwave
 ```
![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/64f7d6ed-e4bb-4b45-9ab5-90e1fcc44d5f)

</details>
<details>
 <summary> magic  </summary>


 Installation of OpenSource VLSI Layout tool - magic:
  ```bash
sudo apt install m4 tcsh csh libx11-dev libx11-dev tcl-dev tk-dev libcairo2-dev mesa-common-dev libglu1-mesa-dev libncurses-dev magic
 ```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/ae34f23e-0e8a-46cc-ae66-186437e8479f)

</details>

## DAY 1
> Introduction to Verilog RTL Design and Synthesis

<details>
 <summary> 1# Introduction to simulator, design and test bench </summary>

- Simulator is a tool for checking the design. The RTL design is a implementation of a spec. The intent of the spec needs to be verified by simulating the design. The tool used for this is iverilog.
- Design is the verilog code (or codes/files) which has the intended functionality to meet with the required spec.
- Test Bench is the setup to ensure the above situation happens by appling a stimulus (test_vector) to the design and checking its functionality.
- Simulation looks for changes on the input signals by evaluating the output. If there is no change in the input, evaluation does not happen.

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/9f057684-677d-4a0a-bbf7-0270b9054e78)

In iverilog, the simulation flow looks like this:

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/060988a9-028e-4167-a6bc-08ea1830d416)


</details>	
<details>
 <summary> 2# Labs using iverilog and gtkwave </summary>

Clone the below repo as it contains library and standard cells verilog modules (test_bench files, source files, lab files, etc)

```bash
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
```

1. Go to verilog_files folder, where the verilog files and its test_bench correspondence are located. To use it with iverilog, start by creating the output file (a.out):

```bash
iverilog good_mux.v tb_good_mux.v
```

2. Execute the a.out file to generate the VCD info as a .vcd file:

```bash
./a.out
```

3. View the VCD info in gtkwave:
```bash
gtkwave tb_good_mux.vcd
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/2b39b43a-4efe-4c29-b704-65f9990174c5)
uut (unit under test)/drag and drop selecting the inputs to the signals window and zoom fit to view the waveforms. Find Next End arrows allows to jump between transitions.

Files used:

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/83f385f9-0224-46ff-81b9-436f339ed689)
![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/fa9fecfc-e0fa-4e2a-8fd2-88078d6d45b4)

</details>
<details>
 <summary> 3# Introduction to Yosys and Logic synthesis </summary>

Yosys is the synthetizer used for converting the RTL to netlist (represantation of the design in standard cells and .lib), as represented below:
![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/d89f5468-cfa1-4fbb-ab34-56e1e5497a41)

It is important to verify the synthesis as well by comparing both vcd files (RTL tb output and netlist tb output), as follows:

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/c19db8ef-9348-4b40-9740-fd637593b2f9)

This means that the netlist and the RTL are simply two representations of the design. The netlist representing rhe design in terms of standard cells and the RTL in terms of behavior.

Logic Synthesis comes to resolve the problem of translating RTL code to Digital Logic Circuit form (Gate level translation + connecyions between the gates) by giving out the netlist file.

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/122d1e02-068f-41f1-9787-6c525521b896)

.lib is a collection of all standard cells or logical modules available, like the basic logical modules AND, OR, NOT, etc; as well as different flavors of these gates and their functionalities (slow, medium and fast versions/ 2, 3, 4 input versions).

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/7590b847-b4bc-4c69-8cbf-5330278aa863)
DFFa = flip flop A
DFFb = flip flop B
COMBI = Combinational logic
CLK = clock
Tclk = Max speed
Tcq_a = Propagation delay of DFFa
Tcombi = Propagation delay of COMBI
Tsetup_b = Setup time to reach the clock rate of DFFb
fclk (max clk freq) = 1/Tclk (minimum clock period needed) ---> performance

So, are faster cells needed? Yes, to increase performance until the required state, but we need slower cells to meet HOLD. The collection of these forms the .lib.
![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/3b18a82a-2ca2-4f2e-ad35-1fd5264be81f)

What we want is for DFFb capture whatever data was launched in the previous cycle from DFFa, not the one before. That is why we need HOLD. The interval between DFFa1 and DFFb1 should be greater than HOLD.

LOAD in Digital Logic Circuit is the capacitance, less capacitance between two transistors A and B, lesser the cell delay. Wider transistors, low delay -> more power and area as well. 
Constraints is the guidance offered to the synthetizer to select the best flavour of cells.
Synthesis example:
![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/fd0a8ccd-af47-49c4-b505-58a897daf023)


</details>
<details>
 <summary> 4# Labs using Yosys and Sky130 PDKs </summary>

The following commands show how to use yosys:
```bash
yosys
```

Once inside yosys, read_liberty command can be used to read libraries:
```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

The command to read the design is:
```bash
read_verilog good_mux.v
```

To synthesize the design we specify the module to use (good_mux):
```bash
synth -top good_mux
```

To generate the netlist:
```bash
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
To view the logic it realized in graphical form write show inside yosys:

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/08730852-683b-4c75-b953-f552f05880c4)

The commands to write the netlist are (the second simplify the netlist):
```bash
write_verilog good_mux_netlist.v
write_verilog -noattr good_mux_netlist.v
```
![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/9d8e2452-b7de-406c-9010-16ebeeb4fa21)

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/2b2b4780-0de9-4726-a2af-6db2fd02e4f3)


</details>

## DAY 2
> Timing libs, hierarchical vs flat synthesis and efficient flop coding styles

<details>
 <summary> 1# Introduction to timing .libs </summary>
Process, Voltage and Temperature (PVT) variations are key points to note when designing silicon, by reading out the .lib and standard verilog codes one can find important information about cell delay, features, specifications and behavioral functionalities.

</details>
<details>
 <summary> 2# Hierarchical vs Flat Synthesis </summary>
To explain Hierarchical vs Flat Synthesis the file of choice is multiple_modules.v:

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/9c8f6cd7-ffe9-420d-964b-176913900ae7)


...which can be represented as:

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/b5cc739e-acf3-4bf3-b01c-3263e9eb739a)

The difference can be seen on yosys, after following the same chain of commands presented before, the command flatten and show stating the module will be used to flatten the hierarchical design and check the logical representation:

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/61258857-79ab-4d1c-a8ec-1107fa84f51d)

```bash
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show multiple_modules
write_verilog -noattr multiple_modules_hier.v
```

Here the hierarchies are preserved:

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/08de784b-1b20-4a87-aeb8-f64af672aa5c)

After flatten command:

```bash
flatten
write_verilog -noattr multiple_modules_flat.v
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/f0761ab6-9e8f-4a83-815a-94c9d9bc5598)

The submodule synthesis (instead of top level as above) goes like this:

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top sub_module1
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/0f8213d9-4c0e-446d-9b4b-c24481d3f524)


</details>
<details>
 <summary> 3# Various Flop Coding Styles and optimization </summary>

The files used are as follows:
```bash
dff_asyncres_syncres.v
dff_asyncres.v
dff_async_set.v
dff_syncres.v
```
Why flops? In a combinational circuit, the propagation delay can be seen as a glitch, to stabilise the signal, flops come handy as they work only at the edge of the clock. To initialize the flop, the control pins of the flop, like reset or set, can be either synchronous (waits for clock) and/or asynchronous (irrespective of clock), sometimes causing race conditions. The two flavours are represented:

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/028bb802-66e8-4120-9f08-81831caf24c1)

To simulate, iverilog and gtkwave can be invoked.

```bash
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
gtkwave tb_dff_asyncres.vcd
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/dd98a88e-4277-4a00-96ff-482f21c0aeb7)

```bash
iverilog dff_async_set.v tb_dff_async_set.v
./a.out
gtkwave tb_dff_async_set.vcd
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/8b23cc12-8eda-4b1f-99a5-184801d1e4b5)

```bash
iverilog dff_syncres.v tb_dff_syncres.v
./a.out
gtkwave tb_dff_syncres.vcd
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/0e0b51bf-8470-42f0-987f-a0d5392e1bd8)

Now for synthesis, invoke yosys.
```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_asyncres.v
synth -top dff_asyncres
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/171b8f53-ea62-4101-ac7a-d1e1b2c2e0e4)

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_async_set.v
synth -top dff_async_set
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/3c19add2-55cd-4603-8c58-fe8ab160423c)

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_syncres.v
synth -top dff_syncres
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/ca88f38c-7e10-4563-bacc-2ff08e735755)

Optimizations enable logical implementations to happen with no hardware involved.

</details>

## DAY 3
> Combinational and sequential optmizations

<details>
 <summary> 1# Introduction to optimizations </summary>
Combinational logic optimisation bring power and area savings by squeezing the logic to get the most optimised design; Some techniques are Constant Propagation, which is a direct optimisation, and Boolean Logic Optimisation, like K-Map and Quine McKluskey done in the synthesis process.

One basic type of Sequential Logic optimisation is Sequential Constant propagation and it follows Q to have a constant value, for example in a flop where Q=0 it does not need to be retained in a circuit.
Other, more advanced, types of Sequential optimisations are not convered in the labs, but are:

- State: Optimisation of unused states
- Cloning: Physical aware synthesis, for example reduce physical distance.
- Retiming: For example spread/partitioning the logic based on timing analysis to work on higher frequencies.

</details>
<details>
 <summary> 2# Combinational logic optimizations </summary>

Files used for the lab:

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/cc209379-2a9c-4d4e-abb2-acfe2c40b3cd)
![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/f573f3b4-e85d-41b1-8f2a-3301d17904b3)

Commands inside yosys are the same as before, with the addition of opt_clean before linking to liberty, as shown below:
```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check.v
synth -top opt_check
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/e866e1df-591a-419f-9528-c8573731462d)
![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/0153a824-e325-4eb9-8c5d-fb5ee5b23418)

```bash
read_verilog opt_check2.v
synth -top opt_check2
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/af017ea0-9a7b-4a4f-b140-e63ef8f267c5)
![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/d154a1ac-87b6-4e5e-b560-8c26881f7668)

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check3.v
synth -top opt_check3
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/d60eaf62-f014-4806-a61b-16dc19a98228)
![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/8ea05a09-8869-4109-b6be-8e9aec415465)

```bash
read_verilog opt_check4.v
synth -top opt_check4
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/a1113426-a8ff-47fd-8554-bb4c4f1acd65)

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_module_opt.v
synth -top multiple_module_opt
flatten
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr multiple_module_opt_flat.v
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/62fcec7f-68dc-4774-87c7-554ef85db71c)


```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_module_opt2.v
synth -top multiple_module_opt2
flatten
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr multiple_module_opt2_flat.v
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/84996f47-2512-4e58-9c0f-bacf56f3505f)


</details>
<details>
 <summary> 3# Sequential logic optimizations </summary>

Files to be used:

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/73213f7c-3c9c-411e-965f-70a5f7325174)

Q behavior in dff_const1 and dff_const2:
![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/1a94e267-7ba4-4958-8f16-6c638cf224ae)
![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/fc717d2a-a31e-422f-828c-b9b0f096fa76)

Synthesis:

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const1.v
synth -top dff_const1
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/14a64e2b-7438-4790-9c43-d9ea3a1493a8)

```bash
read_verilog dff_const2.v
synth -top dff_const2
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![image](https://github.com/nutc4k3/vsd-hdp/assets/25620946/f96270ad-7d62-468e-b28e-b37dbec66725)

```bash
iverilog dff_const3.v tb_dff_const3.v
./a.out
gtkwave tb_dff_const3.vcd
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/4265baca-b2ce-4c4c-bac9-ed72b6558d6b)

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const3.v
synth -top dff_const3
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/12bed2c3-5595-4ccb-b97a-2307171abfcf)

```bash
iverilog dff_const4.v tb_dff_const4.v
./a.out
gtkwave tb_dff_const4.vcd
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/40ce72f6-c46f-46c1-a8c4-5a16afde55f5)


```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const4.v
synth -top dff_const4
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/c0b26e71-8c21-4f29-b957-8a72cf0de233)

```bash
iverilog dff_const5.v tb_dff_const5.v
./a.out
gtkwave tb_dff_const5.vcd
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/3993614a-c180-4d6a-829b-92ea134d8893)

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const5.v
synth -top dff_const5
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/ac7ade3c-e446-4bfd-9656-712db5cc4d0f)

</details>
<details>
 <summary> 4# Sequential optimizations for unused outputs </summary>

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt.v
synth -top counter_opt
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/802e2f70-de22-4029-b773-cbde23f49ea9)

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt2.v
synth -top counter_opt
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/4020bb5d-17de-4f87-9145-53a208384116)

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/7f929391-8cdf-4dc6-bad4-dca69e6b4521)


</details>

## DAY 4
> GLS, blocking vs non-blocking and Synthesis-Simulation mismatch

<details>
 <summary> 1# GLS, Synthesis-Simulation mismatch and Blocking/Non-blocking statements </summary>
The goal is to perform RTL simulation, synthesis and GLS simulation for ternary_operator_mux.v, bad_mux.v and blocking_caveat.v comparing the RTL and Gate level simulation results to remove mismatches and non desired statements.

</details>
<details>
 <summary> 2# Labs on GLS and Synthesis-Simulation Mismatch </summary>

Begin by checking the current waveform of the code (ternary_operator_mux.v):
```bash
iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/2becd2f5-96f4-4d02-b15f-89b83416dbc8)

Then, synthesize and write the GLS netlist:
```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog ternary_operator_mux.v
synth -top ternary_operator_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog -noattr ternary_operator_mux_net.v
show
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/14c5f071-5eab-4ada-a8e6-cd76fe0f7002)

Next, perform GLS simulation:
```bash
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/fac1e163-2b1a-4fb4-ba3d-ab98fc81263d)

Begin by checking the current waveform of the code (bad_mux.v):
```bash
iverilog bad_mux.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/6c24a91b-3cae-4104-a903-763b016b8d44)


Then, synthesize and write the GLS netlist:
```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog bad_mux.v
synth -top bad_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog -noattr bad_mux_net.v
show
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/316e1cec-a025-49cf-b57f-a24742a5cc6c)

Next, perform GLS simulation:
```bash
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_net.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/46b33c89-0e51-4941-aa9e-5c99ff2d0787)

</details>
<details>
 <summary> 3# Labs on synth-sim mismatch for blocking statement </summary>

Begin by checking the current waveform of the code (blocking_caveat.v):
```bash
iverilog blocking_caveat.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/36a1d5e3-3403-4e74-bc03-fe8b6be15521)

Then, synthesize and write the GLS netlist:
```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog blocking_caveat.v
synth -top blocking_caveat
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog -noattr blocking_caveat_net.v
show
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/6cc7159c-c8d4-41d3-a342-a7eb2e00b5aa)

Next, perform GLS simulation:
```bash
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/6cfb53a5-a75b-4aee-8f28-fb6fe8441e47)

</details>

## DAY 5
> Introduction to RISC-V ISA and GNU compiler toolchain

<img width="1316" alt="Screenshot 2024-01-22 at 14 20 48" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/32cb6c27-c527-4416-be62-11d23e7d6ebd">

<details>
 <summary> 1# Introduction to RISC-V basic keywords </summary>

<img width="1316" alt="Screenshot 2024-01-22 at 14 28 43" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/8219b13b-c590-456d-aaec-d34125891666">
<img width="1316" alt="Screenshot 2024-01-22 at 14 29 47" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/8ba98e54-115d-4b01-8f06-f93589754861">
<img width="1316" alt="Screenshot 2024-01-22 at 14 30 53" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/81383ecb-d2d1-4c4b-a416-b247bae6c41b">
<img width="1316" alt="Screenshot 2024-01-22 at 14 33 50" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/37a0c439-e2ec-45c2-a767-8f1d9de3030b">
<img width="1316" alt="Screenshot 2024-01-22 at 14 34 38" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/e3983682-1442-44b8-a796-e2a90a55c26a">
<img width="1316" alt="Screenshot 2024-01-22 at 14 37 16" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/1d47b64c-25af-4d48-a9ab-0f0621572511">

mulw and divw are multiply extensions of RV64M

<img width="1316" alt="Screenshot 2024-01-22 at 14 40 24" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/c50a8353-fa9b-48f0-9a61-383c6047d2e3">
<img width="1316" alt="Screenshot 2024-01-22 at 14 41 34" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/0ef65e63-20bb-41b5-b480-8a3951e51a6d">
<img width="1316" alt="Screenshot 2024-01-22 at 14 42 30" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/833bbdb7-d78f-4b78-b230-1e5b90ca9218">

```bash sum1ton.c
#include <stdio.h>

int main() {
     int i, sum = 0, n = 5;
     for (i=1; i <=n; ++i){
          sum +=1;
     }
     printf("Sum of numbers from 1 to %d is %d", n, sum);
     return 0;
}
```

<img width="506" alt="Screenshot 2024-01-22 at 14 53 26" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/2035141c-c439-4a30-9ff2-66d8793e247c">

</details>
<details>
 <summary> 2# Labwork for RISC-V software toolchain  </summary>

Installation can be made using the following script: [run.sh](https://github.com/kunalg123/riscv_workshop_collaterals/blob/master/run.sh)

Code:
```bash
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
riscv64-unknown-elf-objdump -d sum1ton.o |less
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
riscv64-unknown-elf-objdump -d sum1ton.o |less

riscv64-unknown-elf-gcc = to invoke the gcc compiler
 		-O1 = Specifies the optimization level. (O1 is moderate level of optimization and Ofast is highest level of optimization
			-mabi = This flag specifies the ABI (Application Binary Interface) to be used. In this case, it is set to lp64, which stands for "long 				and pointer 64-bit." This ABI defines the sizes of basic C types, such as int and pointers. lp64 means that int is 32 bits, and pointers and long types are 64 bits.
   			-march = specifies the target RISCV architecture and ISA, rv64i means a 64-bit RISC-V architecture with the base integer ISA.
  		-o = output file name and format
 			-c = input source file and name
          -d - dissassemble

After running -Ofast option 3 instructions got optimized.

riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.cc
spike pk sum1ton.o
spike -d pk sum1ton.o
: until pc 0 100b0 (run only until 100b0 memory address)
: reg 0 a2 (show contents of register a2)
: (press enter to run next instruction)
: reg 0 a2 (change in value to 0x1000)
: reg 0 a0
: (press enter and so on...)
: reg 0 sp (stack point register)
```
<img width="424" alt="Screenshot 2024-02-02 at 11 17 34" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/3d82c10e-484b-49f2-8db4-804a0b56f1ce">
<img width="741" alt="Screenshot 2024-02-02 at 11 18 04" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/282e49ff-f6b1-4453-874e-350c02238b2f">
<img width="459" alt="Screenshot 2024-02-02 at 11 18 43" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/fbf80153-a1b1-4d30-9f3d-96ee6f5b63f5">
<img width="742" alt="Screenshot 2024-02-02 at 11 19 02" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/a762085f-2546-48d6-ba8c-7236925781d3">

<img width="1280" alt="Screenshot 2024-01-22 at 15 23 46" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/0180f6f0-3417-47c8-9092-d1f38b0b0611">
<img width="1280" alt="Screenshot 2024-01-22 at 15 27 36" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/925101fd-09dc-4f9c-a696-f458d0a6ea77">
![spike](https://github.com/nutcakes/vsd-hdp/assets/154557310/f1d48da0-18f4-4e68-b7c8-83967fdfd5f1)



</details>
<details>
 <summary> 3# Integer number representation  </summary>

<img width="1293" alt="Screenshot 2024-01-25 at 15 48 35" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/2a15c1ed-2993-430c-8916-97c518333a77">
<img width="1293" alt="Screenshot 2024-01-25 at 15 52 45" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/e541073e-eca8-4d4b-ab53-e522427e10c6">
<img width="995" alt="Screenshot 2024-01-25 at 15 53 45" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/0b4b38bb-5ff8-4817-9cc0-7ed29490805d">
<img width="1220" alt="Screenshot 2024-01-25 at 15 56 30" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/092eae80-0fa0-459e-ae18-0032a85741ac">
<img width="1220" alt="Screenshot 2024-01-25 at 15 57 57" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/f041571d-3525-450a-883d-84ffe1d26397">

```bash
#include <stdio.h>
#include <math.h>

int main(){
	long long int max = (long long int) (pow2,63) -1);
	long long int min = (long long int) (pow2,63) * -1);
	printf("highest number represented by long long int is %lld\n", max);
	printf("lowest number represented by long long int is %lld\n", min);
	return 0;
}
```


![unisignedHighest](https://github.com/nutcakes/vsd-hdp/assets/154557310/5a4bd992-8ea1-4be2-963e-b01ab5c13cd2)
![unsignedHighest2](https://github.com/nutcakes/vsd-hdp/assets/154557310/f21976be-ed36-4d12-9c74-aba8d3933fb9)
![unsignedHighest3](https://github.com/nutcakes/vsd-hdp/assets/154557310/9f66b240-a815-44a5-9764-225bd8ecdcea)
![unsignedHighest4](https://github.com/nutcakes/vsd-hdp/assets/154557310/bedd05c2-d3d5-4584-801d-112bc3baee16)
![signedint](https://github.com/nutcakes/vsd-hdp/assets/154557310/6411a960-e440-4cdc-8f8d-40cefc17ccb3)
![signedint2](https://github.com/nutcakes/vsd-hdp/assets/154557310/5e5d35c2-060c-413e-b1b2-b16f34784031)
![signedint3](https://github.com/nutcakes/vsd-hdp/assets/154557310/3bb973ac-449b-4f92-906c-055ce95c4a97)
![signedint4](https://github.com/nutcakes/vsd-hdp/assets/154557310/695ef13e-d09d-4c46-b9ee-0bffba7ae432)
<img width="1107" alt="Screenshot 2024-02-09 at 14 40 29" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/0caabe90-8214-4b1b-b2f8-82b2f3f74f91">
![signedint5](https://github.com/nutcakes/vsd-hdp/assets/154557310/ce2a18d2-1062-46e1-afa4-2188c837f1fa)


</details>

## DAY 6
> Introduction to ABI and basic verification flow

<img width="1272" alt="Screenshot 2024-02-09 at 14 59 07" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/7e54502f-8c97-4bd9-8426-364b7fbbb45d">

<details>
 <summary> 1# Application Binary interface (ABI) </summary>

<img width="1272" alt="Screenshot 2024-02-09 at 15 11 12" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/3e8e61c2-f6de-4a9c-867d-1881c3ffe1e2">
<img width="1272" alt="Screenshot 2024-02-09 at 15 12 10" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/0758a0ea-160c-4c75-adb8-a7ec987dbab7">


<img width="1071" alt="Screenshot 2024-02-12 at 16 26 58" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/2e41f225-60cf-43e5-ad18-e97e8475b1fe">
<img width="1222" alt="Screenshot 2024-02-12 at 16 27 45" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/97291e08-7b38-4fd9-9f18-fcc092dbf3e0">


<img width="1222" alt="Screenshot 2024-02-12 at 16 30 01" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/3d772e14-2725-47ee-af0c-cb7904fc430d">
<img width="1222" alt="Screenshot 2024-02-12 at 16 30 13" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/858254b6-922e-4f6b-9df2-cf258b8c9530">


<img width="1222" alt="Screenshot 2024-02-12 at 16 31 11" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/0fc669c7-b49a-4db1-9003-15754982d591">
<img width="1222" alt="Screenshot 2024-02-12 at 16 32 27" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/3c8a3c54-a6c6-4df5-8e3c-75176f617687">


<img width="1222" alt="Screenshot 2024-02-12 at 16 58 21" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/4087f029-6585-48fe-8877-d218e3a3c5e5">
<img width="1222" alt="Screenshot 2024-02-12 at 16 59 03" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/7c2f9012-7e2d-4e77-b724-e3562b30c3a0">
<img width="1151" alt="Screenshot 2024-02-12 at 22 00 03" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/5bdb9309-4c18-49d5-9953-70a1c8f0a339">
<img width="1222" alt="Screenshot 2024-02-12 at 16 59 42" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/a54b5ae1-23b0-4657-9f0d-43f85e5e50ce">
<img width="1222" alt="Screenshot 2024-02-12 at 17 00 49" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/6ba3ecfb-1cb4-4d53-bb94-2e8e9e9fa8de">



<img width="1222" alt="Screenshot 2024-02-12 at 17 02 09" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/6ea813e0-c8e1-433c-bde0-811e0dc0e2c2">

</details>
<details>
 <summary> 2# Lab work using ABI function calls </summary>

<img width="927" alt="Screenshot 2024-02-16 at 18 33 57" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/74b2478d-5242-4f72-9da6-5f25fd5e2b06">

![1_1to9c](https://github.com/nutcakes/vsd-hdp/assets/154557310/b5676029-7d48-444c-b60d-9f70697c73c9)

![2_loadS](https://github.com/nutcakes/vsd-hdp/assets/154557310/dd55d73c-fcad-42d6-9a00-730d97ba3fb7)

![3_spike1to9load](https://github.com/nutcakes/vsd-hdp/assets/154557310/8854421e-a5a8-45f1-b2a4-1a77621ea5a5)

![4_objdump1to9](https://github.com/nutcakes/vsd-hdp/assets/154557310/0a55b6d5-a09d-45b3-9075-3890ffdd9223)

![5_2objdump1to9](https://github.com/nutcakes/vsd-hdp/assets/154557310/fb53ce36-7178-4c84-8362-44f18b82fcb1)

</details>
<details>
 <summary> 3# Basic verification flow using iverilog </summary>

<img width="942" alt="Screenshot 2024-02-16 at 18 59 40" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/86790fe5-ae2a-49de-a435-0195b3eff417">

```bash
After git clone https://github.com/kunalg123/riscv_workshop_collaterals.git, inside the folder "labs",
picorv32.v is the RISC V CPU
testbench.v is the testbench for the entire thing, where picorv32 is a uut
rv32im.sh is a script to convert the code to hex file, load it in the memory of picorv32 and run it.
```
<img width="416" alt="Screenshot 2024-02-16 at 19 08 28" src="https://github.com/nutcakes/vsd-hdp/assets/154557310/8991c551-d56a-4d66-9d46-0cc7d6e9a495">

![6_rv32imsh](https://github.com/nutcakes/vsd-hdp/assets/154557310/5c59f3d8-f425-4c45-9321-f1d578646f78)

</details>

## DAY 7
> A project of a display controller. Simulation for top level verilog and GLS.

<details>
 <summary> 1# Introduction </summary>
We are building a custom RISCV based application core for a specific application for 32 bit processor. Digital display boards, often referred to as electronic display boards, are devices used to visually convey information, data, or messages digitally. They are versatile tools employed in various settings for displaying a wide range of content. In this scenario, we are developing a simple display board where it contains 3 to 7-segment modules and a keypad matrix. The system accepts input from the keypad matrix to accept messages and displays the scrolling text.

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/f73a840f-bf85-4832-9f08-d4b33a62843d)

The system has two important components: Keypad matrix and a 7 segment display.The system has a push button (Display/Input mode) that tells whether it accepts input from the keypad matrix or continue displaying stored text. The system display each character at a time. Note that some letters such as K (K), M (M), V (V), W (W), X (X), and Z (Z) are completely unrecognizable by most people. We try to achieve simple scrolling effect. Shift each letter to left to accomodate the entire message. After each word, all display modules become blank for sometime and again starts to display the next part of a message. For this project, we display only characters available in the keypad. We can modify the code such that we can multiplex 4 characters for each button of the keypad and accomodate alphabets.

Delay circuit is a oscillator that produces squared waves with periods of 1.5s. With respect to this signal, the display changes the text. 555 timer circuit is used to produce a square signal of 1.5s. Since the clock frequency is unknown, we use the 555 timer as a reference for a absolute delay generation.

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/95166cbc-4192-49cf-b2a3-2a468520c5af)

![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/27563a6b-8c31-487f-813f-a2d9ba4f4e95)

Register architecture of x30 for GPIOs:
![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/52527e32-53c9-44bd-b473-0730d3411b84)

```bash
x30[3:0] is row pins of keypad.
x30[7:4] is column pins of keypad.
x30[14:8] is 7 segment display pins.
x30[25] is mode_led to indicate input / display mode of system. LED is ON if input mode else OFF for display mode.
x30[27] is next input which is used as enter button to store each character we enter.
x30[29] is delay pin where it accepts signal from 555 timer.
x30[31] is input/display mode input pin.
```

Binary codes for keypad:
![image](https://github.com/nutcakes/vsd-hdp/assets/154557310/fe2f27b1-d8a5-4520-92af-eaa84f8da5eb)
For row wise scanning process, we should put values as follows and then read column pins to determine the button.

| Buttons | Row | Column |
| --- | --- | --- |
| 1 | Put 1110 | read 1110 |
| 2 | Put 1110 | read 1101 |
| 3 | Put 1110 | read 1011 |
| A | Put 1110 | read 0111 |
| 4 | Put 1101 | read 1110 |
| 5 | Put 1101 | read 1101 |
| 6 | Put 1101 | read 1011 |
| B | Put 1101 | read 0111 |
| 7 | Put 1011 | read 1110 |
| 8 | Put 1011 | read 1101 |
| 9 | Put 1011 | read 1011 |
| C | Put 1011 | read 0111 |
| - | Put 0111 | read 1110 |
| 0 | Put 0111 | read 1101 |
| - | Put 0111 | read 1011 |
| D | Put 0111 | read 0111 |

7 segment hex code:
MSB in x30[14:8] is a and LSB in x30[14:8] is g segments in 7 segment display pins.

| Data | Binary code | 
| --- | --- |
| 1 | 0110000 |
| 2 | 1101101 |
| 3 | 1111001 |
| 4 | 0110011 |
| 5 | 1011011 |
| 6 | 1011110 |
| 7 | 1110000 |
| 8 | 1111111 |
| 9 | 1110011 |
| 0 | 0000000 |
| A | 1110111 |
| B | 0011111 |
| C | 1001110 |
| D | 0111101 |
| - | 0000001 |


<details>
C program:
```c 
int read_keypad(void);
void display1_output(int num);
void display_mode(int mode);

int read_next(void);
int read_mode(void);
int read_delay(void);


int main()
{
	int mode;
	int display1;
	int delay;
	int next;
	int keypad;
	int a=0,b=0,c=0,d=0,e=0,f=0,g=0,h=0,i=0,j=0;
	int count1=0;
	
	
	//initialize with hypen
	display1_output(1);
	
	
	while(1)
	{
		mode=read_mode();
		display_mode(mode);
		if(mode==1)//input new text
		{
			keypad=read_keypad();
			if(keypad!=0)
			{
				if(count1==0) a=keypad;
				else if(count1==1) b=keypad;
				else if(count1==2) c=keypad;
				else if(count1==3) d=keypad;
				else if(count1==4) e=keypad;
				else if(count1==5) f=keypad;
				else if(count1==6) g=keypad;
				else if(count1==7) h=keypad;
				else if(count1==8) i=keypad;
				else if(count1==9) j=keypad;
				else if(count1==10) count1=0;
				if(keypad!=1)
				{
					count1++;
					display1_output(keypad);
					next=read_next();
					while(next==0)
					{
						next=read_next();
					}
				}
				else
				{
					count1=0;
				}
				
			}
		}
		else if(mode==0)//display stored text
		{
			delay=read_delay();
			if(delay==1)
			{
				//end of text
				if(count1==0)
				{
					if(a==1)
					{
						count1=0;
						continue;
					}
					else display1_output(a);
				}
				
				else if(count1==1)
				{
					if(b==1)
					{
						count1=0;
						continue;
					}
					else display1_output(b);
				}
				
				else if(count1==2)
				{
					if(c==1)
					{
						count1=0;
						continue;
					}
					else display1_output(c);
				}
				
				else if(count1==3)
				{
					if(d==1)
					{
						count1=0;
						continue;
					}
					else display1_output(d);
				}
				
				else if(count1==4)
				{
					if(e==1)
					{
						count1=0;
						continue;
					}
					else display1_output(e);
				}
				
				else if(count1==5)
				{
					if(f==1)
					{
						count1=0;
						continue;
					}
					else display1_output(f);
				}
				
				else if(count1==6)
				{
					if(g==1)
					{
						count1=0;
						continue;
					}
					else display1_output(g);
				}
				
				else if(count1==7)
				{
					if(h==1)
					{
						count1=0;
						continue;
					}
					else display1_output(h);
				}
				
				else if(count1==0)
				{
					if(i==1)
					{
						count1=0;
						continue;
					}
					else display1_output(i);
				}
				
				else if(count1==8)
				{
					if(j==1)
					{
						count1=0;
						continue;
					}
					else display1_output(j);
				}
				else {count1=0;continue;}
				count1++;
				
			}
		}
	}
	return(0);
}
int read_keypad(void)
{
	int keypad;
	//unsigned char row[5]={14,13,11,7,0};
	//int row;
	int i=0;
	int mask=0xFFFFFFF0;
	
	
	//row 0
	//row=0x0000000E;
	if(i==0)
	{
		asm volatile(
		"and x30,x30,%0\n\t"
	    	"ori x30, x30, 14\n\t"
	    	:
	    	:"r"(mask)
	    	:"x30"
	    	);
	    	
	    	asm volatile(
	    	"andi %0, x30, 240\n\t"
	    	:"=r"(keypad)
	    	:
	    	:
	    	);
	    	if(keypad!=240) 
	    	{
	    		i=14;
	    	}
	}
	
	//row1
	//row=13;
	if(i==0)
	{
		asm volatile(
		"and x30,x30,%0\n\t"
	    	"ori x30, x30, 13\n\t"
	    	:
	    	:"r"(mask)
	    	:"x30"
	    	);
	    	
	    	asm volatile(
	    	"andi %0, x30, 240\n\t"
	    	:"=r"(keypad)
	    	:
	    	:
	    	);
	    	if(keypad!=240) 
	    	{
	    		i=13;
	    	}
	}
	//row2
	//row=11;
	if(i==0)
	{
		asm volatile(
		"and x30,x30,%0\n\t"
	    	"ori x30, x30, 11\n\t"
	    	:
	    	:"r"(mask)
	    	:"x30"
	    	);
	    	
	    	asm volatile(
	    	"andi %0, x30, 240\n\t"
	    	:"=r"(keypad)
	    	:
	    	:
	    	);
	    	if(keypad!=240) 
	    	{
	    		i=11;
	    	}
	}
	
	//row3
	//row=7;
	if(i==0)
	{
		asm volatile(
		"and x30,x30,%0\n\t"
	    	"ori x30, x30, 7\n\t"
	    	:
	    	:"r"(mask)
	    	:"x30"
	    	);
	    	
	    	asm volatile(
	    	"andi %0, x30, 240\n\t"
	    	:"=r"(keypad)
	    	:
	    	:
	    	);
	    	if(keypad!=240) 
	    	{
	    		i=7;
	    	}
	}
	if(i==0)//no button pressed
	{
		return 0;
	}
	else
	{
		if(i==14)//row=0
		{
			if(keypad==224) keypad=48;//1
			else if(keypad==208) keypad=109;//2
			else if(keypad==176) keypad=121;//3
			else if(keypad==112) keypad=119;//A
		}
		else if(i==13)//row=1
		{
			if(keypad==224) keypad=51;//4
			else if(keypad==208) keypad=91;//5
			else if(keypad==176) keypad=94;//6
			else if(keypad==112) keypad=31;//B
		}
		else if(i==11)//row=2
		{
			if(keypad==224) keypad=112;//7
			else if(keypad==208) keypad=127;//8
			else if(keypad==176) keypad=115;//9
			else if(keypad==112) keypad=78;//C
		}
		else if(i==7)//row=3
		{
			if(keypad==224) keypad=1;//-
			else if(keypad==208) keypad=127;//0
			else if(keypad==176) keypad=1;//-
			else if(keypad==112) keypad=61;//D
		}
	}
	
        
        return keypad;
}

int read_mode(void)
{
	int mode;//read whether controller is in display mode or input mode
	asm volatile(
	"srli x10, x30, 31\n\t"
	"andi %0, x10, 1\n\t"
	:"=r"(mode)
	:
        :"x10"
        );
        return mode;
}

void display1_output(int num)
{
	int mask=0xFFFF80FF;
	int temp=num*256;//shift by 8 bits to left to update display bits in x30
	asm volatile( 
	    "and x30, x30, %1\n\t"
	    "or x30, x30, %0\n\t"
	    :
	    :"r"(temp),"r"(mask)
	    :"x30"
	    );
}

void display_mode(int mode)//shift by 25 bits to left to update display mode led in x30
{
	int mask=0xFDFFFFFF;
	asm volatile(
	    "and x30, x30, %1\n\t"
	    "slli x10, %0, 25\n\t" 
	    "or x30, x30, x10\n\t"  
	    : 
	    :"r"(mode),"r"(mask)
	    :"x30","x10"
	    );
}
int read_delay(void)
{
	int delay;// read delay signal generated by external circuit 
	asm volatile(
	"srli x10, x30, 29\n\t"
	"andi %0, x10, 1\n\t"
        :"=r"(delay)
        :
        :"x10"
        );
        return delay;
}

int read_next(void)
{
	int next;// read next button to accpet next character of text.
	asm volatile(
	"srli x10, x30, 27\n\t"
	"andi %0, x10, 1\n\t"
        :"=r"(next)
        :
        :"x10"
        );
        return next;
}
```
</details>

 </details>
