
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
  
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/2591669a-ab7b-47b0-a9a7-c12d938a9062)

  4. After the cloning is completed, copy the tech file.
  
  Command: `cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/`
  
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ef076efc-74cc-4bd1-8958-7110816d13e3)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/dbdad075-807a-4f08-bf76-a835f774d9f4)


### 3. MAGIC TOOL (VSDSTDCELLDESIGN)

  1. Open MAGIC tool to see the standard cell design in the cloned directory location. Also the tkcon terminal for MAGIC will open.

  Command:
  `magic -T sky130A.tech sky130_inv.mag &`
  
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/14614ce0-1c41-4506-a074-8c4ae7902230)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3b1c391e-f467-48de-a439-3fa26ebebf46)

  2. In the tool, use 's' and 'v' simultaneously to center the cell design.
  3. To select any part of the design, hover the mouse pointer to it and click 's' to select it.
  4. On the right hand side, all the layers are described.
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/9b617de5-b883-476a-9aaf-c2b659d6da9f)

  5. Using 's' 3x will select the whole connection layer where the mouse is pointed in the design.
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/d1dc4152-199f-4271-94f6-53497b3decf2)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/76368cf5-b155-4800-a2dc-d76c42eee9ce)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/8e131995-dd88-4026-a160-0f2e152e9b90)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3fb5087b-a2c0-4659-8a1e-38e2796e193a)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/09b547c1-251a-4a6f-bb40-fab04d1a41c5)

  6. Now in the tkcon terminal, after selecting any part of the design using 's', type `what`. PMOS and NMOS has been decribed the terminal.
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/c96cc201-e20d-4723-90a5-ef728a66ec31)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/079e8873-9579-443f-919d-664035806852)

  7. Go through the vlsistdcelldesign for more details on the cell design of the cloned github.
  8. MAGIC tool is also a DRC check tool and the design always has to be DRC clean. It can highlight the same and errors will be shown in the terminal.
  9. To know the logic, it has to be extracted to SPICE in ngspice:

     a. In the vlsistdcelldesign directory, use `extract all`.
      ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ea0a5ebd-ca49-47c7-9264-e939f0ac2b80)
     
     b. Extracted file is created with .ext.
      ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/206acbb3-32eb-456d-961a-90fdd484b4d6)
     
     c. To use in the **ngspice** tool: `ext2spice cthresh 0 rthresh 0`. Does parasitic extraction as well.

     d. To create .spice file : ext2spice
      ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/51f06562-4ca8-486e-bfad-c01c49664d65)
      ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/e1251cd7-141a-4f70-83ca-da223dad0062)
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
