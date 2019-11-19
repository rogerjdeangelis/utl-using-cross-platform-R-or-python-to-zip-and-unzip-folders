# utl-using-cross-platform-R-or-python-to-zip-and-unzip-folders
Using cross platform R and Python to zip and unzip folders   

    SAS Forum: Using cross platform R and Python to zip and unzip folders                                                
                                                                                                                         
      Two Solutions (probably should add PERL, but too lazy)                                                             
                                                                                                                         
              a. R library zip                                                                                           
              b. R python shutil                                                                                         
                                                                                                                         
    github                                                                                                               
    https://tinyurl.com/wvgcy2o                                                                                          
    https://github.com/rogerjdeangelis/utl-using-cross-platform-R-or-python-to-zip-and-unzip-folders                     
                                                                                                                         
    for single file zip see                                                                                              
    github                                                                                                               
    https://tinyurl.com/yycmtpks                                                                                         
    https://github.com/rogerjdeangelis/utl-using-SAS-R-unix-commands-to-zip-and-unzip-files-on-windows-and-unix          
                                                                                                                         
    https://tinyurl.com/sdodumk                                                                                          
    https://communities.sas.com/t5/SAS-Programming/Create-zip-file-of-all-files-in-a-folder/m-p/605016                   
                                                                                                                         
    Create zip file of all files in a folder                                                                             
                                                                                                                         
    Python install                                                                                                       
    pip install pytest-shutil                                                                                            
                                                                                                                         
    *_                   _                                                                                               
    (_)_ __  _ __  _   _| |_                                                                                             
    | | '_ \| '_ \| | | | __|                                                                                            
    | | | | | |_) | |_| | |_                                                                                             
    |_|_| |_| .__/ \__,_|\__|                                                                                            
            |_|                                                                                                          
    ;                                                                                                                    
                                                                                                                         
    * ceate a directory and with files;                                                                                  
    data _null_;                                                                                                         
                                                                                                                         
      * create directory;                                                                                                
      if _n_=0 then do;                                                                                                  
          %let rc=%sysfunc(dosubl('                                                                                      
             data _null_;                                                                                                
                 rc=dcreate("txt","d:/");                                                                                
             run;quit;                                                                                                   
         '));                                                                                                            
      end;                                                                                                               
                                                                                                                         
      file "d:/txt/file1.txt"; put "file1";                                                                              
      file "d:/txt/file2.txt"; put "file2";                                                                              
      file "d:/txt/file3.txt"; put "file3";                                                                              
                                                                                                                         
    run;quit;                                                                                                            
                                                                                                                         
                                                                                                                         
    d:/txt/file1.txt                                                                                                     
    d:/txt/file2.txt                                                                                                     
    d:/txt/file3.txt                                                                                                     
                                                                                                                         
    *            _               _                                                                                       
      ___  _   _| |_ _ __  _   _| |_                                                                                     
     / _ \| | | | __| '_ \| | | | __|                                                                                    
    | (_) | |_| | |_| |_) | |_| | |_                                                                                     
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                    
                    |_|                                                                                                  
    ;                                                                                                                    
                                                                                                                         
    Volume in drive D                                                                                                    
                                                                                                                         
    Directory of d:\zip     Size    Filename                                                                             
                                                                                                                         
    11/19/2019  01:20 PM     734    fyls.zip                                                                             
                                                                                                                         
    Contents of Zip file                                                                                                 
                                                                                                                         
    ARCLST total obs=5                                                                                                   
                                                                                                                         
     FILENAME         COMPRESS    UNCOMPRESS   TIMESTAMP    PERMISSION                                                   
                                                                                                                         
     txt/                  0           0      1889786460      700                                                        
     txt/file1.txt        12           7      1889786448      600                                                        
     txt/file2.txt        12           7      1889786448      600                                                        
     txt/file3.txt        12           7      1889786448      600                                                        
     txt/r_pgm.txt       120         180      1889788832      600                                                        
                                                                                                                         
    *                                                                                                                    
     _ __  _ __ ___   ___ ___  ___ ___                                                                                   
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                                  
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                  
    | .__/|_|  \___/ \___\___||___/___/                                                                                  
    |_|                                                                                                                  
               ____        _                                                                                             
      __ _    |  _ \   ___(_)_ __                                                                                        
     / _` |   | |_) | |_  / | '_ \                                                                                       
    | (_| |_  |  _ <   / /| | |_) |                                                                                      
     \__,_(_) |_| \_\ /___|_| .__/                                                                                       
                            |_|                                                                                          
    ;                                                                                                                    
                                                                                                                         
    %utl_submit_r64('                                                                                                    
      library(zip);                                                                                                      
      library(SASxport);                                                                                                 
      dir<-"d:/txt";                                                                                                     
      zipr("d:/zip/fyls.zip",dir);                                                                                       
      arclst<-zip_list("d:/zip/fyls.zip");                                                                               
      str(arclst);                                                                                                       
      write.xport(arclst,file="d:/xpt/arclst.xpt");                                                                      
    ');                                                                                                                  
                                                                                                                         
    libname xpt xport "d:/xpt/arclst.xpt";                                                                               
    data arclst;                                                                                                         
      set xpt.arclst;                                                                                                    
    run;quit;                                                                                                            
    libname xpt clear;                                                                                                   
                                                                                                                         
    *_                          _     _ _   _ _                                                                          
    | |__     _ __  _   _   ___| |__ (_) |_(_) |                                                                         
    | '_ \   | '_ \| | | | / __| '_ \| | __| | |                                                                         
    | |_) |  | |_) | |_| | \__ \ | | | | |_| | |                                                                         
    |_.__(_) | .__/ \__, | |___/_| |_|_|\__|_|_|                                                                         
             |_|    |___/                                                                                                
    ;                                                                                                                    
                                                                                                                         
    %utl_submit_py64('                                                                                                   
    import shutil;                                                                                                       
    shutil.make_archive("d:/zip/fyls", "zip", "d:/txt");                                                                 
    ');                                                                                                                  
                                                                                                                         
