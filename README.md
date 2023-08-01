# utl-round-up-to-the-nearest-mutiple-of-n-using-fcmp-code-fx-equals-ceil-x-divided-by-n-times-n
Round up to the nearest mutiple of n using fcmp code fx equals ceil x divided by n times n 
    %let pgm=utl-round-up-to-the-nearest-mutiple-of-n-using-fcmp-code-fx-equals-ceil-x-divided-by-n-times-n;

    Round up to the nearest mutiple of n using fcmp code fx equals ceil x divided by n times n

      Two Solutions

           1. wps fcmp
           2. wps macro


    Simple example of rounding up to the nearest mutiple of n.

    github
    https://tinyurl.com/4xcf29nv
    https://github.com/rogerjdeangelis/utl-round-up-to-the-nearest-mutiple-of-n-using-fcmp-code-fx-equals-ceil-x-divided-by-n-times-n

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    libname sd1 "d:/sd1";

    data sd1.have;
     input x @@;
    cards4;
    9 11.5 15 6.9 5.9
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                       |                                                                                                */
    /*                       | RULES (nearest mutiple of 3)                                                                   */
    /*                       |                                                                                                */
    /* SD1.HAVE total obs=5  | SD1.HAVE total obs=5                                                                           */
    /*                       |                                                                                                */
    /* Obs     X             | Obs     X     Y                                                                                */
    /*                       |                                                                                                */
    /*  1      9.0           |  1      9.0   9                                                                                */
    /*  2     11.5           |  2     11.5   12   Nearest multiple of 3 is 12                                                 */
    /*  3     15.0           |  3     15.0   15                                                                               */
    /*  4      6.9           |  4      6.9   9    Nearest multiple of 3 is 9                                                  */
    /*  5      5.9           |  5      5.9   6                                                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


    /*                         __
    / | __      ___ __  ___   / _| ___ _ __ ___  _ __
    | | \ \ /\ / / `_ \/ __| | |_ / __| `_ ` _ \| `_ \
    | |  \ V  V /| |_) \__ \ |  _| (__| | | | | | |_) |
    |_|   \_/\_/ | .__/|___/ |_|  \___|_| |_| |_| .__/
                 |_|                            |_|
    */


    %utl_submit_wps64x('
    libname sd1 "d:/sd1";
    options cmplib=work.functions;
    proc fcmp outlib=work.functions.temp;
    Subroutine roundup(x, y, base);
        outargs y;
        y = ceil(x/base)*base;
    endsub;
    run;quit;

    data sd1.want ;
        set sd1.have;
        call roundup(x,y,3);
        put y;
    run;quit;

    proc print;
    run;quit;
    ');

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  The WPS System                                                                                                        */
    /*                                                                                                                        */
    /*  Obs     X      Y                                                                                                      */
    /*                                                                                                                        */
    /*   1      9.0     9                                                                                                     */
    /*   2     11.5    12                                                                                                     */
    /*   3     15.0    15                                                                                                     */
    /*   4      6.9     9                                                                                                     */
    /*   5      5.9     6                                                                                                     */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___
    |___ \  __      ___ __  ___   _ __ ___   __ _  ___ _ __ ___
      __) | \ \ /\ / / `_ \/ __| | `_ ` _ \ / _` |/ __| `__/ _ \
     / __/   \ V  V /| |_) \__ \ | | | | | | (_| | (__| | | (_) |
    |_____|   \_/\_/ | .__/|___/ |_| |_| |_|\__,_|\___|_|  \___/
                     |_|
    */

    %utl_submit_wps64x('
    libname sd1 "d:/sd1";
    %macro roundup(x,base)/des="roundup x to the nearest mutiple of n";
         ceil(&x/&base)*&base
    %mend roundup;

    data sd1.want ;
        set sd1.have;
        y = %roundup(x,3);
        put y;
    run;quit;

    proc print;
    run;quit;
    ');

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* The WPS System                                                                                                         */
    /*                                                                                                                        */
    /* Obs     X      Y                                                                                                       */
    /*                                                                                                                        */
    /*  1      9.0     9                                                                                                      */
    /*  2     11.5    12                                                                                                      */
    /*  3     15.0    15                                                                                                      */
    /*  4      6.9     9                                                                                                      */
    /*  5      5.9     6                                                                                                      */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
