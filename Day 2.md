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


3. To check the floorplan in Magic tool use `magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &'
![Day2_7_floorplan](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/69d67888-19f8-4b40-90ec-23ad5b8cf960)
![Day2_8_floorplann](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/7665481f-bd25-455c-b51d-dd68b7051a46)


4. Now `run_placement` after the floorplan is completed.
![image](https://github.com/prachurjyaghy/Physical-Design-using-OpenLANE-SKY130/assets/48976708/df4776e9-c8e7-4399-b57d-f5866b8a7705)

5. To check placement in Magic tool use  ` magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130/libs.tech/magic/sky130.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def & `

![Day2_10_placement](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/29e4a4b3-87e7-4bc8-8475-2ad0f982a8e5)
