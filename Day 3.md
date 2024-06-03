
## DAY 3: Design library cell using Magic Layout and ngspice characterization

### 1. GIT CLONE of "vsdstdcelldesign"

  1. First go to the directory of vsdstdcelldesign on github.
  2. Clone the github repo "https://github.com/nickson-jose/vsdstdcelldesign.git".

  Command: `git clone https://github.com/nickson-jose/vsdstdcelldesign.git`
  
 ![Day3_git_clone](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/6d2a705e-7cd7-460c-a5c6-36ed2d14b358)


  4. After the cloning is completed, copy the tech file.
  
  Command: `cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/`
  ![Day3_copy_tech](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/f51dcc6e-5543-4c43-8987-4c57b41345f5)
  ![day3_copy_list](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/899dfdfa-692a-484b-9854-2c5eb187aa74)




### 2. MAGIC TOOL (VSDSTDCELLDESIGN)

  1. Open MAGIC tool to see the standard cell design in the cloned directory location. Also the tkcon terminal for MAGIC will open.

  Command:
  `magic -T sky130A.tech sky130_inv.mag &`
  
  ![Day3_4_magic](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/38236596-13e6-42cf-910e-7bc7da71671f)
  ![Day3_5_layout](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/4d9a3428-8a37-476b-8e41-77644340349b)

  2. In the tool, use 's' and 'v' simultaneously to center the cell design.
  3. To select any part of the design, hover the mouse pointer to it and click 's' to select it.
  4. On the right hand side, all the layers are described.
  ![Day3_6](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/94c251d8-158b-4335-9094-4b26cdd7d53e)

  5. Using 's' 3x will select the whole connection layer where the mouse is pointed in the design.

  6. Now in the tkcon terminal, after selecting any part of the design using 's', type `what`. PMOS and NMOS has been decribed the terminal.
   ![day3_7_nmos](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/7c3c53b4-c722-489d-9962-086821405d64)
   ![day3_8_pmos](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/71d98626-3aa2-4b77-aaa0-a3a0be71520e)

  7. Go through the vlsistdcelldesign for more details on the cell design of the cloned github.
  8. MAGIC tool is also a DRC check tool and the design always has to be DRC clean. It can highlight the same and errors will be shown in the terminal.
  9. To know the logic, it has to be extracted to SPICE in ngspice:

     a. In the vlsistdcelldesign directory, use `extract all`.
        ![day3_9_eextract](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/1f9b96cb-b65a-40fc-b5c1-d309a5637d0b)

     
     b. Extracted file is created with .ext.
         ![day3_10_file](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/f2e129f7-9c03-411e-a9b7-8908e138629e)

     
     c. To use in the **ngspice** tool: `ext2spice cthresh 0 rthresh 0`. Does parasitic extraction as well.

     d. To create .spice file : ext2spice
         ![day3_11](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/7fc39f9e-b268-44ac-81b0-f6479afd666f)
         ![day3_12_list](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/1d56b1e7-eb2c-4758-bf3a-b3ef3d827899)
         ![day3_13_spice_file](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/339bc903-f494-4522-a1f3-e77c8ba4703e)

   
        > In the .spice file:
        > Contains the details of the PMOS and NMOS and its connection. Update the .spice file as below which includes the pshort and nshort libs, scale, pulse input and transient analysis commands.
        ![day3_14_modell](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/c5da8e0d-11d7-431a-af26-8525fa447792)

       
> For more information and working of MAGIC, go to "http://opencircuitdesign.com/magic/index.html"


### 3. NGSPICE

  1. After the file is saved, invoke the .spice file in ngspice `ngspice sky130_inv.spice`. If ngspice not available, use `sudo apt install ngspice`.
     ![day3_15_ngspice](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/49355b41-9ffa-47c1-ab56-9b716c5db7bd)

  2. Plot the graph using `plot y vs time a`.
    ![day3_17_plott](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/cbe1af40-4d7d-4863-9856-bd6c9b307d79)

  3. Calculate the cell rise and fall delays for PVT characteristics.
    ![day3_16_plot](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/6f667280-0902-498e-bc0e-58ad2bb5c0cd)



### 4. MAGIC TOOL (DRC)

1. For tutorial and more details go to the [opencircuitdesign](http://opencircuitdesign.com/magic/index.html) website.
2. For skywater pdks check [skywaterpdks](https://github.com/google/skywater-pdk)
3. Get the Magic drc open pdk using for lab.
   ```
   wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
   tar xfz drc_tests.tgz
   cd drc_tests
   ls -lrth
   ```
  ![Day3_magic_lab](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/b8b08b4a-c60b-43d0-821e-e6acf3a137a9)


4. File .magicrc helps for startup.
5. Use `magic -d XR` to invoke magic.
6. Open met3.mag file.
![day3_magic_2](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/9c6839bf-9214-42bf-bc58-4816d755f3e5)


7. In tckon, use `drc why`. Each item has its own name and has design rules in google skywater readme under the 'Design Rules' tab. Go to periphery rules for the metal 3.
8. Now using left and then right mouse button create box. GO to the layer window and click on the met3 layer. Then in tckon type `cif see VIA2` It will create the masking for the via.
![day3_magic_5](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/a4f04008-0637-43c0-8429-0c70c424fddb)


9. Now zoom into one via mask and create box as close as possible and type `snap int ` in tkcon.
![day3_magic_6](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/9ffb445d-80c6-4dd2-8ae1-ff60bc400cb9)


10. Next type `box` in tkcon to find the distance.
![day3_magic_7](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/4a7549fa-4377-4a1e-b158-f742e36ae44d)


11. Now load poly using `load poly` in tkcon.
![day3_magic_8](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/1bc03d2c-a450-4cc1-b546-f71957af8978)


12. Now update the poly.9 details in the sky130A.tech file as below and load it in Magic again. Type `drc check`.

![day3_magic_poly9](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/7c6859c8-88db-452f-ae79-54936271daa5)
![day3_magic_poly9_2](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/c9da2ce8-553c-49f3-add1-1cba2b944467)
![day3_magic_poly9_3](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/8d1e9363-18ba-4f1d-bc72-1e16cd0d00e4)
![day3_magic_poly9_last](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/97a33495-59ec-42ca-9e52-f0659dde69e8)
