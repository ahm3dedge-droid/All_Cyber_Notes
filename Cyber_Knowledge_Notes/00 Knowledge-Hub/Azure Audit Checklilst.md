| No. | Control Area          | Simplified Requirement            | Purpose                               |
| --- | --------------------- | --------------------------------- | ------------------------------------- |
| 1   | Security Defaults     | Enable Azure AD security defaults | Apply baseline security automatically |
| 2   | MFA (Privileged)      | Enable MFA for all admins         | Protect high-privilege accounts       |
| 3   | MFA (Users)           | Enable MFA for all users          | Reduce account takeover risk          |
| 4   | MFA Remember          | Disable “remember MFA”            | Prevent MFA bypass                    |
| 5   | Trusted Locations     | Define trusted IP locations       | Apply location-based security         |
| 6   | Geo Blocking          | Block risky countries             | Prevent foreign attacks               |
| 7   | Admin MFA Policy      | Enforce MFA for admin groups      | Secure admin access                   |
| 8   | User MFA Policy       | Enforce MFA for all users         | Strengthen authentication             |
| 9   | Risky Sign-ins        | Require MFA for risky logins      | Stop compromised access               |
| 10  | Azure Management      | Require MFA for management access | Protect admin actions                 |
| 11  | Tenant Creation       | Restrict tenant creation          | Prevent unauthorized tenants          |
| 12  | Guest Access Review   | Review external users via PIM     | Control partner access                |
| 13  | Guest Review          | Review guest users regularly      | Remove inactive guests                |
| 14  | Password Reset        | Require 2-step verification       | Prevent account hijacking             |
| 15  | Password Policy       | Enforce custom banned passwords   | Block weak passwords                  |
| 16  | Auth Info Review      | Require re-confirmation           | Keep recovery info updated            |
| 17  | Reset Alerts (Users)  | Notify users on reset             | Detect unauthorized resets            |
| 18  | Reset Alerts (Admins) | Notify admins on reset            | Monitor admin activity                |
| 19  | App Consent           | Block user app consent            | Prevent risky apps                    |
| 20  | Verified Apps         | Allow verified publishers only    | Limit trusted apps                    |
| 21  | Gallery Apps          | Block self-added apps             | Protect user data                     |
| 22  | App Registration      | Restrict app registration         | Ensure app security review            |
| 23  | Guest Permissions     | Restrict guest access             | Prevent directory exposure            |
| 24  | Guest Invites         | Limit guest invitations           | Control external access               |
| 25  | Admin Portal          | Restrict admin portal             | Protect sensitive settings            |
| 26  | Group Features        | Disable group self-management     | Centralize control                    |
| 27  | Security Groups       | Block user-created groups         | Prevent misuse                        |
| 28  | Group Requests        | Disable owner approvals           | Prevent unauthorized changes          |
| 29  | M365 Groups           | Restrict group creation           | Control collaboration                 |
| 30  | Device Join MFA       | Require MFA for device join       | Prevent rogue devices                 |
| 31  | Admin Roles           | Remove custom admin roles         | Apply least privilege                 |
| 32  | Resource Locks        | Assign lock admin role            | Protect critical resources            |
| 33  | Subscription Moves    | Restrict directory movement       | Prevent subscription misuse           |
| 34  | Defender (Servers)    | Enable Defender for Servers       | Detect server threats                 |
| 35  | Defender (Apps)       | Enable Defender for Apps          | Protect web services                  |
| 36  | Defender (Databases)  | Enable Defender for DB servers    | Secure database systems               |
| 37  | Defender (SQL)        | Enable Defender for Azure SQL     | Protect cloud databases               |
| 38  | Defender (SQL VM)     | Enable Defender on machines       | Secure SQL servers                    |
| 39  | Defender (OSS DB)     | Enable for open-source DB         | Protect MySQL/PostgreSQL              |
| 40  | Defender (Storage)    | Enable Defender for Storage       | Detect data threats                   |
| 41  | Defender (Containers) | Enable Defender for containers    | Secure Kubernetes                     |
| 42  | Defender (Cosmos DB)  | Enable Cosmos DB protection       | Detect NoSQL attacks                  |
| 43  | Defender (Key Vault)  | Enable Key Vault monitoring       | Protect secrets                       |
| 44  | Defender (DNS)        | Enable DNS monitoring             | Detect malicious domains              |
| 45  | Defender (ARM)        | Enable Resource Manager defense   | Detect admin abuse                    |
| 46  | Patch Management      | Apply system updates              | Fix vulnerabilities                   |
| 47  | Security Policy       | Enable all ASC policies           | Maintain compliance                   |
| 48  | Log Analytics         | Auto-install agents               | Enable monitoring                     |
| 49  | Vulnerability Scan    | Enable VA auto-provisioning       | Detect weaknesses                     |
| 50  | Container Security    | Auto-enable container defense     | Secure workloads                      |
