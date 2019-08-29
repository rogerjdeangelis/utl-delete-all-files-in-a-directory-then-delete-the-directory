# utl-delete-all-files-in-a-directory-then-delete-the-directory
Delete all files in a directory then delete the directory      
    Delete all files in a directory then delete the directory                                                      
                                                                                                                   
    github                                                                                                         
    https://tinyurl.com/y5wjjjgn                                                                                   
    https://github.com/rogerjdeangelis/utl-delete-all-files-in-a-directory-then-delete-the-directory               
                                                                                                                   
    SAS forum                                                                                                      
    https://tinyurl.com/yyvln2rs                                                                                   
    https://communities.sas.com/t5/SAS-Programming/delete-a-folder-directory-and-all-files-on-it/m-p/584870        
                                                                                                                   
                                                                                                                   
    *_                   _                                                                                         
    (_)_ __  _ __  _   _| |_                                                                                       
    | | '_ \| '_ \| | | | __|                                                                                      
    | | | | | |_) | |_| | |_                                                                                       
    |_|_| |_| .__/ \__,_|\__|                                                                                      
            |_|                                                                                                    
    ;                                                                                                              
                                                                                                                   
    * ceate a directory and some files;                                                                            
    data _null_;                                                                                                   
                                                                                                                   
      * create directory;                                                                                          
      if _n_=0 then do;                                                                                            
          %let rc=%sysfunc(dosubl('                                                                                
             data _null_;                                                                                          
                 rc=dcreate("hom","d:/");                                                                          
             run;quit;                                                                                             
         '));                                                                                                      
      end;                                                                                                         
                                                                                                                   
      file "d:/hom/file1.hom"; put "file1";                                                                        
      file "d:/hom/file2.hom"; put "file2";                                                                        
      file "d:/hom/file3.hom"; put "file3";                                                                        
                                                                                                                   
    run;quit;                                                                                                      
                                                                                                                   
     d:/hom                                                                                                        
       /file1.hom                                                                                                  
       /file2.hom                                                                                                  
       /file3.hom                                                                                                  
                                                                                                                   
    *            _               _                                                                                 
      ___  _   _| |_ _ __  _   _| |_                                                                               
     / _ \| | | | __| '_ \| | | | __|                                                                              
    | (_) | |_| | |_| |_) | |_| | |_                                                                               
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                              
                    |_|                                                                                            
    ;                                                                                                              
                                                                                                                   
    no files and no directory                                                                                      
                                                                                                                   
    *                                                                                                              
     _ __  _ __ ___   ___ ___  ___ ___                                                                             
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                            
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                            
    | .__/|_|  \___/ \___\___||___/___/                                                                            
    |_|                                                                                                            
    ;                                                                                                              
                                                                                                                   
                                                                                                                   
    %macro utl_delfiles(folder)/des="Delete empty folders";                                                        
          filename filelist "&folder";                                                                             
          data _null_;                                                                                             
             dir_id = dopen('filelist');                                                                           
             total_members = dnum(dir_id);                                                                         
             do i = 1 to total_members;  /* walk through all the files in the folder */                            
                member_name = dread(dir_id,i);                                                                     
                file_id = mopen(dir_id,member_name,'i',0);                                                         
                if file_id > 0 then do; /* if the file is readable */                                              
                   freadrc = fread(file_id);                                                                       
                      rc = fclose(file_id);                                                                        
                      rc = filename('delete',member_name,,,'filelist');                                            
                      rc = fdelete('delete');                                                                      
                end;                                                                                               
                rc = fclose(file_id);                                                                              
             end;                                                                                                  
             rc = fdelete('dir_id');                                                                               
             rc = dclose(dir_id);                                                                                  
          run;                                                                                                     
    %mend utl_delfiles;                                                                                            
                                                                                                                   
    %utl_delfiles(d:/hom);                                                                                         
                                                                                                                   
                                                                                                                   
