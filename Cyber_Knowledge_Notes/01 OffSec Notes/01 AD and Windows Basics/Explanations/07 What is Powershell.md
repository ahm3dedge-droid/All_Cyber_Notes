# **Powershell**

Powershell is basically a Windows Component which allows us to interact and perform various tasks on a windows machine and an Active Directory Environment.

It is based on .NET framework.

it comes pre installed on windows machines so it is very useful to take advantage of pre installed things.

as an attacker it helps us to query information in an Active Directory Environment.

### **Powershell Help**

we can use `Get-Help` to see manual for Powershell commands

Get Help for all command lets

```
Get-Help *
```

Search for any thing with get-help

```
Get-Help <any_topic>
```
## Total 4 language Modes in Powershell

1. Full Language
2. Restricted Language
3. Constrained Laguage
4. No Language

**# See your Current Language Mode**

Command:

```
$ExecutionContext.SessionState.LanguageMode
```
____

_Refference:_ _[https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_language_modes?view=powershell-7.](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_language_modes?view=powershell-7.4)_[4](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_language_modes?view=powershell-7.4)

---
download a file from server and write an output file with this powershell command
```
iwr http://10.150.74.10:80/scripts/scripts.zip -OutFile scripts.zip
```
---
unzip a file in powershell, Uncompress a file
```
Expand-Archive -Path "C:\path\to\file.zip" -DestinationPath "C:\path\to\folder"
```
---
