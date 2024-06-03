# VSD SOC Design Workshop (2 Weeks)




# LAB SESSIONS:

## DAY 1: Get familier to open-source EDA tools

### 1. OpenLANE directory structure

1. Open terminal and go to open_lane_working_dir.
 ![Day1_1](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/808d653e-ff0c-4ab1-bde7-ce087d6e72b5)


  
2. Check the PDKs.
![Day1_2](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/46d6b2dc-6532-4720-9e58-6743b92c3359)



   a. Skywater PDK (for workshop) has OS and OpenLANE and all the PDKs: timing, tech lef and cell lef.
    ![Day1_3](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/4abd5695-736b-44a5-ab64-fe98f2751d8e)
    ![Day1_4](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/f42285c9-9348-4b74-91b0-e2b764881616)

      
   b. Open PDKs: mitigate commercial foundry with OS tools.
     
   c. sky130A (PDK variant) which is made compatible for OS.
![Day1_5](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/a974c7cb-2f36-4a79-879b-19eedf813950)
![Day1_6](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/705dbba8-1177-4195-89fb-3765113475cd)
![Day1_7](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/5fd63643-9fa0-4196-929c-bcdab123ae99)
![Day1_8](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/2adae527-da8b-4d0a-a399-c20f828f2168)
![Day1_9](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/eb15830b-4da5-458c-80fe-1ebea6796f96)





     
3. Invoke the OpenLANE in the openlane directory.
     ```
     docker
     ./flow.tcl -interactive
     package require openlane 0.9
     ```
     ![Day1_10](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/4e3a6674-fd27-4408-b294-a067055ced7a)


     
### 2. Design preparation 

1.  Multiple designs are in OpenLANE. Go inside the picorv32a.
![Day1_11](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/e466bf61-7cdf-4cc1-9bea-7a62567fbcc2)
![Day1_13](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/d19ab74f-0469-48ad-8284-b95171b2a2cc)


2. Check the config.tcl file which will be used for the initial picorv32a design for new runs as base file.
![Day1_14](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/6794d2d7-579d-40ca-b92a-5494e3c8776a)


3. Check the standard cell tcl.
![Day1_15](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/8e9f5b68-567a-4f48-b437-0288cb52727f)


4. Now design step is created using `prep -design picorv32a`. Merging the cell and tech lefs into one.
![Day1_12](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/4b2011a4-b00f-400f-9e83-73a758e2bf54)


### 3. Review files

1. Inside the picrov32a design directory **runs** is created where the tool auto creates directory with current date-time.
![Day1_16](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/fe088a08-45ec-4293-837e-6143041ca813)


2. **tmp** folder is where the temp files are created.

   a. merged.lef is created when using the prep of picorv32 design (merged.py - Has layers, wires, cell level lef info which uses rectangle to define size)
   ![Day1_17](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/d6daa995-da46-4927-9282-e520a8e43fff)


   b. Check the merged.lef using `less merged.lef`
  
  ![Day1_18](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/f8cf496a-82fe-4a58-be91-5aa0e9ecfd3b)
4. **results** folder has all the PnR level folders
![Day1_19](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/ca5b795b-f1da-4229-b847-17d658e87f47)


5. **reports** folder has all the timing analysis in config and reports will be generated here.
![Day1_20](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/9947ee7d-2533-4b0f-9ed0-a607fccd1ccc)


6. **config.tcl** in the run directory has default parameters used for the run. OpenLANE allows to make changes on the run and we can update the config to run it again.
![Day1_21](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/9f0388c8-a6ef-43e1-a962-5b44288a8b96)


7. **cmds.log** takes record of all the command used during the run.
![Day1_22](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/a1ad6830-57d7-4423-917c-38532690cc4d)


8. `run_synthesis` after the design preparation stage. Wait for some time to complete.
![Day1_23](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/b8322679-f7ab-4c32-9530-b54cd2e5afa8)
![Day1_24](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/9240e4c2-073d-4e95-ae3d-45585ddbc463)




### 4. OpenLANE project Git link

1. Setup of OpenLANE from Github using git clone and following the process in the [OpenLANE efabless repository](https://github.com/efabless/openlane2)
2. Refer to FOSSI dialup videos for installation.

### 5. Steps to characterize synthesis results

1. After `run_synthesis`, synthesis file gets created in the run directory. Check other synthesis files.
![Day1_25](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/ceeccece-f809-4e75-9a64-f453efba33e0)
![Day1_26](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/ddf17923-09ac-44d0-9e05-10e991ca28c4)

3. Check report for yosys_4.stat.rpt which is a statistical report. Use `less 1-yosys_4.stat.rpt`
![Day1_27](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/91852d11-3a3d-45f7-8ecb-36b322a8f2bf)



4. Check report for opensta_timing.stat.rpt which has the STA timing reprots. Use `less 2-opensta.min_max.rpt`
 ![Day1_28](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/ea9eda92-23a9-4a3d-bde0-f5b647222a9c)

 ![Day1_29](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/f06dc974-9609-4694-99c2-8f38a04c4284)


5. To calculate the flop ratio, open the 'yosys_4.stat.rpt'. Divide the value of sky130_fd_sc_hd__dfxtp_2 and Total number of cells.
     (sky130_fd_sc_hd__dfxtp_2) / (Total number of cells) = 1613/14876 = 0.1084 = 10.84%



## DAY 2: Good floorplan vs bad floorplan and introduction to library cells

### 1. Steps to run floorplan and placement in OpenLANE

1. Open README.md in configurations directory. Variables required for each stage (Ex: synthesis, floorplan ...), update variable as per flow and requirment are all kept here. Variables are also called switching.
![Day2_2](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/ecd880ac-6447-41e1-b4ae-120a58890bf2)
![Day2_3](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/777e8eb3-dcc6-4714-8f55-f1e532afc1e9)
![Day2_4](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/d27759db-c080-4788-bfd7-79b630d7ff5d)
![Day2_5](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/3e7303b4-b59a-4766-a307-6b3cdd2bde8b)
![Day2_6](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/fe26d7a9-6905-440b-893c-dfdcdd87b80e)

2. Now `run_floorplan`. After run is complete, similar to the synthesis process, go to the **floorplan** directory in the run and review the files.
![Day2_1](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/260a9d07-7cf9-4c86-875d-1e047641995d)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/0bd39537-cd4b-41af-9b84-b3f444e2697b)

3. To check the floorplan in Magic tool use `magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &'
![Day2_7_floorplan](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/69d67888-19f8-4b40-90ec-23ad5b8cf960)
![Day2_8_floorplann](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/7665481f-bd25-455c-b51d-dd68b7051a46)


4. Now `run_placement` after the floorplan is completed.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/df4776e9-c8e7-4399-b57d-f5866b8a7705)



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



## DAY 4: Pre-layout timing analysis and importance of good clock tree

1. Go to the tracks.info file to check where the routing will happen in the metal layer.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/dab60563-7fc9-418e-b80f-be779e7f0786)

2. Update the grid in the MAGIC tool using the tckon terminal as per the tracks.info data.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/2acfb577-fd87-4d33-9d4a-6b6954a853e1)

3. Now to update the width of the standard cell. Should be odd multiple of x pitch.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/41eef897-e280-498b-ab5c-18e2fbb6839b)

4. Ports can be defined by selecting the port and then Edit >> Text..
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/9a745d78-7f3f-47e6-be71-8aa83c8f8fe8)

5. Before extracting LEF, save the cell as `save sky130_vsdinv.mag`
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ca93edd8-53e4-4dc3-acc1-817f575cb470)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/f44b6453-a882-47e7-b431-971a438280f0)

6. Open the saved file and create the LEF using `lef write` in the tckon terminal.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/a2fcfda2-c56f-47d3-a593-2ca178a6b95c)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3c13c73a-164a-4f82-8e1c-a5e6f33454ee)

7. As the port A was enabled, it creates it as pin.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/50f10d6c-572d-41c4-b992-2ce64de7577d)

8. Now this lef file will be moved in the src folder for the picorv32a to use.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/778b2c18-9c91-4105-b8b3-7321edfa01b9)


### 1. OPENLANE

1. To use new cell in synthesis, will check the lib files. The libs are different as per process corners. 
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/9b1b7726-13f3-441a-af2b-8201a87117d8)

2. Copy the libs to the src location.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/4721df9e-6520-4ef4-ac4b-6ab553153d46)

3. Modify config.tcl as following.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/e9c2360e-3b25-4a7a-bfef-c1f4bfd4bb44)

4. Now using following commands start the OPENLANE tool.
```
docker
./flow.tcl -interactive
package require openlane 0.9
```
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6af3cf5b-48b7-427b-9f6e-d250d1405583)

5. Now using `prep -design picorv32a -tag 09-08_16-0 overwrite` the updated config will be used. Then provide the following commands.
```
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/f3dc80cb-8532-4ecf-85c9-c6b34e0cb7e1)

  > If error is show as below for the FASTEST and SLOWEST, update the LIB_MIN and LIB_MAX to LIB_FASTEST and LIB_SLOWEST simultaneously.
  > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/e10677f5-c484-4565-8376-3d22110c76d9)

6.  Run systhesis using `run_synthesis`
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/ea21fb90-e5ea-4d13-a718-b0746a444eb9)

7.  Make modification in the flow.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/7c6d5fcc-f7aa-46a5-8654-caff17f57745)

8. Run floorplan. Use `run_floorplan`
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/072845b4-b03b-4f0c-9df4-be0f1bca42c6)

  > If errors found for run_floorplan, follow the commands one by one:
  > ```
  > init_floorplan
  > place_io
  > global_placement_or
  > tap_decap_or
  > run_placement
  > run_cts
    > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/cd8580d4-a201-409d-a463-f0a0b788902a)
  > gen_pdn
    > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6f835a1f-16a1-4bc0-b512-ed2b2ab94a8d)
  > run_routing
    > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/10f2d841-610d-4a99-ac63-8e89dc710dd5)
    > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3fa662d3-d2f5-4438-98d3-e0b7c02c5f75)
  > ```     
  
9. Now go to the placement location of the run and then read the lef and def in MAGIC. Zoom into the cells and find the 'vsdinv' cell and `expand` after using 's' on the cell.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/bdcdd921-2e04-44fa-9273-700d3cde4fbe)


### 2. OpenSTA (Engine integrated with Openlane)

1. Create a new sdc 'mybase.sdc' using gvim and update the following in it.
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/102088cf-8d26-44fb-9645-ecabc42831bc)

2. Now create a pre_sta.conf file using gvim and update the following in it.
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/691bdfa3-4143-4c42-8842-8b453d9f4f74)

3. Invoke the OpenSTA using the pre_sta.conf file in the openlane directory. Command: `sta pre_sta.conf`
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/c7cd4814-6c4b-4024-a9d1-5cd9528ce520)
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6ff174f9-d581-4d8d-be36-6b3bc4b8294e)


4. Set `set ::env(SYNTH_FANOUT) 4` in the openlane tab for the above STA run to reduce the slack.
  We can check the connections of the net.
  ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/15239466-10bf-4c4b-b1c4-e22aaaf38994)

5. Replace cell as per requirement to increase the size with the command `replace_cell _13160_ sky130_fd_sc_hd__o2111a_4` . To check reports use `report_checks -fields {net cap slew input_pins} -digits 4`. Resize any cells as per requirement to reduce the slack in the reports.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3ec914f6-e505-4774-8fce-39002583882a)

6. If require to check the timing report through a net from startpoint to endpoint, use `report_checks -from _27860_ -to _27762_ -through _13165_` . This will help to check the report for the specific path.

7. Replace the synthesis path in the run directory with the updated timing run data using `write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/New_RUN_13_08/results/synthesis/picorv32a.synthesis.v`. This replaces the existing verilog with the updated timing verilog.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/e278a75c-612f-4b38-806d-d265e7f02f05)

8. Verify the replaced cell in the netlist for verification. Ex: use the cell instance _13160_ and check if the resize happened. It should increase from 2 to 4 size.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/89e32cd5-7533-4604-be26-3d153408d9ec)

9. Run the floorplan `run_floorplan` and placement `run_placement` without the synthesis now or it will update the netlist again. 


### 3. TritonCTS

1. Once placement is completed move on to CTS stage, check the README file in configuration directory for the variables. Run CTS `run_cts`.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/73260b0f-f4e2-43f4-9558-834abe596481)

2. In TCL, TCL proc - defination are made in flow and called during runs.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/d3a4d5fa-f197-445e-9c1c-30c38b1250b5)

![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/b07cad66-663e-45c2-b914-5022cb6ffab2)
  
  > As per flow, synthesis in not part of the openroad scripts whereas others all are present.
  > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6e08172d-6fcc-4c93-be6d-6edcccc91562)

3.  Inside the or_cts.tcl, we can check the variables using `echo`.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6c303434-8565-4193-bda3-da20845dc456)


4. Inside the same or_cts.tcl file, clock_tree_synthesis where the **TritonCTS** engine is used and the control is passed to it.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/747733ea-067f-4cd0-94d3-bae1e239cf59)

5. Check the clock buffers used.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/c02f28d0-a36e-43e5-a3a0-e263db1af7e6)

  > Current drawback for TritonCTS - it cannot create optimized CTS for multiple corners.
6. Compare the CTS_MAX_CAP from the tcl script and the typical lib.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/66668371-0075-4e2c-90f1-075c476aafd7)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/3794131a-cb67-4eaf-a0e5-fddec107ec40)


### 4. OPENROAD

1. Invoke the openroad `openroad`. As we are inside the openlane, we can use the variables.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/328d9199-696a-44f7-9b8b-e681f111a863)

2. Timing analysis is done after creating db using the lef and def files and only once is required to be created. Post cts def to be used.
```
read_lef /openLANE_flow/designs/picorv32a/runs/New_RUN_13_08/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/New_RUN_13_08/results/cts/picorv32a.cts.def
```
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/1f7e79be-0436-4c23-9958-6f4af6405a1e)

    > NOTE: as we have invoked the openroad in its directory, no need to provide the full path or else will face error.
    
3. Create the db file.
```
write_db pico_cts.db
read_db pico_cts.db
```
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6c05ff3b-3612-4988-af94-841801b84a9a)

4. Follow the same statements as in the .conf file.
```
read_verilog /openLANE_flow/designs/picorv32a/runs/New_RUN_13_08/results//synthesis/picorv32a.synthesis_cts.v
read_liberty -max $::env(LIB_SLOWEST)
read_liberty -min $::env(LIB_FASTEST)
read_sdc /openLANE_flow/designs/picorv32a/src/mybase.sdc
```
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/cb4cc9da-2939-4399-9752-14bd86a3cfa1)

5. As clocks have been built, the propagated clocks will calculate the actual cell delay in the clock path and check the reports.
```
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -format full_clock_expanded -digits 4
```
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/549d68d6-562a-467e-8c5f-51446e948cb8)

6. As per the above commands, we are using 'min_max' by using the 'typical' lib only. So exit and load openroad again.

7. Now to do analysis for the 'typical' library.
```
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/New_RUN_13_08/results//synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/mybase.sdc
set_propagated_clock [all_clocks]
```

8. Now check the report again. Use `report_checks -path_delay min_max -fields {slew trans net cap input_pin} -format full_clock_expanded -digits 4`
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/4ec6f47d-add1-4da7-9e93-df5cee290db9)

   > **Example: Updating the clock buffer list to remove the 'clkbuf_1' and add it again.**
   > In TCL, lreplace does not overwrite the list. So need to write into the list `set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]`. Run cts after this `run_cts` to check the modifications.
   > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/95f0167b-7a8b-4022-b9fb-620fb6ed0f24)
   >
   > TritonCTS will hang, check the process using `top`. Kill process `kill -9 <PID>` for openroad.
   > ![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/6bae4397-3740-467d-a61a-a44973e8207c)
   > 
   > Check the CURRENT_DEF variable which is set to the post cts def. Use `echo $::env(CURRENT_DEF)`
   > 
   > Use the def after placement `set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/New_RUN_13_08/results/placement/picorv32a.placement.def`
   > 
   > Check `echo $::env(CTS_CLK_BUFFER_LIST)` and run_cts. Then follow the commands in Step 7. Check the slack using `report_clock_skew -hold` and `report_clock_skew -setup`.
   > 
   > To add the clock buffer again into the list, `set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]`


## DAY 5: Final steps for RTL2GDS using tritonRoute and openSTA

### 1. Power Distribution Network (PDN)

1. Invoke openlane and check the CURRENT_DEF `echo $::env(CURRENT_DEF)` which shows the previous run's def used.
2. Use `gen_pdn` for creation of power network.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/30ac2957-6295-48a5-af3c-aaaa7d119bbb)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/4ea7bf46-abdb-441d-8960-9ff9c883564f)

3. This will now update the CURRENT_DEF which includes the cts and power defs. Check def `echo $::env(CURRENT_DEF)`.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/8683b014-bc84-4791-bcc4-d4df3de572b0)


### 2. TritonRoute

1. Check the Readme.md file in the config for the Routing variables. Since the tool is updated, the 'ROUTING_STRATEGY' is now divided among other variables like 'ROUTING_OPT_ITERS' , 'GLB_RT_MAX_DIODE_INS_ITERS' and other variables for routing process. No need to update variable. Check the existing values.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/c5a3c5ef-fc19-435b-aaf3-3215f097de19)

2. Now start `run_routing`. Using the default variable values, the TritonRoute will move to have 'zero' DRC violations. Therfore no DRC file will be created.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/86f77cd8-b058-4cf8-81ad-82a0d0c22922)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/8e6c6e0d-ddc0-47f3-81bb-fd590745b83e)

3. Routing guides for Global 'fastroute' and Detailed 'tritonRoute' routing can be found in the 'tmp' directory of the respective run.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/8b21a3e3-eb6e-41d5-8560-7e838cb6a3a8)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/326a27b9-6ed4-485c-b3f1-04d23b07feb6)

4. Openlane now supports SPEF creation in its routing flow. So check the .spef file in the '<run_dir>/routing' after the routing is comlpleted. The variable 'GLB_RT_MAX_DIODE_INS_ITERS' in the routing configuration makes sure to create the .spef file using the lef and the routing def.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/072dc1a8-f68b-4656-af18-3f16c385ab1a)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/97c00fa9-2a7b-4e2e-bfc0-382e1d6c4768)

6. A pre-route netlist is created as '_preroute.v' in the synthesis directory before the routing.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/54cb56d5-3e5b-41ec-8782-19cd6d514d24)

7.  In post STA analysis, will use the following:
```
read_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/New_RUN_13_08/results/synthesis/picorv32a.synthesis_preroute.v
read_sdc  /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/mybase.sdc
read_spef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/New_RUN_13_08/results/routing/picorv32a.spef
```
