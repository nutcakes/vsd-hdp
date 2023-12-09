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




</details>

## DAY 3
> Combinational and sequential optmizations

<details>
 <summary> 1# Introduction to optimizations </summary>



</details>
<details>
 <summary> 2# Combinational logic optimizations </summary>



</details>
<details>
 <summary> 3# Sequential logic optimizations </summary>



</details>
<details>
 <summary> 4# Sequential optimzations for unused outputs </summary>



</details>

## DAY 4
> GLS, blocking vs non-blocking and Synthesis-Simulation mismatch

<details>
 <summary> 1# GLS, Synthesis-Simulation mismatch and Blocking/Non-blocking statements </summary>



</details>
<details>
 <summary> 2# Labs on GLS and Synthesis-Simulation Mismatch </summary>



</details>
<details>
 <summary> 3# Labs on synth-sim mismatch for blocking statement </summary>



</details>

