---
layout: post
title:  "My First Open Source Contribution - Part 1"
date:   2018-09-22 09:56:31 +0100
---

Yesterday was a big day for me, inspired by the talk by Maggie Pint Monday, at Microsoft's Leopardstown campus, I took another look at contributing to an open source project. I know PowerShell and so surely there is something I can help with. The talk by Maggie informed me of a practice among the open source community of tagging entry level issues as "up-for-grabs" so I search GitHub for "up-for-grabs"+"PowerShell" and obviously I got 100's of hits. I eventually came across a project that I recognised, JiraPS, we use the Atlassian stack in work and I'm familiar with the Jira APIs because I've written personal functions to speed up our Sprint Planning and Refinement ceremonies.

This is a project would worth further inspection, I browsed the [JiraPS Issues](https://github.com/AtlassianPS/JiraPS/issues/) for up-for-grabs issues and found [JiraPS Issue-229](https://github.com/AtlassianPS/JiraPS/issues/229). I know my way around PowerShell objects, so this one seems doable. I decided to have a go because what have I got to lose, it is Friday night and my wife is out at a fashion show. I read the [contributions](https://atlassianps.org/docs/Contributing/) guide and see that they want me to fork the repo to work locally – no problem, let’s get into this.
This issue details expected behaviour, so I started there and tried to replicate it to see what isn’t working.

```powershell
PS C:\JiraPS> "project,summary,assignee" > "./data.csv"
PS C:\JiraPS> "CS,Some Title,admin" >> "./data.csv"
PS C:\JiraPS> import-csv "./data.csv" | New-JiraIssue
cmdlet New-JiraIssue at command pipeline position 2
Supply values for the following parameters:
```

Ok so it's clear from this test that the function isn't expecting to take the parameters from the pipeline, but that can be fixed with the addition of the parameter attribute.

```powershell
    Param (
        [parameter(ValueFromPipeline=$True)]
        [string[]]$Project
    )
```

or actually: 

```powershell
    Param (
        [parameter(ValueFromPipelineByPropertyName=$True)]
        [string[]]$Project
    )
```

So lets add that and see what I get.

```powershell
PS C:\JiraPS> import-csv "./data.csv" | New-JiraIssue
cmdlet New-JiraIssue at command pipeline position 2
Supply values for the following parameters:
IssueType:
```

Progress, it accepted the mandatory parameter, so let's complete the change and add it to the rest of the input parameters. It can't be this easy.

```powershell
PS C:\JiraPS> import-csv "./data.csv" | New-JiraIssue
Get-JiraConfigServer : The term 'Get-JiraConfigServer' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
At C:\JiraPS\JiraPS\Public\New-JiraIssue.ps1:50 char:19
+         $server = Get-JiraConfigServer -ErrorAction Stop -Debug:$fals ...
+                   ~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Get-JiraConfigServer:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
```

So, what is going on? It is understandable that the function failed to run as I am testing in isolation without the whole module loaded, it is accepting the input for the mandatory parameters.
I added a **write-host** into the function to see print out the $project variable and a break to exit the function because this fix isn’t really concerned with the actual function.
    begin {
        Write-Verbose "[$($MyInvocation.MyCommand.Name)] Function started"

        Write-Host $Project
        break

Running this produced the following:

```powershell
PS C:\JiraPS> import-csv "./data.csv" | New-JiraIssue -Verbose
VERBOSE: [New-JiraIssue] Function started

PS C:\JiraPS\>
```

This is very strange the variable is accepted but not accessible to print/use, I found my answer [here]( https://learn-powershell.net/2013/05/07/tips-on-implementing-pipeline-support/). I opened up another PowerShell session and played around with the numbers examples. 

```powershell
Function Get-Something {
    [cmdletbinding()]
    Param (
        [parameter(ValueFromPipeline=$True)]
        [string[]]$numbers
    )
    Begin {
        Write-Verbose "Initialize stuff in Begin block"
    }

    Process {
        Write-Verbose "Stuff in Process block to perform"
        $numbers
    }

    End {
        Write-Verbose "Final work in End block"
    }
}
PS C:\> 1,2,3 | Get-Something
1
2
3
PS C:\>
```

Versus the following with the variable in the **Begin** block.

```powershell
Function Get-Something {
    [cmdletbinding()]
    Param (
        [parameter(ValueFromPipeline=$True)]
        [string[]]$numbers
    )
    Begin {
        Write-Verbose "Initialize stuff in Begin block"
        $numbers
    }

    Process {
        Write-Verbose "Stuff in Process block to perform"
    }

    End {
        Write-Verbose "Final work in End block"
    }
}
PS C:\> 1,2,3 | Get-Something -verbose
VERBOSE: Initialize stuff in Begin block
VERBOSE: Stuff in Process block to perform
VERBOSE: Stuff in Process block to perform
VERBOSE: Stuff in Process block to perform
VERBOSE: Final work in End block
PS C:\>
```

That’s it, the variable is being accepted but is inaccessible in the **Begin** block. It makes sense after being slapped in the face with it, how can you process $variable1 in begin block when it only runs once? What would you do with $variable2? Exaclty.
With the problem figured out I wondered what to do about it, do I just tell the JiraPS people that it can’t be done with the code the way it is written? I don’t know I’m new to this, I’ll be honest I started writing a reply to the Issue, but then to try fix it instead. Let me go back to the code and look for a solution not just point out the problem.
I wondered could it be this is easy, the problem is the begin block, why not move the code out of the begin block = done. Thinking back to the numbers example above, If I need to do whatever is in the begin block that references an input variable, then I’ll need to do it for each object piped into the function. The aim here is to be able to generate an input object of one or many new issues and then pipe them into the function for processing.

```powershell
    begin {
        Write-Verbose "[$($MyInvocation.MyCommand.Name)] Function started"

        $server = Get-JiraConfigServer -ErrorAction Stop -Debug:$false

        $createmeta = Get-JiraIssueCreateMetadata -Project $Project -IssueType $IssueType -Credential $Credential -ErrorAction Stop -Debug:$false

        $resourceURi = "$server/rest/api/latest/issue"
    }
```

You can see where this is going without knowing much about the rest of the project, if you need createmeta once you need it everytime. I made the change saved the code, next I need a Pull Request. Read how to [submit a PR](https://atlassianps.org/docs/Contributing/submitting-a-pr.html).
Oh crap I made my changes on a branch from Master, quickly I checkout the Develop branch and branch off from there, re-implement my changes/fix and push to my fork of the project.
GitHub takes over from here, it offers a shortcut to create the PR back into the parent project. So I do, I fill start to fill in the form, crap again **I’ve not done any testing**.