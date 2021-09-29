Trying to create a PowerShell Script that takes a pipeline variable.

I understand the basics of begin...process...end and that they have to either exist at the script or function level.

But what I am trying to do is pass an array to a script that passes that array to a function that contains the begin...process...end

Here is the example<br>
From the command line: <code>@("test","test2","Test3") | .\testfilesearch.ps1</code>
However, if I do <code>.\testfilesearch.ps1 -testvalues @("test","test2","Test3")</code> that works, but I need to get info from a file or get-adcomputer.

The script has the following
```
  [cmdletbinding()]
param(
    [parameter(
        Mandatory = $true,
        ValueFromPipeline = $true)]
    $testvalues
)  


function writedata  {
    [cmdletbinding()]
    param(
        [parameter(
            Mandatory = $true,
            ValueFromPipeline = $true)]
        $pipelineInput
    )
    Begin {}
    
    Process {
        #I've tried with and without the ForEach loop
        ForEach ($input in $pipelineInput) {
            write-host "$input"
        }
    }
    End {}
}

#I've tried each of these combinations
#writedata $testvalues
#$testvalues | writedata
<#foreach ($dataval in $testvalues) {
    writedata $dataval
}#>
```
