# utl-adding-the-missing-math-stat-and-string-functions-to-python-sql-pandasql-sqllite3
Adding the missing math stat and string functions to python sql pandasql sqllite3 libsqlitefunctions.dll 
    %let pgm=utl-adding-the-missing-math-stat-and-string-functions-to-python-sql-pandasql-sqllite3;

    Adding the missing math stat and string functions to python sql pandasql sqllite3 libsqlitefunctions.dll
    R has these functions builtin.

    github
    https://tinyurl.com/s5dtywa3
    https://github.com/rogerjdeangelis/utl-adding-the-missing-math-stat-and-string-functions-to-python-sql-pandasql-sqllite3

    Need these extensions for Win 10 padassql
    Compiled extensions
    https://tinyurl.com/yda8rc3k
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories/blob/master/libsqlitefunctions.dll

    You will need to compile?
    https://sqlite.org/contrib/download/extension-functions.c/download


      Missing functions in pandasql sqllite3

      Math         String
      ==========   ================
      acos         replicate
      asin         charindex
      atan         leftstr
      atn2         rightstr
      atan2        ltrim
      acosh        rtrim
      asinh        trim
      atanh        replace
      difference   reverse
      degrees      proper
      radians      padl
      cos          padr
      sin          padc
      tan          strfilter
      cot
      cosh         Aggregate
      sinh         ================
      tanh         stdev
      coth         variance
      exp          mode
      log          median
      log10        lower_quartile
      power        upper_quartile.
      sign
      sqrt
      square
      ceil
      floor
      pi

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /*----                                                                   ----*/
    /*----  functions stdev(standard deviation) and median are not present   ----*/
    /*----                                                                   ----*/

    /*----  SAMPLE INPUT                                                     ----*/

    libname sd1 "d:/sd1";
    data sd1.have;
      do x=1 to 4;
         output;
      end;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* SD1.HAVE total obs=4                                                                                                   */
    /*                                                                                                                        */
    /* Obs    X                                                                                                               */
    /*                                                                                                                        */
    /*  1     1                                                                                                               */
    /*  2     2                                                                                                               */
    /*  3     3                                                                                                               */
    /*  4     4                                                                                                               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


    %utl_submit_wps64x("
    options validvarname=any lrecl=32756;
    libname sd1 'd:/sd1';
    proc python;
    export data=sd1.have python=have;
    submit;
    from os import path;
    import pandas as pd;
    from pandasql import sqldf;
    want = sqldf('''
      select
          stdev(x)    as stdevx
         ,median(x)   as medianx
      from
         have
    ''');
    print(want);
    endsubmit;
    run;quit;
    ");

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* NOTE: no such function: median                                                                                         */
    /* NOTE: no such function: stdev                                                                                          */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*         _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| `_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    */

    %utl_submit_wps64x("
    libname sd1 'd:/sd1';
    proc python;
    export data=sd1.have python=have;
    submit;
    from os import path;
    import pandas as pd;
    import numpy as np;
    import pandas as pd;
    from pandasql import sqldf;
    mysql = lambda q: sqldf(q, globals());
    from pandasql import PandaSQL;
    pdsql = PandaSQL(persist=True);
    sqlite3conn = next(pdsql.conn.gen).connection.connection;
    sqlite3conn.enable_load_extension(True);
    sqlite3conn.load_extension('c:/temp/libsqlitefunctions.dll');
    mysql = lambda q: sqldf(q, globals());
    want = pdsql('''
      select
          stdev(x)    as stdevx
         ,median(x)   as medianx
      from
         have
    ''');
    print(want);
    endsubmit;
    run;quit;
    ");

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  The WPS System                                                                                                        */
    /*                                                                                                                        */
    /*  The PYTHON Procedure                                                                                                  */
    /*                                                                                                                        */
    /*       STDEVX  MEDIANX                                                                                                  */
    /*                                                                                                                        */
    /*  0  1.290994      2.5                                                                                                  */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

