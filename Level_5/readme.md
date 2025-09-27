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
   ![c_des1](images/c_des1.png)

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
  
   
   <div align="center">:star::star::star::star::star::star:</div> 
   
## :trophy: Level Status: 

- All objectives completed.
- I have learned about Gate level simulation (GLS) and synthesis-simulation mismatch issues due to `missing sensitivity list` and `blocking statement ordering`.
- 🔓 Next level unlocked 🔜 [Level-5(Day-5): Optimization in synthesis (If,case,for,generate useage in verilog)](../Level_5/readme.md).





