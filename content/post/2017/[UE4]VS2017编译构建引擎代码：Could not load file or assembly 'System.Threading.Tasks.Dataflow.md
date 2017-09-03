---
title: "[UE4]VS2017编译构建引擎代码：Could not load file or assembly 'System.Threading.Tasks.Dataflow"
date: "2017-08-25T14:33:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

如果用VS2017编译构建引擎代码，在双击GenerateProjectFiles.bat时出现以下错误：

    Setting up Unreal Engine 4 project files...
    MSBUILD : error MSB1025: An internal failure occurred while running MSBuild.
    Microsoft.Build.Shared.InternalErrorException: MSB0001: Internal MSBuild Error: Throwing from logger shutdown
    =============
    System.IO.FileNotFoundException: Could not load file or assembly 'System.Threading.Tasks.Dataflow, Version=4.5.24.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies. The system cannot find the file specified.
    File name: 'System.Threading.Tasks.Dataflow, Version=4.5.24.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'
       at Microsoft.Build.BackEnd.Logging.LoggingService.ShutdownComponent()
       at Microsoft.Build.Evaluation.ProjectCollection.ShutDownLoggingService()

    WRN: Assembly binding logging is turned OFF.
    To enable assembly bind failure logging, set the registry value [HKLM\Software\Microsoft\Fusion!EnableLog] (DWORD) to 1.
    Note: There is some performance penalty associated with assembly bind failure logging.
    To turn this feature off, remove the registry value [HKLM\Software\Microsoft\Fusion!EnableLog].


     ---> System.IO.FileNotFoundException: Could not load file or assembly 'System.Threading.Tasks.Dataflow, Version=4.5.24.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies. The system cannot find the file specified.
       at Microsoft.Build.BackEnd.Logging.LoggingService.ShutdownComponent()
       at Microsoft.Build.Evaluation.ProjectCollection.ShutDownLoggingService()
       --- End of inner exception stack trace ---
       at Microsoft.Build.Shared.ErrorUtilities.ThrowInternalError(String message, Exception innerException, Object[] args)
       at Microsoft.Build.Evaluation.ProjectCollection.ShutDownLoggingService()
       at Microsoft.Build.Evaluation.ProjectCollection.Dispose(Boolean disposing)
       at Microsoft.Build.CommandLine.MSBuildApp.BuildProject(String projectFile, String[] targets, String toolsVersion, Dictionary`2 globalProperties, ILogger[] loggers, LoggerVerbosity verbosity, DistributedLoggerRecord[] distributedLoggerRecords, Boolean needToValidateProject, String schemaFile, Int32 cpuCount, Boolean enableNodeReuse, TextWriter preprocessWriter, Boolean debugger, Boolean detailedSummary)
       at Microsoft.Build.CommandLine.MSBuildApp.Execute(String commandLine)

    Unhandled Exception: Microsoft.Build.Shared.InternalErrorException: MSB0001: Internal MSBuild Error: Throwing from logger shutdown
    =============
    
原因：没有安装Microsoft Build Tools 2015，vs2017安装器没有包含这个工具，需要单独下载安装：    
https://www.microsoft.com/en-us/download/details.aspx?id=48159
