# Smart Always snippets
###Description
The snippets for the always block are context dependant and configurable:

 - always ff, always comb, always latch are specific to file with extension .sv
 - Signal name for clk, clk_en and reset (low and high) can be configured (see below).
 - The clock enable part of the snippets will be present only if the a signal with the correct name has been declared


The name for clk and reset can be extracted from the current buffer:

 - if the default clock name is not found in any posedge signal_name list, the highest occurence of a signal with a c in its name will be used
 - if the default reset low name is not found in any negedge signal_name list, the highest occurence of will be used
 - if the default reset high name is not found in any posedge signal_name list, the highest occurence of a signal without a c in its name will be used

The automatic extraction of the name will not be perfect in all cases, but it will always be better than the basic behavior

###Configuration
 - `sv.clk_name` : Clock name, default to "clk".
 - `sv.rst_n_name` : Reset active low,  default to "rst_n"
 - `sv.rst_name`: Reset active high, default to "rst".
 - `sv.always_name_auto`: Boolean to enable clk/rst name auto extraction, default to true
 - `sv.always_sv_only`: Boolean to filter simple always in .sv files, default to true.
 - `sv.clk_en_name`: Clock enable name, default to "clk_en"
 - `sv.always_ce_auto` : Boolean to insert the clock enable part only if the clk enable has been declared. Default to true.
 - `sv.always_ff_begin_end` : Boolean to add begin/end for the whole always block. Default to true
 - `sv.always_label` : Boolean to add a label to the always block. Default to true and only valid if begin/end is enabled.
 - `sv.always_one_cursor` : Boolean to simplify the snippet to position the cursor on the first line. Default to false.
 - `sv.disable_autocomplete` : Boolean to fully disable smart auto-completion, mainly for debug, default to false.
 - `sv.completion.xxx` : Completion list where xxx can be systemtask (for any completion starting with $), tick (for compiler directive) and uvm.
To only modify one element of the list use the setting `sv.completion.xxx.user` . The completion is defined as a list with 3 elements: the trigger word, the description and code snippets.

### Example
Here is a quick example showing how the always snippets adapts automatically to the context:
<video controls>
  <source src="../images/always.webm" type="video/webm">
Your browser does not support the video tag.
</video>


---
# Intellisense-like autocompletion

### Description
This feature provides contextual auto-completion after a . :

 - For standard type the completion will provide the possible function (insert, pop, push for a queue for example).
 - For structure or interface, you will have access to the fields.
 - For classes, you get access to public fields and auto-snippets for function. The object "this" gives also access to protected and private members.
 - Inside an instance, this will provides completion for all ports not connected yet


This feature also supports the scope operator (::) :

 - For a package you will get all typedef and signal declared inside the package
 - For an enum type you will get all the possible values

Struture assignement is also supported: just call manually the autocompletion while inside the structure assignement (mystruct ='{}) and you get a list of all non affected field.

### Example
Here is a quick example showing various autocompletion for interface, struct, module binding:
<video controls>
  <source src="../images/completion.webm" type="video/webm">
Your browser does not support the video tag.
</video>

---
# FSM template

### Description
IF you have defined one signal in your module as an enum (either directly or
through an typedef defined in the same model or in a package),
you can create the template for the associated FSM.

To access this function, use the palette with the command `Verilog: Insert FSM template`.
You will be asked to select a signal (state) amongst the list of all available signal.

The template is two processes : one synchronous with state <= state\_next and the second combinatorial with a case(state) with all possible value and state_next value default to state.

Note that this works for any enum or bit vector.

The corresponding Sublime command (for keybinding or use in your own plugin) is `verilog_insert_fsm_template`

### Case completion
If you have written `case(my_signal)` you can call manually the autocompletion (*ctrl+space* by default in sublime) to have all possible value filled.

This works for any enum or bit vector. This also works if you are doing your case on only part of a signal like case(cnt[2:1]) will only result in 4 possible values.

### Example
Here is a quick example showing insertion of the FSM template and autocompletion of case on a bit vector:
<video controls>
  <source src="../images/fsm.webm" type="video/webm">
Your browser does not support the video tag.
</video>

---
# Simple Snippets
The plugin provides snippets for a lot of standard keyword or system task.

### SystemVerilog Keywords
 - module
 - interface
 - package
 - class
 - case
 - function/task
 - for loop

### Comment box
You can create a comment box using `///` as a trigger.

### Macro
Trigger for macro is `\``

You will get the most used ones: include, define, ifdef, ...

This can be modified/expanded using the config `sv.completion.tick.user` or fully redefined with `sv.completion.tick`

### System Tasks
Trigger for macro is `$`

You will get the most used ones: $display, $sformatf, $signed, $fopen, ...

This can be modified/expanded using the config `sv.completion.systemtask.user` or fully redefined with `sv.completion.systemtask`

### UVM functions

A few UVM functions are available as snippets:

 - uvm_config_db_get : uvm_config_db#()::get(this, "$1", "$0", $0);
 - uvm_config_db_set : uvm_config_db#()::set(this, "$1", "$0", $0);
 - uvm_report_info   : uvm_report_info("$1", "$0", UVM_NONE);
 - uvm_report_warning: uvm_report_warning("$1", "$0");
 - uvm_report_error  : uvm_report_error("$1", "$0");
 - uvm_report_fatal  : uvm_report_fatal("$1", "$0");

This can be modified/expanded using the config `sv.completion.uvm.user` or fully redefined with `sv.completion.uvm`

---
# Find unused signals

This function allows to look for signal declared but not used: after executing the command you get the list of unused signal in the input panel.

If you hit enter, all remaining signals name in the list will be removed from the code.

If you hit escape, all signals are simply selected.
<video controls>
  <source src="../images/unused.webm" type="video/webm">
Your browser does not support the video tag.
</video>
