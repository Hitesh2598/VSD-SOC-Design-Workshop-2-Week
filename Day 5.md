## DAY 5: Final steps for RTL2GDS using tritonRoute and openSTA

### 1. Power Distribution Network (PDN)

1. Invoke openlane and check the CURRENT_DEF `echo $::env(CURRENT_DEF)` which shows the previous run's def used.
2. Use `gen_pdn` for creation of power network.
![day5_1](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/a59faa69-3e79-452b-be33-3a02014f3ee7)
![day5_2](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/3d7f27d7-4985-42bf-9162-7bf4877fe61d)


3. This will now update the CURRENT_DEF which includes the cts and power defs. Check def `echo $::env(CURRENT_DEF)`.
![day5_3](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/d8a1ed9e-e458-48d0-9246-0cb6f7c4a5cf)

### 2. Routing

 Now start `run_routing`. 
![day5_4](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/42a407b7-215b-4b34-9327-49152f610774)

![day5_5](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/bf9dba6d-b0dd-4288-b64f-d11d2fcf26b6)

![day5_6](https://github.com/Hitesh2598/VSD-SOC-Design-Workshop-2-Week-/assets/108817818/cc81f4bf-5aeb-4cab-9f2b-5c57a5ca5038)

