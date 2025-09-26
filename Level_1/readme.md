# Level-1(Day-1): Introduction to Verilog RTL design and Synthesis

## List of Objectives

- :book: <b>Learning Objective-1:</b> [Introduction to iverilog simulaor](#book-Introduction-to-iverilog-simulator)
- :dart: <b>Practiccal Objective-1:</b> [Lab using iverilog and gtkwave](#dart-Lab-using-iverilog-and-gtkwave)
   - :microscope: <b>Lab-1:</b>
   - :microscope: <b>Lab-2:</b>
- :book: <b>Learning Objective-2:</b> [Introduction to Yosys and Logic synthesis](#book-Introduction-to-Yosys-and-Logic-synthesis)
- :dart: <b>Practical Objective-2:</b> [Labs using Yosys and SKY130 PDK](#dart-Labs-using-Yosys-and-SKY130-PDK)
    - :microscope: <b>Lab-3:</b>

 <div align="center">:star::star::star::star::star::star:</div> 
 
## :book: Introduction to iverilog simulator

### :bulb: Simulator
   - RTL design is checked for matching with the specification by simulating the design.
   - The tool used for `simulating the design` is known as `simulator`.
   - `Icarus Verilog (iverilog)` is an example of simulator.
 
---
### :bulb: Design
   - Design is the actual verilog code or set of verilog codes which has the intended functionality to meet with the required specification.
   - Written in hardware description language (HDL) like Verilog.
   - Functional verification is used to validate the RTL design.
---
### :bulb: Testbench
   - Testbench is the setup to apply stimulus `(test_vectors)` to the design to check its functionality.
   - It is the integration the `Design`, `Stimulus generator`, `Stimulus observer`.
   - `Stimulus generator` give `primary inputs` to the design under test (DUT).
   - `Stimulus observer` take `primary outputs` from the design under test (DUT).
   - Testbench has no primary inputs or outputs.
---
### :bulb: How Simulator Works
   - Simulator looks for the changes in input values.
   - Output is evaluated based on the change of input `(if no change in input, no change in output)`.
     
     ![testbench_img](Level_1/images/tb_rv.png)  
---
### :bulb: Iverilog Based simulation flow
   1. Design and testbench files are given to iverilog simulatior.
   2. iverilog simulator generate .vcd file.
   3. .vcd file is given to gtkwave.
   4. gtkwave helps to visualize the input-output waveform (timing diagram).
      
   ![iverilog_flow](Level_1/images/iv_sim_flow.png)

  <div align="center">:star::star::star::star::star::star:</div> 

### :dart: Lab using iverilog and gtkwave 
 #### :microscope: Lab-1: Clone SKY130 open source process design kit(PDK) on Ubuntu VM as test file library
   
   Open the Ubuntu terminal and clone the SKY130 PDK repository using the following command
     
   ```
   $ git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
     
   ```

    
      

