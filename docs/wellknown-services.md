# Well-known services

## RDP (3389)
Ways to investigate this service:

- Connect with known credentials against this service. Be careful, you could lock out accounts.
- Execute RDP-specific nmap scripts to detect CVE's.

Tools: rdp_check.py from impacket. This script tests whether an account is valid on the target host attempting to reach CredSSP auth.

Not much to do here.

```
 python rdp_check.py HOMENETEU\KuiperM:PASS@wserv21
```

Connect via Windows terminal or just trough RDP client GUI
Tools: FreeRDP
Check if your own account has access

```
    mstsc /v:10.10.19.2
```

## WinRM (5985,5986)
Windows Remote Management (WinRM) is a Microsoft protocol that allows remote management of Windows machines over HTTP(S) using SOAP. On the backend it's utilising WMI, so you can think of it as an HTTP based API for WMI.

If WinRM is enabled on the machine, it's trivial to remotely administer the machine from PowerShell. In fact, you can just drop in to a remote PowerShell session on the machine (as if you were using SSH!)

```
    Test-WSMan -computername prete92382
    Invoke-Command -computername prete92382.eu.rabonet.com -ScriptBlock {ipconfig /all}

    $User = "Domain01\User01"
    $PWord = Read-Host -Prompt 'Enter a Password' -AsSecureString
    $Credential = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $User, $PWord
    Enter-PSSession -ComputerName bxts131565.eu.rabonet.com -Credential $Credential
```

Brute-forcing winrm could block users. 