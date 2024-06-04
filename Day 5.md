## DAY 5: Final steps for RTL2GDS using tritonRoute and openSTA

### 1. Power Distribution Network (PDN)

1. Invoke openlane and check the CURRENT_DEF `echo $::env(CURRENT_DEF)` which shows the previous run's def used.
2. Use `gen_pdn` for creation of power network.
![day5_1](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/a59faa69-3e79-452b-be33-3a02014f3ee7)
![day5_2](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/3d7f27d7-4985-42bf-9162-7bf4877fe61d)


3. This will now update the CURRENT_DEF which includes the cts and power defs. Check def `echo $::env(CURRENT_DEF)`.
![day5_3](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/d8a1ed9e-e458-48d0-9246-0cb6f7c4a5cf)

### 2. Routing

1. Now start `run_routing`. 
![day5_4](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/42a407b7-215b-4b34-9327-49152f610774)


2. Routing guides for Global 'fastroute' and Detailed 'tritonRoute' routing can be found in the 'tmp' directory of the respective run.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/8b21a3e3-eb6e-41d5-8560-7e838cb6a3a8)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/326a27b9-6ed4-485c-b3f1-04d23b07feb6)

3. Openlane now supports SPEF creation in its routing flow. So check the .spef file in the '<run_dir>/routing' after the routing is comlpleted. The variable 'GLB_RT_MAX_DIODE_INS_ITERS' in the routing configuration makes sure to create the .spef file using the lef and the routing def.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/072dc1a8-f68b-4656-af18-3f16c385ab1a)
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/97c00fa9-2a7b-4e2e-bfc0-382e1d6c4768)

4. A pre-route netlist is created as '_preroute.v' in the synthesis directory before the routing.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/54cb56d5-3e5b-41ec-8782-19cd6d514d24)

5.  In post STA analysis, will use the following:
```
read_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/New_RUN_13_08/results/synthesis/picorv32a.synthesis_preroute.v
read_sdc  /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/mybase.sdc
read_spef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/New_RUN_13_08/results/routing/picorv32a.spef
