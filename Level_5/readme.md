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
   
  
 ### :microscope: Lab-2:`Blocking statement issue` Functional simulation of RTL design and GLS simulation (Test design: `blocking_caveat.v`)
   
   :zap: Open the `blocking_caveat.v` file using text editor (For viewing the code not for simulation)-
     
   ```
   $ gvim blocking_caveat.v 
   ```
   ![gls_des_2](images/gls_des_2.png)

   :bulb:
   
   :zap: Simulate `blocking_caveat.v`-

   ```
   $ iverilog blocking_caveat.v tb_blocking_caveat.v
   $ ./a.out
   $ gtkwave tb_blocking_caveat.vcd

   ```

   ![w1_bc](images/w1_bc.png)

   :bulb: Functional simulation shows that it is not acting like intended.

   :zap: Synthesize `blocking_caveat.v` and generate netlist-
   
   ```
   $ yosys
   $ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ read_verilog blocking_caveat.v
   $ synth -top blocking_caveat
   $ abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   $ show
   ```
   ![s_bc](images/s_bc.png)

   Generate netlist-
   
   ```
   $ write_verilog -noattr blocking_caveat_net.v
   ```

   :bulb: It generated an `and` and an 'or' cell.

   :zap: Gate level simulation of `blocking_caveat.v`
   
   
 Give the netlist `blocking_caveat_net.v` ,premitive ,standard cells and the testbench used for RTL design case `tb_blocking_caveat.v` to iverilog simulator-
    
   ```
   $ iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v
   $ ./a.out
   $ gtkwave tb_blocking_caveat.vcd

   ```
   ![w2_bc](images/w2_bc.png)

   :x: Here is no `Synthesis-simulation` mismatch.
   
   :bulb: This mismatch is caused by `blocking statement ordereing issue`.

   :warning: Use blocking assignment statements cautiously.
 
   <div align="center">:star::star::star::star::star::star:</div> 
   
## :trophy: Level Status: 

- All objectives completed.
- I have learned about Gate level simulation (GLS) and synthesis-simulation mismatch issues due to `missing sensitivity list` and `blocking statement ordering`.
- 🔓 Next level unlocked 🔜 [Level-5(Day-5): Optimization in synthesis (If,case,for,generate useage in verilog)](../Level_5/readme.md).





