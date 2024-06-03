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
