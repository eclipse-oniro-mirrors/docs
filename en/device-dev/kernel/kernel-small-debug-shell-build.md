# Shell Command Programming Example

## Example Description<a name="section87143612316"></a>

This section describes how to add a shell command  **test**  using static registration and dynamic registration.

## Static Registration<a name="section1660495712314"></a>

Development process:

1.  Define the  **cmd\_test**  function to be called to add a command.

2.  Use the  **SHELLCMD\_ENTRY**  function to add the new command.

3.  Add a parameter to the  **liteos\_tables\_ldflags.mk**  link options for linking to the new command.

4.  Recompile the code and run it.


## Static Registration Programming Example<a name="section1233411684113"></a>

1.  Define the  **cmd\_test**  function to be called to add a command.

    ```
    #include "shell.h" 
    #include "shcmd.h"  
    int cmd_test(void) 
    {     
        printf("hello everybody!\n");     
        return 0; 
    }
    ```

2.  Add the new command.

    ```
    SHELLCMD_ENTRY(test_shellcmd, CMD_TYPE_EX, "test", 0, (CMD_CBK_FUNC)cmd_test);
    ```

3.  Add a parameter to the link options for linking to the new command.

    Add  **-utest\_shellcmd**  to the  **LITEOS\_TABLES\_LDFLAGS**  option in the  **liteos\_tables\_ldflags.mk**  file.

4.  Recompile the code.

    ```
    make clean;make
    ```

5.  Run the  **help**  command to view all the commands registered in the system.

    The command output contains the  **test**  command \(the following command output is for reference only.\)

    ```
    OHOS # help
    *******************shell commands:*************************
    
    arp           cat           cd            chgrp         chmod         chown         cp            cpup          
    date          dhclient      dmesg         dns           format        free          help          hwi           
    ifconfig      ipdebug       kill          log           ls            lsfd          memcheck      mkdir         
    mount         netstat       oom           partinfo      partition     ping          ping6         pwd           
    reset         rm            rmdir         sem           statfs        su            swtmr         sync          
    tftp          touch         umount        uname         test         systeminfo    task          telnet        
    watch         writeproc     
    ```


## Dynamic Registration<a name="section6804126192412"></a>

Development process:

1.  Use the  **osCmdReg**  function to add a new command.

2.  Recompile the code and run it.


## Dynamic Registration Programming Example<a name="section2335121613418"></a>

1.  Call the  **osCmdReg**  function from the  **app\_init**  function to dynamically register the command.

    ```
    #include "shell.h" 
    #include "shcmd.h"  
    int cmd_test(void) 
    {     
        printf("hello everybody!\n");     
        return 0; 
    }  
    void app_init(void) 
    {      
        ....      
        ....      
        osCmdReg(CMD_TYPE_EX, "test", 0,(CMD_CBK_FUNC)cmd_test);      
        .... 
    }
    ```

2.  Recompile the code.

    ```
    make clean;make
    ```

3.  Run the  **help**  command to view all the commands registered in the system.

    The command output contains the  **test**  command.

    ```
    OHOS # help
    *******************shell commands:*************************
    
    arp           cat           cd            chgrp         chmod         chown         cp            cpup          
    date          dhclient      dmesg         dns           format        free          help          hwi           
    ifconfig      ipdebug       kill          log           ls            lsfd          memcheck      mkdir         
    mount         netstat       oom           partinfo      partition     ping          ping6         pwd           
    reset         rm            rmdir         sem           statfs        su            swtmr         sync          
    tftp          touch         umount        uname         test          systeminfo    task          telnet        
    watch         writeproc     
    ```


