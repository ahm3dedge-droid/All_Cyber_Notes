## 1️⃣ Local → Remote (Upload)

##### Single file
```
scp /local/path/file.txt user@REMOTE_IP:/remote/path/
```

##### Entire directory (recursive)
```
scp -r /local/path/directory/ user@REMOTE_IP:/remote/path/
```

---

## 2️⃣ Remote → Local (Download)

##### Single file
```
scp user@REMOTE_IP:/remote/path/file.txt /local/path/
```

##### Entire directory (recursive)
```
scp -r user@REMOTE_IP:/remote/path/directory/ /local/path/
```

---

## Common useful options (recommended)
custom SSH port
```
-P 2222
```        
enable compression
```
-C
```              
verbose (debug)
```
-v
```

##### Example with options
```
scp -P 2222 -C user@REMOTE_IP:/remote/path/file.txt /local/path/
```

---

## Windows-specific notes

### From **Linux → Windows**

Windows OpenSSH default path:
```
scp file.txt user@WINDOWS_IP:/c/Users/USERNAME/Desktop/
```

### From **Windows → Linux** (CMD / PowerShell)
```
scp C:\Users\USERNAME\Desktop\file.txt user@LINUX_IP:/home/user/
```

---

## Quick reference (one-glance)

| Direction      | Command                     |
| -------------- | --------------------------- |
| Local → Remote | `scp file user@ip:/path/`   |
| Remote → Local | `scp user@ip:/path/file ./` |
| Directory      | add `-r`                    |
| Custom port    | add `-P`                    |

---
