# Level-5(Day-5): Optimization in synthesis (If,case,for,generate useage in verilog)

## List of Objectives

 - :dart: <b>Practiccal Objective-1:</b> []()
   - :microscope: <b>Lab-1:</b> []()
   - :microscope: <b>Lab-2:</b>[]()
     
 <div align="center">:star::star::star::star::star::star:</div> 
 
## :dart: Labs on incomplete `if`, 'case' statement and overlapping `case`
 ### :microscope: Lab-1:Incomplete `if` statement issue

   :zap: Open the `incomp_if.v` file using text editor (For viewing the code not for simulation)-
     
   ```
   $ gvim incomp_if.v 
   ```
   ![if_des](images/if_des.png)

   :bulb: `Else` statement missing.
   
   :zap: Simulate `incomp_if.v`-

   ```
   $ iverilog incomp_if.v tb_incomp_if.v
   $ ./a.out
   $ gtkwave tb_incomp_if.vcd

   ```

   ![w_if1](images/w_if1.png)

  :bulb:  `Inferred latch` behaviour is observed due to incomplete `if` statement.

   :zap: Synthesize `incomp_if.v`-
   
   ```
   $ yosys
   $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ read_verilog incomp_if.v
   $ synth -top incomp_if
   $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ show
   ```
   ![s_if1](images/s_if1.png)

  :bulb: A `latch` is generated instead of a `mux`.
   
  ---

  :zap: Open the `incomp_if2.v` file using text editor (For viewing the code not for simulation)-
     
   ```
   $ gvim incomp_if2.v 
   ```
   ![if_des_1](images/if_des_1.png)

   :bulb: `If` and `else if` statement present but `else` statement missing.
   
   :zap: Simulate `incomp_if2.v`-

   ```
   $ iverilog incomp_if2.v tb_incomp_if2.v
   $ ./a.out
   $ gtkwave tb_incomp_if2.vcd

   ```

   ![w_if2](images/w_if2.png)

  :bulb:  `Inferred latch` behaviour is observed due to incomplete `if` statement.

   :zap: Synthesize `incomp_if2.v`-
   
   ```
   $ yosys
   $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ read_verilog incomp_if2.v
   $ synth -top incomp_if2
   $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ show
   ```
   ![s_if2](images/s_if2.png)

  :bulb: A `latch` is generated instead of a `mux`.
   
  
### :microscope: Lab-2:Incomplete `case` statement issue, partial assignment overlapping `case` 
   :zap: Open the `incomp_case.v` file using text editor (For viewing the code not for simulation)-
     
   ```
   $ gvim incomp_case.v 
   ```
   ![c_des_1](images/c_des_1.png)

   :bulb: All cases are not present.
   
   :zap: Simulate `incomp_case.v`-

   ```
   $ iverilog incomp_case.v tb_incomp_case.v
   $ ./a.out
   $ gtkwave tb_incomp_case.vcd

   ```

   ![w_c1](images/w_c1.png)

  :bulb:  `Inferred latch` behaviour is observed due to incomplete `case` statement.

   :zap: Synthesize `incomp_case.v`-
   
   ```
   $ yosys
   $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ read_verilog incomp_case.v
   $ synth -top incomp_case
   $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ show
   ```
   ![s_c1](images/s_c1.png)

  :bulb: Output is `latched` for unassigned `cases`.
  
  :warning: Complete all cases or use `default` for generating combinational circuit.

 ---

  :zap: Open the `partial_case_assign.v` file using text editor (For viewing the code not for simulation)-
     
   ```
   $ gvim partial_case_assign.v 
   ```
   ![c_des_2](images/c_des_2.png)

   :bulb: All cases are present but all variables are not assigned in all cases.

   :x: There were some errors in the verilog file `tb_partial_case_assign.v`-
   
     - module name 
     - 'uut' name
     - `i3` port is not present in `uut`.
     - `sel` is two bit line not 1 bit.
     - dumpfile name
     
   :white_check_box:  Fixed version of `tb_partial_case_assign.v`.

   ![fix_tb_par](images/fix_tb_par.png)


   :zap: Simulate `partial_case_assign.v`-

   ```
   $ iverilog partial_case_assign.v tb_partial_case_assign.v
   $ ./a.out
   $ gtkwave tb_partial_case_assign.vcd

   ```

   ![w_c2](images/w_c2.png)

  :bulb:  `Inferred latch` behaviour is observed due to partial assignment.

   :zap: Synthesize `partial_case_assign.v`-
   
   ```
   $ yosys
   $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ read_verilog partial_case_assign.v
   $ synth -top partial_case_assign
   $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ show
   ```
   ![s_c2](images/s_c2.png)

  :bulb: Output is `latched` for `partial assignment issues`.
  
  :warning: Same variables should be assigned in all cases.
  
  ---

  :zap: Open the `bad_case.v` file using text editor (For viewing the code not for simulation)-
     
   ```
   $ gvim bad_case.v 
   ```
   ![c_des_3](images/c_des_3.png)

   :bulb: All cases are present but overlapping of cases occur due to ambiguous.
   
   :zap: Simulate `bad_case.v`-

   ```
   $ iverilog bad_case.v tb_bad_case.v
   $ ./a.out
   $ gtkwave tb_bad_case.vcd

   ```

   ![w_c3](images/w_c3.png)

  :bulb:  Unintended situation occurs for ambiguous `cases`.

   :zap: Synthesize `bad_case.v` and generate netlist-
   
   ```
   $ yosys
   $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ read_verilog bad_case.v
   $ synth -top bad_case
   $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ show
   ```
   ![s_c3](images/s_c3.png)

   Generate netlist-
   
   ```
   $ write_verilog -noattr bad_case_net.v
   ```

   :zap: Gate level simulation of `bad_case.v`
   
   
 Give the netlist `bad_case.v` ,premitive ,standard cells and the testbench used for RTL design case `tb_bad_case.v` to iverilog simulator-
    
   ```
   $ iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_case_net.v tb_bad_case.v
   $ ./a.out
   $ gtkwave tb_bad_case.vcd

   ```
   ![w_c4](images/w_c4.png)

   :x: Here is `Synthesis-simulation` mismatch.
   
   :bulb: This mismatch is caused by `overlapping case`.
 
   :bulb: Multiple cases can be evaluated, it is not like prioritize logic of `if` (only one condition evaluated for 'if').
  
   :warning: Overlapping cases should be avoided( as multiple cases are selected and unintended results are produced).
  

   
   <div align="center">:star::star::star::star::star::star:</div> 

## :dart: Labs on `for` loop and `for generate`
 ### :microscope: Lab-4: Introduction to `for` loop (Test design: `` )
   :zap: Open the `mux_generate.v` file using text editor (For viewing the code not for simulation)-
     
   ```
   $ gvim mux_generate.v 
   ```
   ![f_des_1](images/f_des_1.png)

   :bulb: It resides inside the `always` procedural block.

   :bulb: It helps to efficiently write the code for large design with multiple instantiation of same block.
   
   
   :zap: Simulate `mux_generate.v`-

   ```
   $ iverilog mux_generate.v tb_mux_generate.v
   $ ./a.out
   $ gtkwave tb_mux_generate.vcd

   ```

   ![w_f1](images/w_f1.png)

  :bulb:  It functionally same as mux.


 ### :microscope: Lab-4: Advantages of `for loop` over `case` statement (Test design: `demux_generate.v` and `demux_case.v`)

   :zap: (Using `case`) Open the `demux_case.v` file using text editor (For viewing the code not for simulation)-
     
   ```
   $ gvim demux_case.v 
   ```
   ![f_des_2](images/f_des_2.png)
   
   :zap: Simulate `demux_case.v`-

   ```
   $ iverilog demux_case.v tb_demux_case.v
   $ ./a.out
   $ gtkwave tb_demux_case.vcd

   ```

   ![w_f2](images/w_f2.png)

  :bulb:  It is acting like a demux.

  ---

  :zap: (Using `for`) Open the `demux_generate.v` file using text editor (For viewing the code not for simulation)-
     
   ```
   $ gvim demux_generate.v 
   ```
   ![f_des_3](images/f_des_3.png)
   
   :zap: Simulate `demux_generate.v`-

   ```
   $ iverilog demux_generate.v tb_demux_generate.v
   $ ./a.out
   $ gtkwave tb_demux_generate.vcd

   ```

   ![w_f3](images/w_f3.png)

  :bulb:  It is acting like a demux.

  :bulb: Use `for` loop over `case` to design large Demux.
  

   <div align="center">:star::star::star::star::star::star:</div> 
   
## :trophy: Level Status: 

- All objectives completed.
- I have learned about Gate level simulation (GLS) and synthesis-simulation mismatch issues due to `missing sensitivity list` and `blocking statement ordering`.
- 🔓 Next level unlocked 🔜 [Level-5(Day-5): Optimization in synthesis (If,case,for,generate useage in verilog)](../Level_5/readme.md).





