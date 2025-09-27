# Level-3(Day-3): Gate level simulation,blocking vs non-blocking statement,synthesis-simulation mismatch


## List of Objectives

 - :dart: <b>Practiccal Objective-1:</b> []()
   - :microscope: <b>Lab-1:</b> []()
     
 <div align="center">:star::star::star::star::star::star:</div> 
 
## :dart: Lab on GLS and `Synthesis-Simulation mismatch`
 ### :microscope: Lab-1: Functional simulation of RTL design and GLS simulation (Test design: `ternary_operator_mux.v`)
   
   :zap: Open the `ternary_operator_mux.v` file using text editor (For viewing the code not for simulation)-
     
   ```
   $ gvim ternary_operator_mux.v 
   ```
   ![gls_des](images/gls_des.png)

   :bulb: Our aim is MUX, here one approach is shown using ternary operator.
   
   :zap: Simulate `ternary_operator_mux.v`-

   ```
   $ iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
   $ ./a.out
   $ gtkwave tb_ternary_operator_mux.vcd

   ```

   ![w1_te_mux](images/w1_te_mux.png)

   :bulb: Functional simulation shows that it is acting like a mux.

   :zap: Synthesize `ternary_operator_mux.v` and generate netlist-
   
   ```
   $ yosys
   $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ read_verilog ternary_operator_mux.v
   $ synth -top ternary_operator_mux
   $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ show
   ```
   ![s_te_mux](images/s_te_mux.png)

   Generate netlist-
   
   ```
   $ write_verilog -noattr ternary_operator_mux_net.v
   ```

   :bulb: It is generated a `mux` cell.

   :zap: Gate level simulation of `ternary_operator_mux.v`
   
   
 Give the netlist `ternary_operator_mux_net.v` ,premitive ,standard cells and the testbench used for RTL design case `tb_ternary_operator_mux.v` to iverilog simulator-
    
   ```
   $ iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v
   $ ./a.out
   $ gtkwave tb_ternary_operator_mux.vcd

   ```
   ![w2_te_mux](images/w2_te_mux.png)

   :white_check_mark: Here is no `Synthesis-simulation` mismatch.

  ---

  :zap: Open the `bad_mux.v` file using text editor (For viewing the code not for simulation)-
     
   ```
   $ gvim bad_mux.v 
   ```
   ![gls_des_1](images/gls_des_1.png)

   :bulb: Our aim is MUX, here one approach is shown using procedural block.
   
   :zap: Simulate `bad_mux.v`-

   ```
   $ iverilog bad_mux.v tb_bad_mux.v
   $ ./a.out
   $ gtkwave tb_bad_mux.vcd

   ```

   ![w1_bm](images/w1_bm.png)

   :bulb: Functional simulation shows that it is not acting like a mux.

   :zap: Synthesize `bad_mux.v` and generate netlist-
   
   ```
   $ yosys
   $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ read_verilog bad_mux.v
   $ synth -top bad_mux
   $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ show
   ```
   ![s_bm](images/s_bm.png)

   Generate netlist-
   
   ```
   $ write_verilog -noattr bad_mux_net.v
   ```

   :bulb: It is generated a `mux` cell.

   :zap: Gate level simulation of `bad_mux.v`
   
   
 Give the netlist `bad_mux_net.v` ,premitive ,standard cells and the testbench used for RTL design case `tb_bad_mux.v` to iverilog simulator-
    
   ```
   $ iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_net.v tb_bad_mux.v
   $ ./a.out
   $ gtkwave tb_bad_mux.vcd

   ```
   ![w2_bm](images/w2_bm.png)

   :x: Here is `Synthesis-simulation` mismatch.
   
     
  <div align="center">:star::star::star::star::star::star:</div> 
 
## :dart: Lab on Sequential logic optimization (`Sequential constant`)
 ### :microscope: Lab-2: Observe the designs `dff_cons*.v`
   
  :zap: Open the designs `dff_cons*.v` using text editor-
  
   ```
   $ gvim dff_cons*.v
   ```
   ![opt_dff_des](images/opt_dff_des.png)
   
   :bulb: Here we have to find the `sequential constant` cases.
   ### :microscope: Lab-3: Simulate the designs `dff_cons*.v`
   
  :zap: Simulate design `dff_const1.v` using iverilog-
     
   ```
  $ iverilog dff_const1.v tb_dff_const1.v
  $ ./a.out
  $ gtkwave tb_dff_const1.vcd
  ```
  ![w_dff_con_1](images/w_dff_con_1.png)

  :bulb: Output `q` is changing. It is not an example of sequential constant.

  :zap: Simulate design `dff_const2.v` using iverilog-
     
   ```
  $ iverilog dff_const2.v tb_dff_const2.v
  $ ./a.out
  $ gtkwave tb_dff_const2.vcd
  ```
  ![w_dff_con_2](images/w_dff_con_2.png)

  :bulb: Output `q` is not changing. It is an example of sequential constant.

  :zap: Simulate design `dff_const3.v` using iverilog-
     
   ```
  $ iverilog dff_const3.v tb_dff_const3.v
  $ ./a.out
  $ gtkwave tb_dff_const3.vcd
  ```
  ![w_dff_con_3](images/w_dff_con_3.png)

  :bulb: Output `q` is changing. It is not an example of sequential constant.

  :zap: Simulate design `dff_const4.v` using iverilog-
     
   ```
  $ iverilog dff_const4.v tb_dff_const4.v
  $ ./a.out
  $ gtkwave tb_dff_const4.vcd
  ```
  ![w_dff_con_4](images/w_dff_con_4.png)

  :bulb: Output `q` is not changing. It is an example of sequential constant.

  :zap: Simulate design `dff_const5.v` using iverilog-
     
   ```
  $ iverilog dff_const5.v tb_dff_const5.v
  $ ./a.out
  $ gtkwave tb_dff_const5.vcd
  ```
  ![w_dff_con_5](images/w_dff_con_5.png)

  :bulb: Output `q` is changing. It is not an example of sequential constant.

  ### :microscope: Lab-4: Synthesize the designs `dff_cons*.v` and observe optimizations
  
  :zap: Synthesize the design `dff_cont1.v` using Yosys and SKY130 PDK-
  
  ```
  $ yosys
  $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ read_verilog dff_const1.v
  $ synth -top dff_const1
  $ dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ show

  ```

  ![s_dff_con_1](images/s_dff_con_1.png)
  
  :bulb: Here an asynchronous reset D flip-flop is generated with input `d` always `1'b1'.
  
  :bulb: It is not an example of `sequential constant` optimization.

  ---
  :zap: Synthesize the design `dff_cont2.v` using Yosys and SKY130 PDK-
  
  ```
  $ yosys
  $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ read_verilog dff_const2.v
  $ synth -top dff_const2
  $ dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ show

  ```

  ![s_dff_con_2](images/s_dff_con_2.png)
  
  :bulb: Here an asynchronous reset D flip-flop is generated with input `d` always `1'b0'.
  
  :bulb: It is an example of `sequential constant` optimization.

  ---
  :zap: Synthesize the design `dff_cont3.v` using Yosys and SKY130 PDK-
  
  ```
  $ yosys
  $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ read_verilog dff_const3.v
  $ synth -top dff_const3
  $ dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ show

  ```

  ![s_dff_con_3](images/s_dff_con_3.png)
  
  :bulb: Here one asynchronous reset D flip-flop and one asynchronous set D flip-flop are generated.
  
  :bulb: It is not an example of `sequential constant` optimization.

  ---
  :zap: Synthesize the design `dff_cont4.v` using Yosys and SKY130 PDK-
  
  ```
  $ yosys
  $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ read_verilog dff_const4.v
  $ synth -top dff_const4
  $ dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ show

  ```

  ![s_dff_con_4](images/s_dff_con_4.png)
  
  
  :bulb: It is an example of `sequential constant` optimization.

  ---
  :zap: Synthesize the design `dff_cont5.v` using Yosys and SKY130 PDK-
  
  ```
  $ yosys
  $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ read_verilog dff_const5.v
  $ synth -top dff_const5
  $ dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ show

  ```

  ![s_dff_con_5](images/s_dff_con_5.png)
  
  :bulb: Here two asynchronous reset D flip-flop are generated with input `d` always `1'b1'.
  
  :bulb: It is not an example of `sequential constant` optimization.

  ---

 ## :dart: Lab on Sequential logic optimization (`Sequential unused output`)
 ### :microscope: Lab-5: Observe the designs `counter_opt*.v`
   
  :zap: Open the designs `dff_cons*.v` using text editor-
  
   ```
   $ gvim counter_opt*.v
   ```
   ![seq_un_op_des](images/seq_un_op_des.png)
   
   :bulb: Here we have to find the `sequential unused output` cases.
 
  ### :microscope: Lab-6: Synthesize the designs `counter_opt*.v` and observe optimizations
  
  :zap: Synthesize the design `counter_opt.v` using Yosys and SKY130 PDK-
  
  ```
  $ yosys
  $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ read_verilog counter_opt.v
  $ synth -top counter_opt
  $ dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ show

  ```

  ![seq_un_op_synt_1](images/seq_un_op_synt_1.png)
  
  :bulb: Here only one D flipflop generated for `LSB` bit of counter as other two bits of counter are not used for output.
  
  :bulb: It is an example of `sequential unused ouput` optimization.

  ---
:zap: Synthesize the design `counter_opt2.v` using Yosys and SKY130 PDK-
  
  ```
  $ yosys
  $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ read_verilog counter_opt2.v
  $ synth -top counter_opt2
  $ dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  $ show

  ```

  ![seq_un_op_synt_2](images/seq_un_op_synt_2.png)
  
  :bulb: Here three D flipflop generated for as three bits of counter are used for output.
  
  :bulb: It is not an example of `sequential unused ouput` optimization.

  ---
 
   <div align="center">:star::star::star::star::star::star:</div> 
   
## :trophy: Level Status: 

- All objectives completed.
- I have learned about different combinational and sequential logic optimization during synthesis.
- 🔓 Next level unlocked 🔜 [Level-5(Day-5): Optimization in synthesis (If,case,for,generate useage in verilog)](../Level_5/readme.md).




