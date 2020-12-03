# Description

Generates STS token for cross account with MFA and update the local AWS credential.

## PSGallery Url

Download this module from PowerShell Gallery via below Url
<https://www.powershellgallery.com/packages/AWSMFAProfile>

### Example 1

```powershell
Set-AWSCredential -AccessKey <YOURACCESSKEY> -SecretKey <YOURSECRETKEY>
Set-AWSMFAProfile -DeviceARN "arn:aws:iam::123456789123:mfa/johndoe@contoso.com" -SessionName "john" -StoreAs "NorthWindTraders" -RoleARN "arn:aws:iam::9876543219876:role/CrossAccountRole" -MFAToken 123456
Get-EC2Instance -ProfileName "NorthWindTraders" -Region "ap-southeast-2"
```

1. The defualt credential is defined.
2. Cross account access to "NorthWindTraders (9876543219876)" with "CrossAccountRole" assumed role and stored under "NorthWindTraders" profile name.
3. Retrieve EC2 instances from "NorthWindTraders" account.

### Example 2

```powershell
Set-AWSCredential -AccessKey <YOURACCESSKEY> -SecretKey <YOURSECRETKEY> -StoreAs "Contoso"
Set-AWSMFAProfile -DeviceARN "arn:aws:iam::123456789123:mfa/johndoe@contoso.com" -SessionName "john" -StoreAs "NorthWindTraders" -RoleARN "arn:aws:iam::9876543219876:role/CrossAccountRole" -ParentProfile "Contoso" -Duration 25200 -MFAToken 123456
Get-EC2Instance -ProfileName "NorthWindTraders" -Region "ap-southeast-2"
```

1. Set "Contoso" profile name as parent/master account which used to login to AWS.
2. Cross account access to "NorthWindTraders (9876543219876)" with "CrossAccountRole" assumed role and stored under "NorthWindTraders" profile name by using "Contoso" as parent/master profile where the session is expired after 7 hours.
3. Retrieve EC2 instances from "NorthWindTraders" account.
