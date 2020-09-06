# Instantiation

## Description
Use palette command `Verilog: Instantiate Module` or use keybinding to function `verilog_module_inst` (ctrl+F10).

This open the palette with all verilog file (*.v, *.sv) from the project or all opened file in the current window if not inside a project: select one and the instantiation will be inserted in the buffer.

If the module has some parameter you can enter the value of each parameter one by one:

 - If the default value is good you can directly press enter
 - If you enter "parameter myParam = value" or "localparam myParam = value" this will add myParam to the declaration list
 - If setting sv.param_propagate is true the default value proposed is the declaration of a new parameter with the same name and same default value

If autoconnection is enabled, signal with same name as port will be used as connection.
If they have not been declared, the signal declaration will also be added.
Location of signal declaration is configurable:

 - Just above module instantiation
 - First empty line after a start pattern
 - Last empty line between a start and an end pattern

Options allows to extend search to a signal matching port name with a prefix (ending with \_) or a suffix (starting with \_).
In case of multiple match, if one prefix/suffix is contained in the instance name it will be selected,
otherwise the first one will be used.

If you use some prefix/suffix in your ports name, they can be ignored when searching for a matching signal: this is defined by a list of prefix and suffix (see [Configuration](#configuration) ).

When autoconnection is used you will get a status about number of signal declaration added, list of non perfect matching connection (port data_i connected to signal data for example) and information about mismatches between signal and port definition.
In case of mismatch, a comment is added on the connection line about the expected type and the defined type.

## Configuration

 - `sv.fillparam`: On module instantiation with parameter user is asked a value for each parameter. Default to true.
 - `sv.param_explicit`: On module instantiation with parameter, default value can be explicitly mapped. Default to false.
 - `sv.autoconnect`: Control if signals are created and connected in module instantiation. Default to true.
 - `sv.autoconnect_allow_prefix`: True to expand search for signal to \w+_port. Default to true.
 - `sv.autoconnect_allow_suffix`: True to expand search for signal to port_\w+. Default to true.
 - `sv.autoconnect_port_prefix`: List of string of prefix to be removed before looking for matching signal. Default to empty list.
 - `sv.autoconnect_port_suffix`: List of string of suffix to be removed before looking for matching signal. Default to empty list.
 - `sv.instance_prefix`: Prefix to the module instantiation name, default to "i_".
 - `sv.instance_suffix`: Suffix to the module instantiation name, default to "" (no suffix).
 - `sv.decl_indent`: Number of indentation level for signal declaration, default to 1.
 - `sv.decl_start`: Pattern to find for start of signals auto-declaration . Empty string to get declaration just above instantiation. Default to "Signals declaration".
 - `sv.decl_end`: Pattern to find just after start to insert signal declaration before. Empty string to use first empty line after start pattern. Default to "/*----"
 - `sv.param_oneline`: On module instantiation with parameter, check if paramter binding can fit on one line. Default to true.
 - `sv.inst_oneline`: On module instantiation check if complete instantiation can fit on one line. Default to true.
 - `sv.param_explicit`: Control if parameter setting is explicit (appears in module instantiation even when default is used). Default to false.
 - `sv.param_propagate`: Control if symbolic parameter are used instead of default value. Default to false.

---
# Dot Star toggling
If the cursor is inside a module instantiation it is possible to toggle on/off the .* feature of System Verilog binding.

If the .* is already used, this will expand it to have explicit connection. Note that no check is done to verify that a signal with the correct name have been declared.

If there is no .\*, all binding with same port and signal name will be removed and replaced by a single .\*

Use palette command `Verilog: Toggle .*` or use keybinding to function `verilog_toggle_dot_star`.

In the keybinding file provided in this doc, the command is associated to *ctrl+shift+F10*.

---
# Example
Here is an example showing module instantiation with autoconnect activated and the toggling on/off of .*

<video controls>
  <source src="../images/instance.webm" type="video/webm">
Your browser does not support the video tag.
</video>
