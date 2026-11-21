[Azure Blob Storage Misconfigurations: Attacker’s Gateway to Data | by Avyukt Security | InfoSec Write-ups](https://infosecwriteups.com/azure-blob-storage-misconfigurations-attackers-gateway-to-data-b7d8e957440e)

so here 1st i looked up this article and configured the tool

## Steps to setup the Microburst:
1. download the GitHub Zip and unzip
2. install the required modules **AZ**, **Azure**, **MSOnline** with the below commands

```
Install-Module AZ
```
```
Install-Module Azure
```
3. Now open the Powershell and locate the, Module File **MicroBurst.psm1**, 
Now import the Module

```
Import-Module .\MicroBurst.psm1
```

4. Use the below command to check the Existence. 
5. Now use the command below to enumerate the Blob Storage.

```
Invoke-EnumerateAzureBlobs -Base {TARGET_HERE}
```

- actually we need to type the *company name* or *target name* after the **-Base** flag to let the tool find Storage Accounts.
- we can also add custom keywords in the Permutations "\MicroBurst-master\Misc\permutations.txt"

if we want to use custom permutations, this is the command to use

```
Invoke-EnumerateAzureBlobs -Base {TARGET_HERE} -Permutations .\Misc\permutations-v2.txt
```
