
## DAY 3: Design library cell using Magic Layout and ngspice characterization

### 1. IO placer

1. As openlane is an iterative tool, variables can be updated to change as per requirement. Example, changing the IO spacing.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/424b27ba-60f3-4c18-abce-26ecc033e02a)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/78ac31df-e77e-4a39-97a8-8beaff6ea292)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/65d2872a-6709-47fa-b973-42a1019a26a0)


### 2. GIT CLONE of "vsdstdcelldesign"

  1. First go to the directory of vsdstdcelldesign on github.
  2. Clone the github repo "https://github.com/nickson-jose/vsdstdcelldesign.git".

  Command: `git clone https://github.com/nickson-jose/vsdstdcelldesign.git`
  
 ![Day3_git_clone](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/6d2a705e-7cd7-460c-a5c6-36ed2d14b358)


  4. After the cloning is completed, copy the tech file.
  
  Command: `cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/`
  ![Day3_copy_tech](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/f51dcc6e-5543-4c43-8987-4c57b41345f5)
  ![day3_copy_list](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/899dfdfa-692a-484b-9854-2c5eb187aa74)




### 3. MAGIC TOOL (VSDSTDCELLDESIGN)

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
        > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/643d6892-ac72-451f-ba65-7930ef5180fc)
        > If file not updated as above, then the below error could be shown for sub ckt
        > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/20fbaa5f-38a9-4b76-804a-379125349f67)
> For more information and working of MAGIC, go to "http://opencircuitdesign.com/magic/index.html"


### 4. NGSPICE

  1. After the file is saved, invoke the .spice file in ngspice `ngspice sky130_inv.spice`. If ngspice not available, use `sudo apt install ngspice`.
     ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ae7b999a-aa26-422c-bf94-22ab8a098e9d)
  2. Plot the graph using `plot y vs time a`.
  3. Calculate the cell rise and fall delays for PVT characteristics.
     ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/10187b06-394c-4361-a434-f01b2929d053)


### 5. MAGIC TOOL (DRC)

1. For tutorial and more details go to the [opencircuitdesign](http://opencircuitdesign.com/magic/index.html) website.
2. For skywater pdks check [skywaterpdks](https://github.com/google/skywater-pdk)
3. Get the Magic drc open pdk using for lab.
   ```
   wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
   tar -xfz
   cd drc_tests
   ls -lrth
   ```
   ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/b5c83484-ecf7-431d-bd97-40a963aa40ce)

4. File .magicrc helps for startup.
5. Use `magic -d XR` to invoke magic.
6. Open met3.mag file.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/39d67add-ff75-4e27-8395-f0e65eaa8ec5)

7. In tckon, use `drc why`. Each item has its own name and has design rules in google skywater readme under the 'Design Rules' tab. Go to periphery rules for the metal 3.
8. Now using left and then right mouse button create box. GO to the layer window and click on the met3 layer. Then in tckon type `cif see VIA2` It will create the masking for the via.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/a3fc8f9f-c3fd-4b02-99cd-a75105018d20)

9. Now zoom into one via mask and create box as close as possible and type `snap int ` in tkcon.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6113d36a-6fe7-49cc-b386-e284884407cc)

10. Next type `box` in tkcon to find the distance.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/72f1a2e1-8e2f-4b5c-94a7-563bb08b99f5)

11. Now load poly using `load poly` in tkcon.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/5e2bbb9e-de39-4e43-9c6e-bc7e7c397a2d)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/046090e8-fc06-4a35-82ff-7fdeb27ae893)

12. Now update the poly.9 details in the sky130A.tech file as below and load it in Magic again. Type `drc check`.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/c6566801-2a8a-4f77-95eb-b10ae75852f3)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/2bc25a0f-242c-4e86-b878-9060d6fea94c)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/e9e12aa5-99e9-4fa2-9f6d-07a12335f27e)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/7ab973a2-24ef-43be-9e10-7e15aaf0dfbb)
