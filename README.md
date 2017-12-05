# utl_sometimes_a_macro_without_an_argument_will_not_create_a_local_symbol_table
Gotcha!   Sometimes a macro without an argument will not create a local symbol table.   When I call a macro without an argument local macro variables can become global.   X1 is global and has the value 2, while x2 is local to the macro and missing outside the macro.
