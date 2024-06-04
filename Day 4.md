## DAY 4: Pre-layout timing analysis and importance of good clock tree

1. Go to the tracks.info file to check where the routing will happen in the metal layer.
![day4_1](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/f4c5a11d-21ab-4001-bc0d-7bf41afd6818)


2. Update the grid in the MAGIC tool using the tckon terminal as per the tracks.info data.
![Day4_2](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/c6dc452f-389d-4b77-a4ab-249eedf5fb28)

3. Before extracting LEF, save the cell as `save sky130_vsdinv.mag`
![day4_3](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/4590a301-78a9-4096-9b49-3ad8368b67fe)

4. Open the saved file and create the LEF using `lef write` in the tckon terminal.
![day4_4_lef](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/41d3f23b-e916-4480-9fb5-fee6226ff446)
![day4_5_ff](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/5e8920a4-553b-44b3-8a1e-ebe9a4c23797)

5. As the port A was enabled, it creates it as pin.
![day4_6_lef_file](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/09bea3c4-9dc8-451a-a0b7-01033f587b9f)


6. Now this lef file will be moved in the src folder for the picorv32a to use.
![day4_7_copy](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/362b738c-00eb-4522-9d60-affb614bb98c)


### 1. OPENLANE

1. To use new cell in synthesis, will check the lib files. The libs are different as per process corners. 
![day4_8](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/343f2d1c-18c1-4c57-b9d9-2039037140f7)


2. Copy the libs to the src location.
![day4_9](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/8afe9449-3657-42ae-9525-0ed547f3801d)


3. Modify config.tcl as following.
![day4_10_1](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/e93691db-ade5-4871-83f5-6c163af5f58e)


4. Now using following commands start the OPENLANE tool.
```
docker
./flow.tcl -interactive
package require openlane 0.9
```
![day4_11](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/84e1c260-cefb-410d-9061-668021ea96b3)


5. Now using `prep -design picorv32a -tag 09-08_16-0 overwrite` the updated config will be used. Then provide the following commands.
```
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```
![day4_13](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/1d94e70e-28d9-4d27-947f-2b08984c0814)


  > If error is show as below for the FASTEST and SLOWEST, update the LIB_MIN and LIB_MAX to LIB_FASTEST and LIB_SLOWEST simultaneously.
  
6.  Run systhesis using `run_synthesis`
![day4_14_synth](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/31ff620b-a930-4daf-b860-a5220915d0f2)

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


