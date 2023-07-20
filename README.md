# JetBrains ReSharper InspectCode GitHub Action

C# static analysis on GitHub Actions using JetBrains ReSharper InspectCode.

[![official JetBrains project](https://jb.gg/badges/official-flat-square.svg)](https://confluence.jetbrains.com/display/ALL/JetBrains+on+GitHub)

## Usage

```yml
name: InspectCode

on:
  push:
    branches:
      - main
      - 'releases/*'
  pull_request:
    types: [opened, reopened]
  workflow_dispatch:
  
jobs:
  inspect-code:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: recursive

      - name: Annotate
        # You may pin to the exact commit or the version.
        uses: JetBrains/ReSharper-InspectCode@v0.2
        with:
          solution: ./YourSolution.sln

    permissions:
      security-events: write
```

## Configuration

Use [`with`](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idstepswith) to define any action parameters:
```yaml
with:
  tool-version: 2023.2.0-eap09
```
You can use GitHub Workflow editor to get a list of all supported inputs with descriptions. 
|Name                     |Description                                                                                                                                                                               |Default           |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|
|`settings`               |Path to the file to use custom settings from (default: Use R#'s solution shared settings if exists)                                                                                       |                  |
|`output`                 |Write inspections report to specified file                                                                                                                                                |results.sarif.json|
|`format`                 |Write inspections report in specified format [Xml, Html, Text, Sarif]                                                                                                                     |Sarif             |
|`jobs`                   |Run up to N jobs in parallel. 0 means as many as possible                                                                                                                                 |0                 |
|`absolute-paths`         |Use absolute paths in inspections report                                                                                                                                                  |False             |
|`no-swea`                |Force disable solution-wide analysis                                                                                                                                                      |False             |
|`swea`                   |Force enable solution-wide analysis                                                                                                                                                       |False             |
|`project`                |Analyze only projects selected by provided wildcards (default: analyze all projects in solution)                                                                                          |                  |
|`include`                |Analyze only files selected by provided wildcards (default: analyze all files in solution)                                                                                                |                  |
|`exclude`                |Exclude files selected by provided wildcards from analysis (default: analyze all files in solution)                                                                                       |                  |
|`dumpIssuesTypes`        |Dump issues types                                                                                                                                                                         |False             |
|`sEverity`               |Minimal severity level to report [INFO, HINT, SUGGESTION, WARNING, ERROR]                                                                                                                 |SUGGESTION        |
|`debug`                  |Show debugging messages                                                                                                                                                                   |False             |
|`verbosity`              |Display this amount of information [OFF, FATAL, ERROR, WARN, INFO, VERBOSE, TRACE]                                                                                                        |INFO              |
|`help`                   |Show help and exit                                                                                                                                                                        |                  |
|`version`                |Show tool version and exit                                                                                                                                                                |                  |
|`toolset`                |MsBuild toolset version. Highest available is used by default. Example: --toolset=12.0                                                                                                    |                  |
|`toolset-path`           |MsBuild toolset (exe/dll) path. Example: --toolset-path=/usr/local/msbuild/bin/current/MSBuild.exe                                                                                        |                  |
|`mono`                   |Mono path. Empty to ignore Mono. Not specified for autodetect. Example: --mono=/Library/Frameworks/Mono.framework/Versions/Current/bin/mono                                               |                  |
|`dotnetcore`             |.NET Core path. Empty to ignore .NET Core. Not specified for autodetect. Example: --dotnetcore=/usr/local/share/dotnet/dotnet                                                             |                  |
|`dotnetcoresdk`          |.NET Core SDK version. Example: --dotnetcoresdk=3.0.100                                                                                                                                   |                  |
|`disable-settings-layers`|Disable specified settings layers. Possible values: GlobalAll, GlobalPerProduct, SolutionShared, SolutionPersonal, ProjectShared, ProjectPersonal                                         |                  |
|`no-buildin-settings`    |Suppress global, solution and project settings profile usage. Alias for --disable-settings-layers:GlobalAll;GlobalPerProduct;SolutionShared;SolutionPersonal;ProjectShared;ProjectPersonal|False             |
|`caches-home`            |Path to the directory where produced caches will be stored                                                                                                                                |                  |
|`properties`             |MSBuild properties                                                                                                                                                                        |                  |
|`targets-for-references` |MSBuild targets. These targets will be executed to get referenced assemblies of projects.                                                                                                 |                  |
|`targets-for-items`      |MSBuild targets. These targets will be executed to get other items (e.g. Compile item) of projects.                                                                                       |                  |
|`eXtensions`             |Install and use specified extensions                                                                                                                                                      |                  |
|`source`                 |Install extensions from specified source(s)                                                                                                                                               |                  |
|`measure`                |Measure own tool's performance [MEMORY, SAMPLING, TIMELINE]                                                                                                                               |                  |
|`no-build`               |Do not build solution before processing                                                                                                                                                   |False             |
|`build`                  |Build solution before processing                                                                                                                                                          |True              |
|`target`                 |MsBuild target to execute before processing.                                                                                                                                              |Build             |
|`telemetry-optout`       |Opt out from telemetry                                                                                                                                                                    |                  |
|`solution`               |Solution file                                                                                                                                                                             |                  |
|`tool-version`           |Tool Version                                                                                                                                                                              |2023.2-EAP5D      |
