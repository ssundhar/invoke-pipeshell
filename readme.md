# Invoke-PipeShell

This script demonstrates a remote command shell running over an SMB Named Pipe
The shell is interactive PowerShell or single PowerShell commands

## Parameters

    .PARAMETER Mode
        Client or Server
    .PARAMETER Server
        Hostname of Server
    .PARAMETER AESKey
        16 character key used for encryption
    .PARAMETER Pipe
        Name of server's named pipe
    .PARAMETER Timeout
        Time in milliseconds a client will consider a server unreachable
    .PARAMETER i
        Use interactive shell.  If false, a single command will be issued from the -c parameter
    .PARAMETER c
        command to run in non-interactive mode  

## Examples

### Server

Host the Named Pipe shell.  Commands are executed here.

    Import-Module .\Invoke-PipeShell.ps1; Invoke-PipeShell -mode server -aeskey PmsqQUt2PoYMFNq7 -pipe tapsrv.5604.1234

### Client

Connects to the server.  Issues commands to server and displays results.

#### Interactive Client

    Import-Module .\Invoke-PipeShell.ps1; Invoke-PipeShell -mode client -server localhost -aeskey PmsqQUt2PoYMFNq7 -pipe tapsrv.5604.1234 -i

    SHELL: ls
    
    Directory: C:\Users\user\Documents

    Mode                LastWriteTime     Length Name
    ----                -------------     ------ ----
    d----         3/21/2016   3:28 PM            files
    
    SHELL: pwd
    
    Path
    ----
    C:\Users\user\Documents


#### Non-interactive client

    Import-Module .\Invoke-PipeShell.ps1; Invoke-PipeShell -mode client -server localhost -aeskey PmsqQUt2PoYMFNq7 -pipe tapsrv.5604.1234 -c ls

    Directory: C:\Users\user\Documents
      
    Mode                LastWriteTime     Length Name
    ----                -------------     ------ ----
    d----         3/21/2016   3:28 PM            files


#### Extra commands
    ----------------
    leave - exits client, leaves server running
    kill - kill server and client