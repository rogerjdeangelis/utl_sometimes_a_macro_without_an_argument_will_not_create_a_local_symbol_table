# utl_sometimes_a_macro_without_an_argument_will_not_create_a_local_symbol_table
Gotcha!   Sometimes a macro without an argument will not create a local symbol table.   When I call a macro without an argument local macro variables can become global.   X1 is global and has the value 2, while x2 is local to the macro and missing outside the macro.
    Sometimes a macro without an argument will NOT create a local symbol table

    github
    https://goo.gl/UCMgCi
    https://github.com/rogerjdeangelis/utl_sometimes_a_macro_without_an_argument_will_not_create_a_local_symbol_table

    https://goo.gl/si5VFg
    https://communities.sas.com/t5/Base-SAS-Programming/Call-symput-in-a-macro-with-without-parameter-s-and-global/m-p/418306

    DerekG profile
    https://communities.sas.com/t5/user/viewprofilepage/user-id/99762

    PROBLEM
    =======
      Gotcha!
      Sometimes a macro without an argument will not create a local symbol table.
      When I call a macro without an argument local macro variables can become global.
      X1 is global and has the value 2, while x2 is local to the macro and missing outside the macro.

    *                               _
      _____  ____ _ _ __ ___  _ __ | | ___
     / _ \ \/ / _` | '_ ` _ \| '_ \| |/ _ \
    |  __/>  < (_| | | | | | | |_) | |  __/
     \___/_/\_\__,_|_| |_| |_| .__/|_|\___|
                             |_|
    ;

    %symdel x1 x2 / nowarn;

    data mydata;
        input a b;
        datalines;
        1 2
        3 4
        ;
    run;


    * macro without argument;
    %macro m1;
        data _null_;
            set mydata;
            if a=1 then call symput('x1', put(b, 1.));
        run;
    %mend m1;

    %macro m2(n=);
        data _null_;
            set mydata;
            if a=1 then call symput('x2', put(b, 1.));
        run;
    %mend m2;


    options mprint;
    %m1;
    %m2(n=1);

    %put &x1;
    %put &x2;


    451   %put &x1;
    2
    452   %put &x2;
    WARNING: Apparent symbolic reference X2 not resolved.
    &x2


