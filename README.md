# TokenTactics
Azure JSON Web Token ("JWT")Token Manipulation Toolset


Azure JWT's allow you to authenticate to certain endpoints as the user who signed in with the device code. Even if they used multi-factor authentication. Once you have a user's JWT, it may be possible to access certain apps such as Outlook, SharePoint, OneDrive, MSTeams and more. 

For instance, if you have a Graph or MSGraph token, you can then connect to Azure and dump users, groups, etc. You could then, depending on conditional access policies, switch to an Azure Core Management token and run [AzureHound](https://github.com/BloodHoundAD/AzureHound). Then, switch to an Outlook token and read/send emails! 

There are some example requests to endpoints in the resources folder.

You may also use these tokens with [AAD Internals](https://o365blog.com/aadinternals/) as well.

## Installation and Usage

```Import-Module .\TokenTactics.psd1```

```Get-Help Get-Azure-Token```

```RefreshTo-SubstrateToken```

### Generate Device Code

```Get-AzureToken -Client MSGraph```
Once the user has logged in, you'll be presented with the JWT and it will be saved in the $response variable. To access the access token use ```$response.access_token``` from your PowerShell window to display the token. You may also display the refresh token with ```$response.refresh_token```. Hint: You'll want the refresh token to keep refreshing to new tokens!

#### DOD/Mil Device Code
```Get-AzureToken -Client DODMSGraph```

### Refresh or Switch Tokens

```RefreshTo-OutlookToken -domain myclient.org -refreshToken ey..```

```$OutlookToken.access_token```

### Connect
```Connect-AzureAD -AadAccessToken $response.access_token -AccountId user@myclient.org```

### Commands
```powershell
Get-Command -Module TokenTactics

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Function        Dump-OWAMailboxViaMSGraphApi                       0.0.1      TokenTactics
Function        Forge-UserAgent                                    0.0.1      TokenTactics
Function        Get-AzureToken                                     0.0.1      TokenTactics
Function        Get-TenantID                                       0.0.1      TokenTactics
Function        Open-OWAMailboxInBrowser                           0.0.1      TokenTactics
Function        Parse-JWTtoken                                     0.0.1      TokenTactics
Function        RefreshTo-AzureCoreManagementToken                 0.0.1      TokenTactics
Function        RefreshTo-AzureManagementToken                     0.0.1      TokenTactics
Function        RefreshTo-DODMSGraphToken                          0.0.1      TokenTactics
Function        RefreshTo-GraphToken                               0.0.1      TokenTactics
Function        RefreshTo-MAMToken                                 0.0.1      TokenTactics
Function        RefreshTo-ManageOfficeToken                        0.0.1      TokenTactics
Function        RefreshTo-MSGraphToken                             0.0.1      TokenTactics
Function        RefreshTo-MSManageToken                            0.0.1      TokenTactics
Function        RefreshTo-MSTeamsToken                             0.0.1      TokenTactics
Function        RefreshTo-OfficeAppsToken                          0.0.1      TokenTactics
Function        RefreshTo-OutlookToken                             0.0.1      TokenTactics
Function        RefreshTo-SubstrateToken                           0.0.1      TokenTactics
```

## Authors and contributors
- [@0xBoku](https://github.com/boku7) co-author and researcher.

TokenTactic's methods are highly influenced by the great research of Dr Nestori Syynimaa at https://o365blog.com/.

