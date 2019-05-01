pipeline{
    agent any
    stages{
        stage('IISDetails'){
            steps{
              powershell 'echo "Running script to get iis details"'
              powershell '''
              Import-Module WebAdministration;

Write-Host "#####Getting Websites Hosted on the server######" -ForegroundColor Green;

get-website | select name,id,state,physicalpath,
@{n="Bindings"; e= { ($_.bindings | select -expa collection) -join ';' }} | format-table -AutoSize -wrap
#@{n="LogFile";e={ $_.logfile | select -expa directory}}, 
#@{n="attributes"; e={($_.attributes | % { $_.name + "=" + $_.value }) -join ";" }};

Write-Host "#####Getting App-pools Hosted on the server######" -ForegroundColor Green;

Get-ChildItem -Path IIS:\AppPools\ | Select-Object name, state, managedRuntimeVersion, managedPipelineMode, @{e={$_.processModel.username};l="username"}, <#@{e={$_.processModel.password};l="password"}, #> @{e={$_.processModel.identityType};l="identityType"}
format-table -AutoSize -wrap;

Write-Host "#####Getting WebApplications Hosted on the server######" -ForegroundColor Green;

Get-WebApplication;

              '''
            }
        }
    }
}
