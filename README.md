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



</details>
<details>
 <summary> 3# Introduction to Yosys and Logic synthesis </summary>



</details>
<details>
 <summary> 4# Labs using Yosys and Sky130 PDKs </summary>



</details>

## DAY 2
> Timing libs, hierarchical vs flat synthesis and efficient flop coding styles

<details>
 <summary> 1# Introduction to timing .libs </summary>



</details>
<details>
 <summary> 2# Hierarchical vs Flat Synthesis </summary>



</details>
<details>
 <summary> 3# Various Flop Coding Styles and optimization </summary>



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

