# Level-2(Day-2): Timing libraries,hierarchial vs flat synthesis, efficient flip-flop coding styles

## List of Objectives

- :dart: <b>Practiccal Objective-1:</b> [Lab for introduction to timing.lib]()
   - :microscope: <b>Lab-1:</b> [Clone SKY130 open source process design kit(PDK) on Ubuntu VM as test file library]()
   - :microscope: <b>Lab-2:</b> [ Simulate a RTL design using iverilog]()
   - :microscope: <b>Lab-3:</b> [ Read and edit (editing process only) verilog file using text editor]()
- :dart: <b>Practical Objective-3:</b> [Labs on Hierarchial and Flat synthesis)
    - :microscope: <b>Lab-4:</b> [Synthesize a design using Yosys and SKY130 PDK (Test design: 2:1 MUX (Verilog file named as "good_mux.v"))]()     
- :book: <b>Learning Objective-1:</b> [Various flip-flop coding practices]()
- :dart: <b>Practical Objective-3:</b> [Labs on flip-flop design,simulation,synthesis and optimization]()
    - :microscope: <b>Lab-5:</b> [Synthesize a design using Yosys and SKY130 PDK (Test design: 2:1 MUX (Verilog file named as "good_mux.v"))]()

 <div align="center">:star::star::star::star::star::star:</div> 
 
## :dart: Lab for introduction to timing.lib
 ### :microscope: Lab-1: Open the library file , significance of the filename.
   
   :zap: Open the `.lib` file using text editor-
     
   ```
   $ gvim sky130_fd_sc_hd__tt_025C_1v80.lib
   ```
   ![lib_vim_1](images/lib_vim_1.png)
   
   :zap: Go to the command line mode in gvim text editor by pressing `:` -

   - Syntax off-
   ```
    :syn off
   ```
   - Line numbers-
   ```
    :se nu
   ```
   ![lib_vim_2](images/lib_vim_2.png)
   
   :zap: Significance of the filename-

   - Based on process, voltage and temperature variation cell performance changes.
   - The performance of cells in `.lib` file are generalized in certain values of these three parameters.
   - We can observe the parameters in the name of `.lib` file.
   -  For the `sky130_fd_sc_hd__tt_025C_1v80.lib` file-
      - Process: `tt` (Typical pocess).
      - Voltage: `1v80` (1.80 V).
      - Temparature: `025C` (25 degree celcius).
   
  ### :microscope: Lab-2: Observe Cell definition, parameters
  :zap: Cell names can be seen using the following command-
   ```
   /cell+ space key
   :g//
   ```
   ![lib_cell](images/lib_cell.png)

  :zap: Now we can check any cell's line number and go to that cell definition-
  ```
  :
  ```
  ![lib_cell_1](images/lib_cell_1.png)
  
  :zap: Analyze the cell parameters-
  
   - There are different leakage power for different input combinations.
   - Area,power,capacitance are also present in the definition.
     
  ### :microscope: Lab-3: Compare area,power of variants of same cell
  :zap: We have opened three different flavours of same cell using line number-
  ```
  :36663
  :vsp
  :vsp
  :36904
  :37145
  ```
  ![cell_comp](images/cell_comp.png)
  
   :zap: Compare three cells-

   - `and2_0`,`and2_1`,`and2_2` cells are opened.
   - Area is increasing from `and2_0` to`and2_2`.
   - Speed is increasing from `and2_0` to `and2_2`.
   - Power is increasing from `and2_0` to `and2_2`.
     
  <div align="center">:star::star::star::star::star::star:</div> 
 
## :dart: Lab on Hierarchial vs Flatten synthesis
 ### :microscope: Lab-1: Hierarchial synthesis
   
  :zap: Synthesize `multiple_modules.v` as hierarchial-
     
   ```
  $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ read_verilog multiple_modules.v
  $ synth -top multiple_modules
  ```
  ![hier_synth_1](images/hier_synth_1.png)
  
  ```
  $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ show
  ```
  ![hier_synth_2](images/hier_synth_2.png)

  ```
  $ write_verilog multiple_modules_net.v 
  ```

   ![hier_net_v](images/hier_net_v.png)
   
   ### :microscope: Lab-2: Flat synthesis
   
  :zap: Synthesize `multiple_modules.v` as flatten-
     
   ```
  $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ read_verilog multiple_modules.v
  $ synth -top multiple_modules
  $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ flatten
  $ show
  ```
  ![flat_synth_1](images/flat_synth_1.png)

  ```
  $ write_verilog multiple_modules_flat.v 
  ```

   ![flat_net_v](images/flat_net_v.png)
   
 
  ### :microscope: Lab-3: Compare hierarchical and flat synthesis
  :zap: Hierarchial vs Flat netlist
   ```
   $ gvim multiple_modules_hier.v
   :vsp
   :sp multiple_modules_flat.v
   :exit
   ```
   ![comp_hier_flat](images/comp_hier_flat.png)

  :bulb: Significance of flat synthesis-

  - If a submodule is instantiated multiple times the multiple time synthesis of same submodule is problematic.
  - We can synthesize submodule one time and use this multiple time.
  - This is the significance of `synth -top`-
    
    ```
    synth -top `submodule_name`
    ```
 ### :microscope: Lab-3: Compare area,power of variants of same cell
  :zap: We have opened three different flavours of same cell using line number-
  ```
  :36663
  :vsp
  :vsp
  :36904
  :37145
  ```
  ![cell_comp](images/cell_comp.png)
  
   :zap: Compare three cells-

   - `and2_0`,`and2_1`,`and2_2` cells are opened.
   - Area is increasing from `and2_0` to`and2_2`.
   - Speed is increasing from `and2_0` to `and2_2`.
   - Power is increasing from `and2_0` to `and2_2`.
  

 <div align="center">:star::star::star::star::star::star:</div>   
 
## :book: Introduction to Yosys and Logic synthesis

### :bulb: Synthesizer
   - RTL design to gate level design.
   - RTL design is the behavoural representation of the required specification.
   - Gate level design means representation of the required specification as the connection of logic gates.
   - `Netlist` is the file which includes the required locgic gates and connections between gates after synthesizing.
   - The tool used for synthesizing the RTL design is known as synthesizer.
   - `Yosys` is an example of open source synthesizer.
  
---
### :bulb: Yosys based synthesis flow
   - Start yosys
   - `.lib file` is given to yosys.
   - `.v design file` is given to yosys
   - Top module is synthesized as interconnection of logical block.
   - Logical blocks/gates are translated to standard cells from process design kit (PDK) libray.
   - Netlist is generated.
   - The netlist is also simulated using iverilog with the `RTL design testbench` to prevent `synthesis-simulation mismatch`.

   ![yosys_flow](images/yosys_flow.png)
    
---
### :bulb: `.lib` file
   - `.lib` file is the collection of logical modules (blocks or gates).
   - Logic gates like `and, or, not` and blocks like `mux, or_and_invert,D flip-flop` etc.
   - There are different flavors of same gate `slow`, `medium`, `fast`.
   - Here we are using `sky130_fd_sc_hd__tt_025C_1v80.lib` open source library.
---
### :bulb: Reason for different flavours of gate

   ![fast_cell](images/fast_slow_cell.png)

- #### Why fast cell ?
  - Combinational delay in logic path determines the maximum speed of digital logic circuit.
    
   ![fast_cell_1](images/fast_cell_1.png)
  - We need faster cells to make T<sub>comb</sub> small and thus increase mcircuit speed.
  - We can understand `setup time` with the train boarding analogy that we have to go to the station some time before the departure of the train.
  - Setup time is the time duration before clock edge from which the data should be stable in D flip-flop data input port.
  - Used for preventing Setup time violation and critical path issues.
- #### Why slow cell ?
  
  - Reliable data flow (launch and capture) between flip-flops.
    
   ![slow_cell](images/slow_cell_1.png)
  - We need faster cells to make T<sub>comb</sub> small and thus increase mcircuit speed.
  - Suppose DFF-A launch data in a clk-edge and DFF-B receive that data in next clk-edge.
  - DFF-B should not receive the new data of DFF-A in clk-edge-1.DFF-B should receive clk-edge-0 data of DFF-A in clk-edge-1.
  - DFF-A propagation delay (T<sub>CQ_A</sub>) and T<sub>comb</sub> are used to slow the DFF-A new data to reach the DFF-B in same clock edge.
  - Hold time is the time duration after clock edge till which the data should be stable in D flip-flop data input port.
  - Used for preventing hold time violation.
    
  ![slow_cell_2](images/slow_cell_2.png)
---    
### :bulb: Problems with fast cell and slow cell
  - Capacitence is the load in digital circuit
  - Faster charging or discharging of capacitance  means smaller the cell delay.
  - For faster charging/discharging, we need transistors capable of sourcing more current (wide transistors).
  - For the slower cells narrow transistors so power and are less.
  - #### Fast cell problem
    - Wide transistors
    - More area, more power
    - Hold time violation
  - #### Slow cell problem
    - Sluggish circuit
    - More delay
    - Setup time violation
### :bulb: Selection of cells
  - Guidance by the user in terms of `constraints` for selecting cells as per requirement.
 
<div align="center">:star::star::star::star::star::star:</div> 
 
## :dart: Lab using Yosys and SKY130 PDK 
 ### :microscope: Lab-4: Synthesize a design using Yosys and SKY130 PDK (Test design: 2:1 MUX (Verilog file named as "good_mux.v"))
   
   :zap: Go to verilog_files directory-
   ```
   $ cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
   ```
   :zap: Start yosys-
   ```
   $ yosys
   ```
   ![yosys](images/yosys.png)

   :zap: Give the `.lib` file to yosys for checking the availavle cells-
   ```
   $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```
   ![read_lib](images/read_lib.png)
   
   :zap: Give the `.v` file `good_mux.v` to yosys for reading the design-
   ```
   $ read_verilog good_mux.v
   ```
   ![read_ver](images/read_ver.png)
   
   :zap: Specify the module `good_mux` which to be synthesized as root design-
   ```
   $ synth -top good_mux
   ```
   ![synth](images/synth.png)
   
   :zap: Generate the netlist for the design using the standard cell library-
   ```
   $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```
   ![abc](images/abc.png)

   :zap: Visualize the synthesized design-
   ```
   $ show
   ```
   ![show](images/show.png)

   :zap: Write the netlist as `.v` file `good_mux_net.v` with or without attribute (use only one)-
   ```
   $ write_verilog good_mux_net.v
   $ write_verilog -noattr good_mux_net.v
   ```
   ![write_ver](images/write_ver.png)
   
   :zap: Read the netlist-
   ```
   $ !gvim good_mux_net.v
   ```
   ![net_vim](images/net_vim.png)

   <div align="center">:star::star::star::star::star::star:</div> 
   
## :trophy: Level Status: 

- All objectives completed.
- I have learned simulation using iverilog,GTKWave (for timing diagram viewing) and synthesis using Yosys and SKY130 PDK.
- 🔓 Next level unlocked 🔜 [Level-2(Day-2): Timing libraries,hierarchial vs flat synthesis, efficient flip-flop coding styles](../Level_3/readme.md).


