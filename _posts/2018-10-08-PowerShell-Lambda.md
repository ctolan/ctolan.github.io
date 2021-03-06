---
layout: post
title:  "Getting Started with PowerShell AWS Lambda"
date:   2018-10-08 09:56:31 +0100
tags: PowerShell Lambda
author:
  twitter: ConorT
---

A month ago now [AWS announced Lambda support for PowerShell Core](https://aws.amazon.com/blogs/developer/announcing-lambda-support-for-powershell-core/), this is awesome and something I am certainly going to learn to use. PowerShell is my go to language in work but when I move to web platforms PowerShell seems so far away. Hopefully these Lambda’s will be able to bridge writing in my native tongue while away from home.

First things first, I’ll want to setup Visual Studio Code for PowerShell Core not PowerShell v5.1 that I’m currently running. I grabbed the [latest PowerShell release here](https://github.com/PowerShell/PowerShell/releases) and installed it. I also downloaded the [.NET 2.1 Core SDK](https://www.microsoft.com/net/download) because it is used for uploading to Lambda. Lastly I need to install the new [AWS Lambda PSCore module](https://www.powershellgallery.com/packages/AWSLambdaPSCore/1.1.0.0)

![PWSH AWS Lambda Module Install Image]({{ site.url }}/images/PWSH-AWS-Lambda-1-min.PNG)

```powershell
PS > Install-Module -Name AWSLambdaPSCore
Untrusted repository
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): A
PS > get-command –module AWSLambdaPSCore

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

Ok let us get to the code:

{% raw %}

```powershell
PS > New-AWSPowerShellLambda -ScriptName LambdaHello -Template Basic
WARNING: This script requires the AWSPowerShell.NetCore module which is not installed locally.
WARNING: To use the AWS CmdLets execute "Install-Module AWSPowerShell.NetCore" and then update the #Requires statement to the version installed. If you are not going to use the AWS CmdLets then remove the #Requires statement from the script.
Created new AWS Lambda PowerShell script LambdaHello.ps1 from template Basic at C:\LambdaHello
```

The basic template script is pretty empty, I set it to write-host "Hello World!" I did as instructed and installed AWSPowerShell.NetCore (but having completed this and looking back I know that for my basic HelloWorld I do not need this.)

```powershell
PS > Install-Module AWSPowerShell.NetCore

Untrusted repository
You are installing the modules from an untrusted repository. If you trust this repository, change its InstallationPolicy value by running the
Set-PSRepository cmdlet. Are you sure you want to install the modules from 'PSGallery'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): A
```

Now to try publish my HelloWorld Lambda with Publish-AWSPowerShellLambda cmdlet.

```powershell
PS >Publish-AWSPowerShellLambda -ScriptPath .\LambdaHello.ps1 -Name  HelloWorld -Region eu-west-1
Error retrieving configuration for function HelloWorld: The security token included in the request is invalid.
Error publishing PowerShell Lambda Function: -1
CALLSTACK:
Command                     Arguments
-------                     ---------
_deployProject
Publish-AWSPowerShellLambda {{Region=eu-west-1$null}, {Region=eu-west-1$null}, {Region=eu-west-1$null}, {Region=eu-we...
<ScriptBlock>               {{=$null}, {=$null}, {=$null}, {=$null}}
At C:\Program Files\PowerShell\Modules\AWSLambdaPSCore\1.1.0.0\Private\_DeploymentFunctions.ps1:194 char:13
+             throw $msg
+             ~~~~~~~~~~
+ CategoryInfo          : OperationStopped: (Error publishin...
:String) [], RuntimeException
+ FullyQualifiedErrorId : Error publishing PowerShell Lambda Function: -1
CALLSTACK:
Command                     Arguments
-------                     ---------
_deployProject
Publish-AWSPowerShellLambda {{Region=eu-west-1$null}, {Region=eu-west-1$null}, {Region=eu-west-1$null}, {Region=eu-we...
<ScriptBlock>               {{=$null}, {=$null}, {=$null}, {=$null}}
```

{% endraw %}

*Errors* Quick get back to Google.

I thought ok maybe I don't have everything necessary installed, I re-installed the AWS PowerShell module and would try to connect with those cmdlets to check if it is me or the new stuff.

```powershell
Install-Module -Name AWSPowerShell -AllowClobber
```

I used "-AllowClobber" because some of the cmdlets existed and it is a force install switch.

So by now i think i must all the necessary modules installed.

- PowerShell Core 6
- AWS PowerShell Lambda Module
- AWS PowerShell Module
- AWS PowerShell NetCore

Yet i still could not publish sucessfully.

I tried setting Environment variables for my AWS Access Key and AWS Secret Key, but this didn't work. It did set me on the right path checking the AWS PowerShell credentials connectivity, I looked [here](https://aws.amazon.com/blogs/developer/handling-credentials-with-aws-tools-for-windows-powershell/) for how to set/create a new AWS Credential via PowerShell.

```powershell
PS C:> Set-AWSCredentials -AccessKey 123MYACCESSKEY -SecretKey 456SECRETKEY -StoreAs myAWScreds
```

I was now able to list all AMI's on eu-west-1, but still not able publish my Lambda!

I gave up for the night and came back starting with again with Google, I
[found the answer](https://stackoverflow.com/questions/43195587/aws-powershell-use-stsrole-the-security-token-included-in-the-request-is-inval). When I listed the credentials in my session there were two.

```powershell
PS > Get-AWSCredentials -ListStoredCredentials
WARNING: The ListProfile switch is deprecated and will be removed from a future release.  Please use ListProfileDetail instead.
myAWScreds
default

PS > Remove-AWSCredentialProfile default

PS > Publish-AWSPowerShellLambda -ScriptPath .\LambdaHello.ps1 -Name  HelloWorld -Region eu-west-1
```

I removed the _default_ credential leaving only the one I created with the correct Key and secret it worked!

![PWSH Lambda Published Image]({{ site.url }}/images/PWSH-VSCode-3.PNG)

So now what? Back to the [AWS documentation](https://aws.amazon.com/blogs/developer/announcing-lambda-support-for-powershell-core/). I logged into the AWS console again and there is my function.

![AWS Lambda Published Image]({{ site.url }}/images/PowerShell-Lambda-AWS-1.PNG)

Looking around I spotted the Test button, so I created an empty test.
![AWS PowerSHell Lambda Works Image]({{ site.url }}/images/PowerShell-Lambda-AWS-test.PNG)

I executed the function from the main page once created and it works!
![AWS PowerSHell Lambda Works Image]({{ site.url }}/images/PowerShell-Lambda-AWS-Works.PNG)
