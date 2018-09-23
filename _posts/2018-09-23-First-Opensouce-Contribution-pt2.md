---
layout: post
title:  "My First Open Source Contribution - Part 2"
date:   2018-09-23 09:56:31 +0100
---

Picking up right where I left off yesterday **Crap again I’ve not do any testing**, I have come too far now not to keep going. I took a look at their [guide for writing tests](https://atlassianps.org/docs/Contributing/writing-tests.html). Come on seriously?

Ok well I will just have to figure it out, ah of course there is a Tests folder, and it contains New-JiraIssue.tests.ps1 and it is Pester, of course it is! Sweet I can do this.

The test looks well written, clear mocking of all the external function calls, phew that could have stopped me in my tracks because I really haven’t looked at the code of this function. I was only working with the parameters so far.
There is one behaviour test written already, so I’ll probably start here.

```powershell
        Context "Behavior testing" {
            It "Creates an issue in JIRA" {
                { New-JiraIssue @newParams } | Should Not Throw
                # The String in the ParameterFilter is made from the keywords
                # we should expect to see in the JSON that should be sent,
                # including the summary provided in the test call above.
                Assert-MockCalled -CommandName Invoke-JiraMethod -ModuleName JiraPS -Times 1 -Scope It -ParameterFilter { $Method -eq 'Post' -and $URI -like "$jiraServer/rest/api/*/issue" }
            }
        }
```

This is how the function is currently called and what I’ve changed adds a new way to feed the function from the pipeline. I wrote the following test reusing the rest of the already working code and mocking and parameters etc.

```powershell
            It "Creates an issue in JIRA from pipeline" {
                { $pipelineParams | New-JiraIssue } | Should Not Throw
                # The String in the ParameterFilter is made from the keywords
                # we should expect to see in the JSON that should be sent,
                # including the summary provided in the test call above.
                Assert-MockCalled -CommandName Invoke-JiraMethod -ModuleName JiraPS -Times 1 -Scope It -ParameterFilter { $Method -eq 'Post' -and $URI -like "$jiraServer/rest/api/*/issue" }
            }
```

Time to run the tests and see what happens.
![Tests Pass! image]({{ site.url }}/images/ Issue-229-Tests-Pass.PNG)
This is awesome, that’s my test passing – tick.

Ok documentation, do I need to write documentation? I guess I do, and there is Docs folder and there is already a New-JiraIssue helpfile, this is actually easier than I expected – the benefit of contributing to an existing project is that a lot of the work has already been done or there would be nothing to contribute to. I found the bit in the help file with the examples and copy paste changed to cover the new use case, my new functionality that I added to this project #satifaction. Documentation – tick.
Right it is getting late now and the end is in sight, I create the PR, [this PR]( https://github.com/AtlassianPS/JiraPS/pull/312). That’s me done, I leave it to the JiraPS team to review and I’ll see what happens.



