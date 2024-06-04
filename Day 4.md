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
![day4_18_set](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/4b32e463-81c9-4b13-9e7a-e5456917fa93)


8. Run floorplan. Use `run_floorplan`


  > If errors found for run_floorplan, follow the commands one by one:
  > ```
  > init_floorplan
  > place_io
  > global_placement_or
  > tap_decap_or
  > run_placement
 
9. Now go to the placement location of the run and then read the lef and def in MAGIC. Zoom into the cells and find the 'vsdinv' cell and `expand` after using 's' on the cell.
![day4_16_placement_1](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/fc6687fe-5995-4795-9259-d2e51e1d68e1)
![day4_17_placement_layout](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/785981ef-e2b1-4357-b922-45188074c7b8)




### 2. TritonCTS

1. Once placement is completed move on to CTS stage, check the README file in configuration directory for the variables. Run CTS `run_cts`.
![day4_cts](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/ad4b3218-3fc1-44e6-a266-861ef1448c7f)

![day_ctsss](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/fd192b83-3003-425e-bb09-9e3c3248d69f)



### 3. OPENROAD

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


