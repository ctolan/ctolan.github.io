---
layout: post
title:  "PowerShell AWS Lambdas"
date:   2018-10-08 09:56:31 +0100
---

A month ago now [AWS announced Lambda support for PowerShell Core](https://aws.amazon.com/blogs/developer/announcing-lambda-support-for-powershell-core/), this is awesome and something I am certainly going to learn to use. PowerShell is my go to language in work but when I move to web platforms PowerShell seems so far away. Hopefully these Lambda’s will be able to bridge writing in my native tongue while away from home.

First things first, I’ll want to setup Visual Studio Code for PowerShell Core not PowerShell v5.1 that I’m currently running. I grabbed the [latest PowerShell release here](https://github.com/PowerShell/PowerShell/releases) and installed it. I also downloaded the [.NET 2.1 Core SDK](https://www.microsoft.com/net/download) because it is used for uploading to Lambda. Lastly I need to install the new [AWS Lambda PSCore module](https://www.powershellgallery.com/packages/AWSLambdaPSCore/1.1.0.0)

![PWSH AWS Lambda Module Install Image]({{ site.url }}/images/PWSH-AWS-Lambda-1.PNG)

```powershell
PS C:\Program Files\PowerShell\6> Install-Module -Name AWSLambdaPSCore
Untrusted repository
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): A
PS C:\Program Files\PowerShell\6> get-command –module AWSLambdaPSCore

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Function        Get-AWSPowerShellLambdaTemplate                    1.1.0.0    AWSLambdaPSCore
Function        New-AWSPowerShellLambda                            1.1.0.0    AWSLambdaPSCore
Function        New-AWSPowerShellLambdaPackage                     1.1.0.0    AWSLambdaPSCore
Function        Publish-AWSPowerShellLambda                        1.1.0.0    AWSLambdaPSCore
```

All looks good to me.

Next up is setting Visual Studio Code to use PWSH in the terminal, I followed the guide by Ian Noble [found here](https://www.iannoble.co.uk/use-powershell-core-visual-studio-code/)

![PWSH VSCode Install Image]({{ site.url }}/images/PWSH-VSCode-2.PNG)

![PWSH VSCode Installed Image]({{ site.url }}/images/PWSH-VSCode-1.PNG)

Click the + if you do not see it the first time after a restart. I needed to acknowledge a security prompt the first time.