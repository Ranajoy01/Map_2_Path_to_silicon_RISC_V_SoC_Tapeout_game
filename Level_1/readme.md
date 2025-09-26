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

## :dart: Lab using iverilog and gtkwave 
 ### :microscope: Lab-1: Clone SKY130 open source process design kit(PDK) on Ubuntu VM as test file library
   
   :zap: Open the Ubuntu terminal and clone the SKY130 PDK repository using the following command-
     
   ```
   $ git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
     
   ```
   :zap: Go to the Workshop directory cloned recently-
   ```
   $ cd sky130RTLDesignAndSynthesisWorkshop
   ```
   :zap: Here all test verilog files and standard cell libraries are available-
   - Check test verilog files-
   ```
   $ cd verilog_files
   $ ls
   ```
   ![test_verilog_files](Level_1/images/ts_ver.png)
   
   - Check Standard cell library-
   ```
   $ cd lib
   $ ls
   ```
   ![standard_cell](Level_1/images/std_cell.png)
   
  ### :microscope: Lab-2: Simulate a RTL design using iverilog (Test design: 2:1 MUX (Verilog file named as "good_mux.v"))
  :zap: Go to verilog_files directory-
  ```
  $ cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
  ```
  :zap: Give the design file "good_mux.v" and testbench file"tb_good_mux.v" to iverilog for compiling-
  ```
  $ iverilog good_mux.v tb_good_mux.v
  ```
  ![iverilog_log](Level_1/images/iverilog_log.png)
  
  :zap: An executable file a.out is generated.Now execute this file-
  ```
  $ ./a.out
  ```
  ![a_out_log](Level_1/images/a_out_log.png)
  
  :zap: A `.vcd file` is produced named as "tb_good_mux.vcd".Give this file to GTKWave-
  ```
  $ gtkwave tb_good_mux.vcd
  ```
  ![gtkwave_op](Level_1/images/gtkwave_op.png)
    
  ### :microscope: Lab-3: Read and edit verilog file using text editor (Observe the verilog code syntax for Test design: 2:1 MUX (Verilog file named as "good_mux.v"))
  :zap: Open verilog files on gvim text editor ('-o' is used to open multiple files in same window)-
  ```
  $ gvim good_mux.v tb_good_mux.v -o  
  ```
  ![verilog_file_text](Level_1/images/text_vim.png)
  
   :zap: Analysis of the design `good_mux.v`-

   - It has `i0,i1,sel` three primary inputs.
   - It has `y` as the primary output.
   - Ports are declared after module keyword.
   - `MUX functionality` is coded in the body (Inside module and endmodule).
  
  :zap: Analysis of the testbench `tb_good_mux.v`-

   - It has no primary inputs or primary outputs.
   - Design 'good_mux' is instantiated in this testbench.
   - Stimulus to the design are generated.
   - Primary outputs from design under test `(DUT)` or unit under test `(UUT)` are dumped into `.vcd file` as per the variation of primary inputs to UUT.
  
  :zap: Edit file in gvim text editor-

   - Press `i` to enter into the `insert` mode
   - Press `Esc` to enter into the `normal` mode
   - `:w` for saving the file 
  
