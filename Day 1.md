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
      
Chip module area: 147712.918400

Flop ratio = no of DFFs (D flip-flop)/Total no of cells. 

Total no of cells = 14876 

No of DFFs (count of sky130_fd_sc_hd__dfxtp_2) = 1613

(sky130_fd_sc_hd__dfxtp_2) / (Total number of cells) = 1613/14876 = 0.1084 = 10.84%


