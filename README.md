# Deploying Web Jobs With VSTS

This project details how to create a classic .Net Framework Web Job In Visual Studio and deployment it using Visual Studio Online.

## Create a New App Service in  Azure

* Create a new app service in Azure to host your web job.  We will deploy the web job we are about to create here.

## Creating the web job project

1. In Visual Studio 2017, create a new web job project:

    `new project->Cloud->Azure WebJob(.Net Framework)`

2. Update Nuget Packages

## Creating the VSTS Build Pipeline

Create a new build pipeline and use the Desktop App Template

On the `Build Solution` task set the MSBuild Arguments to:

```bash
/p:DeployOnBuild=true /p:WebPublishMethod=Package /p:PackageAsSingleFile=true /p:SkipInvalidConfigurations=true /p:PackageLocation="$(build.artifactstagingdirectory)\\"
```

On the `Copy Files` task

1. The `Source folder` should be `$(system.defaultworkingdirectory)`  (this is the default value)
2. The `Contents` should be `**\bin\$(BuildConfiguration)\**`  (this is the default value)
3. Change the `Target Folder` to be`$(build.artifactstagingdirectory)\WebJobTest\App_Data\jobs\continuous\WebJobTest `



## Creating the VSTS Release Pipeline

1. Create an `Deploy Azure App Service Task`
2. Change the `Package or Folder` to `$(System.DefaultWorkingDirectory)/_clippingsiowebapi-.NET Desktop-CI (2)/drop/WebJobTest`
3. 



