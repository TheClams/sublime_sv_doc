# Alignment
This function will help keep your code properly align.

It works for port declaration, module instantiation, signal declaration and assignement.

This is available from the palette under the name `Verilog: Alignment`.

The corresponding Sublime command (for keybinding or use in your own plugin) is `verilog_align`

In the keybinding file provided in this doc, the command is associated to *ctrl+shift+a*


---
### Reindentation
It is possible to only call the reindent part of the function without using the special alignment. Just pass as argument cmd {"cmd":"reindent"}.

In the keybinding file provided in this doc, the command is associated to *alt+shift+a*

---
### Configuration

Here is the list of configuration parameter for alignment:

 - `sv.one_bind_per_line` : For module instantiation, force only one binding per line. Default to true.
 - `sv.one_decl_per_line` : For signal declaration, force only one signal per declaration. Default to false.
 - `sv.max_line_length`   : Split one line into multiple if too long. Default to 120. Unused for the moment ...
 - `sv.strip_empty_line`  : Strip empty line inside module declaration. Default to true.
 - `sv.mod_import_same_line`  : When aligning module declaration, put import statement on same line as module. Default to false.
 - `sv.alignment_ignore_tick` : Ignore line identation for every line starting with \`ifdef, \`elsif ... Default to false.
 - `sv.align_comma_semicolon` : Aligne comma/semi-colon for signal/port declaration. Default to true.

---
### Example

<video controls>
  <source src="../images/alignment.webm" type="video/webm">
Your browser does not support the video tag.
</video>