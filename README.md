# utl_hash_lookup_with_multiple_keys_nice_simple_example
Hash lookup with multiple keys nice simple example.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Hash lookup with multiple keys nice simple example                                                    
                                                                                                          
    Same result in WPS and SAS                                                                            
                                                                                                          
    see                                                                                                   
    https://stackoverflow.com/questions/50749244/can-i-do-hash-merge-by-multiple-keys-in-sas              
                                                                                                          
    Richard's profile                                                                                     
    https://stackoverflow.com/users/1249962/richard                                                       
                                                                                                          
                                                                                                          
    INPUT                                                                                                 
    =====                                                                                                 
                                                                                                          
    MULTIPLE KEYS                                                                                         
                                                                                                          
    WORK.HAVE total obs=5                                                                                 
                                                                                                          
      LUKEY1    LUKEY2                                                                                    
                                                                                                          
         1         1                                                                                      
         1         2                                                                                      
         2         4                                                                                      
         3         6                                                                                      
         3         7                                                                                      
                                                                                                          
    WORK.ALL total obs=100                                                                                
                                                   |  RULES                                               
       KEY1    KEY2    X1    X2    X3    X4    X5  |                                                      
                                                   |                                                      
         1       1      1     2     3     4     5  |  ** match output                                     
         1       2      1     2     3     4     5  |  ** match output                                     
         1       3      1     2     3     4     5  |  ** skip nomatch                                     
         1       4      1     2     3     4     5  |  ** skip nomatch                                     
         1       5      1     2     3     4     5  |  ** skip nomatch                                     
      ....                                                                                                
                                                                                                          
    PROCESS                                                                                               
    =======                                                                                               
                                                                                                          
    data want;                                                                                            
      length lukey1 lukey2 8;                                                                             
      call missing (lukey1,lukey2);                                                                       
      if _n_ = 1 then do;                                                                                 
        declare hash elig (dataset:"have");                                                               
        elig.defineKey ('lukey1','lukey2');                                                               
        elig.defineDone ();                                                                               
      end;                                                                                                
      set all;                                                                                            
      if 0 = elig.find(key:key1, key:key2);                                                               
    run;                                                                                                  
                                                                                                          
                                                                                                          
    OUTPUT                                                                                                
    ======                                                                                                
                                                                                                          
    WORK.WANT total obs=5                                                                                 
                                                                                                          
                 KEYS MATCH                                                                               
      ================================                                                                    
      LUKEY1    LUKEY2    KEY1    KEY2    X1    X2    X3    X4    X5                                      
                                                                                                          
         1         1        1       1      1     2     3     4     5                                      
         1         2        1       2      1     2     3     4     5                                      
         2         4        2       4      1     2     3     4     5                                      
         3         6        3       6      1     2     3     4     5                                      
         3         7        3       7      1     2     3     4     5                                      
                                                                                                          
    *                _              _       _                                                             
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _                                                      
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |                                                     
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |                                                     
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|                                                     
                                                                                                          
    ;                                                                                                     
                                                                                                          
    data have;                                                                                            
      input lukey1 lukey2;                                                                                
    cards4;                                                                                               
    1 1                                                                                                   
    1 2                                                                                                   
    2 4                                                                                                   
    3 6                                                                                                   
    3 7                                                                                                   
    ;;;;                                                                                                  
    run;quit;                                                                                             
                                                                                                          
    data all;                                                                                             
      do key1 = 1 to 10; do key2 = 1 to 10;                                                               
        array x(5) (1:5);                                                                                 
        output;                                                                                           
      end; end;                                                                                           
    run;                                                                                                  
                                                                                                          
    %utl_submit_wps64('                                                                                   
    libname wrk sas7bdat "%sysfunc(pathname(work))";                                                      
    data want;                                                                                            
      length lukey1 lukey2 8;                                                                             
      call missing (lukey1,lukey2);                                                                       
      if _n_ = 1 then do;                                                                                 
        declare hash elig (dataset:"wrk.have");                                                           
        elig.defineKey ("lukey1","lukey2");                                                               
        elig.defineDone ();                                                                               
      end;                                                                                                
      set wrk.all;                                                                                        
      if 0 = elig.find(key:key1, key:key2);                                                               
    run;quit;                                                                                             
    proc print;                                                                                           
    run;quit;                                                                                             
    ');                                                                                                   
                                                                                                          
