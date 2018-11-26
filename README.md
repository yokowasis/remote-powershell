*This is the [Source](https://superuser.com/questions/332381/windows-equivalent-of-ssh-how-to-connect-to-a-remote-machine-and-access-comman/1086581)*

# Server

First, enable the WINRM service (the windows application that processes remote commands) on the SERVER.
On the server computer, open PowerShell and run:

```
Enable-PSRemoting -Force
```

There is also other way of doing this. You can open a command prompt and run:

```
winrm -quickconfig
```

There could be much more configurations to change. No need for now.

# Client

On the CLIENT computer enable the WINRM service. The procedure is similar to what we've done for server above. Just run the command:

```
Enable-PSRemoting -Force
```

Then run on the CLIENT computer in PowerShell:

```
Set-Item wsman:\localhost\client\trustedhosts *
```

Which means that the client will trust all servers (hosts). Finally, run this (on the CLIENT again I emphasize):

```
Restart-Service WinRM
```

You are ready to go. Check rest of Shanteva's answer. On the CLIENT computer, run for instance:

```
Enter-PSSession -ComputerName 12.34.56.78 -Credential Administrator
```

It will ask for a password and the remote console opens which looks like:

```
[12.34.56.78]: PS C:\Users\Administrator\Documents>
```


### Finish
