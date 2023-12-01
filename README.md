# VSD-HDP
> A repository containing a detailed documentation of my progress in the [VSD-HDP](https://www.vlsisystemdesign.com/hdp/) program

* VSD-HDP Status Quick links:
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
<summary> Yosys & OpenSta </summary>

Installation of OpenSource RTL synthesis tool - Yosys
```bash
$ apt install yosys
```
![yosys](https://github.com/nutc4k3/vsd-hdp/assets/25620946/b184573f-9d18-4f45-9beb-8b75ac438a1e)

 
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
## DAY 1
> Tool Usage Warm Up

## DAY 2

  
  
