+++
title= "[UE4]Android package for engine source build"
date= "2017-12-19T19:20:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Android", "Build"]
+++


先设置NDK的环境变量：
https://docs.unrealengine.com/latest/INT/Platforms/Android/Reference/index.html#environmentvariables
{{< figure src="/img/20171219-[UE4]Android package for engine source build/[UE4]Android package for engine source build-01.jpg">}}


然后重新运行引擎源码根目录下的Setup.bat。此时会开始下载几百兆的内容，且Excluding没有出现Android字样，如果没有配置NDKROOT，Excluding会包含Android，表示下载内容排除android编译环境。
{{< figure src="/img/20171219-[UE4]Android package for engine source build/[UE4]Android package for engine source build-02.jpg">}}

如果不设置环境变量，也可以通过命令行Setup.bat --all来下载所有平台的编译文件（包括ios和linux）。

下载完成后，rebuild一下Development - Android
{{< figure src="/img/20171219-[UE4]Android package for engine source build/[UE4]Android package for engine source build-03.jpg">}}


##### 常见错误

如果不下载android的相关文件，编译安卓版本时可能出现以下错误：

错误1（出现这个错误的另一个原因是Project Settings的Android-SDK的NDK API Level修改了，UE4默认是android-19）：

	UATHelper: Packaging (Android (ASTC)):   clang++.exe: error: no such file or directory: 'C:/UnrealEngine-4.18.1-release/Engine/Build/Android/Prebuilt/bsdsignal/lib/armeabi-v7a/libbsdsignal.a'
	UATHelper: Packaging (Android (ASTC)):   Total build time: 899.04 seconds (Local executor: 890.45 seconds)
	UATHelper: Packaging (Android (ASTC)): Took 899.2723232s to run UnrealBuildTool.exe, ExitCode=5
	UATHelper: Packaging (Android (ASTC)): ERROR: Command failed (Result:5): C:\UnrealEngine-4.18.1-release\Engine\Binaries\DotNET\UnrealBuildTool.exe WarSoul Android Development -Project=G:\Source\Work\project2\ue4_proj\WarSoul\WarSoul.uproject  G:\Source\Work\project2\ue4_proj\WarSoul\WarSoul.uproject -NoUBTMakefiles  -remoteini="G:\Source\Work\project2\ue4_pr
	oj\WarSoul" -skipdeploy -noxge -NoHotReload -ignorejunk. See logfile for details: 'UnrealBuildTool-2017.12.18-17.10.06.txt' 
	UATHelper: Packaging (Android (ASTC)):        (see C:\UnrealEngine-4.18.1-release\Engine\Programs\AutomationTool\Saved\Logs\UAT_Log.txt for full exception trace)
	UATHelper: Packaging (Android (ASTC)): AutomationTool exiting with ExitCode=5 (5)
	UATHelper: Packaging (Android (ASTC)): BUILD FAILED
	PackagingResults: Error: Unknown Error


错误2：

	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lgpg
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lPhysX3PROFILE
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lPhysX3ExtensionsPROFILE
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lPhysX3CookingPROFILE
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lPhysX3CommonPROFILE
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lPxFoundationPROFILE
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lPxPvdSDKPROFILE
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lPsFastXmlPROFILE
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lPhysX3VehiclePROFILE
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lcxa_demangle
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -licudata
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -licuuc
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -licui18n
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -licule
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -liculx
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -licuio
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lfreetype2412
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lharfbuzz
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lpng
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lcurl
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -logg
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lvorbis
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lvorbisfile
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lopus
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lspeex_resampler
	10>D:/sdks/NVPACK_new/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld : error : cannot find -lPhysX3CookingPROFILE

错误3：

	10>  Added repository: D:\sdks\NVPACK_new\android-sdk-windows\extras\android\m2repository
	10>  AARImports: com.google.android.gms, play-services-auth, 11.0.4
	10>  AARImports: com.google.android.gms, play-services-games, 11.0.4
	10>  AARImports: com.google.android.gms, play-services-nearby, 11.0.4
	10>  AARImports: com.google.android.gms, play-services-plus, 11.0.4
	10>  AARImports: com.android.support, support-v13, 25.2.0
	10>  AARImports: com.google.android.gms, play-services-ads, 11.0.4
	10>EXEC : error : System.IO.DirectoryNotFoundException: 未能找到路径“C:\UnrealEngine-4.18.1-release\Engine\Intermediate\Android\APK\gradle\app\aar-imports.gradle”的一部分。
	10>            在 System.IO.__Error.WinIOError(Int32 errorCode, String maybeFullPath)
	10>            在 System.IO.FileStream.Init(String path, FileMode mode, FileAccess access, Int32 rights, Boolean useRights, FileShare share, Int32 bufferSize, FileOptions options, SECURITY_ATTRIBUTES secAttrs, String msgPath, Boolean bFromProxy, Boolean useLongPath, Boolean checkHost)
	10>            在 System.IO.FileStream..ctor(String path, FileMode mode, FileAccess access, FileShare share, Int32 bufferSize, FileOptions options, String msgPath, Boolean bFromProxy, Boolean useLongPath, Boolean checkHost)
	10>            在 System.IO.StreamWriter.CreateFile(String path, Boolean append, Boolean checkHost)
	10>            在 System.IO.StreamWriter..ctor(String path, Boolean append, Encoding encoding, Int32 bufferSize, Boolean checkHost)
	10>            在 System.IO.File.InternalWriteAllText(String path, String contents, Encoding encoding, Boolean checkHost)
	10>            在 UnrealBuildTool.UEDeployAndroid.GenerateGradleAARImports(String EngineDir, String UE4BuildPath, List`1 NDKArches) 位置 C:\UnrealEngine-4.18.1-release\Engine\Source\Programs\UnrealBuildTool\Platform\Android\UEDeployAndroid.cs:行号 3843
	10>            在 UnrealBuildTool.UEDeployAndroid.MakeApk(AndroidToolChain ToolChain, String ProjectName, String ProjectDirectory, String OutputPath, String EngineDirectory, Boolean bForDistribution, String CookFlavor, Boolean bMakeSeparateApks, Boolean bIncrementalPackage, Boolean bDisallowPackagingDataInApk, Boolean bDisallowExternalFilesDir) 位置 C:\UnrealEngine-4.18.1-release\Engine\Source\Programs\UnrealBuildTool\Platform\Android\UEDeployAndroid.cs:行号 2972
	10>            在 UnrealBuildTool.UEDeployAndroid.PrepTargetForDeployment(UEBuildDeployTarget InTarget) 位置 C:\UnrealEngine-4.18.1-release\Engine\Source\Programs\UnrealBuildTool\Platform\Android\UEDeployAndroid.cs:行号 3472
	10>            在 UnrealBuildTool.AndroidPlatform.Deploy(UEBuildDeployTarget Target) 位置 C:\UnrealEngine-4.18.1-release\Engine\Source\Programs\UnrealBuildTool\Platform\Android\UEBuildAndroid.cs:行号 521
	10>            在 UnrealBuildTool.UnrealBuildTool.RunUBT(BuildConfiguration BuildConfiguration, String[] Arguments, FileReference ProjectFile) 位置 C:\UnrealEngine-4.18.1-release\Engine\Source\Programs\UnrealBuildTool\UnrealBuildTool.cs:行号 1718
	10>  Total build time: 5.60 seconds (NoActionsToExecute executor: 0.00 seconds)
	10>C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V140\Microsoft.MakeFile.targets(41,5): error MSB3075: The command "..\..\Build\BatchFiles\Build.bat UE4Game Android Development -waitmutex" exited with code 5. Please verify that you have sufficient rights to run this command.

错误4：

如果设置了NDKROOT并重新运行Setup.bat下载了android相关的文件，rebuild的时候可能出现以下错误：

	error : D:/sdks/NVPACK/android-ndk-r12b/ndk-build.cmd failed with args APP_ABI="armeabi-v7a " NDK_DEBUG=1
	
解决办法：重启机器。。。


错误5：

	ProcessResult.StdOut:   Compiling Native code with NDK API 'android-19'
	ProcessResult.StdErr:   Performing 1 actions (4 in parallel)
	ProcessResult.StdErr:   [1/1] clang++.exe WarSoul-armv7-es2.so
	ProcessResult.StdErr:   D:/sdks/NVPACK/android-ndk-r12b/toolchains/arm-linux-androideabi-4.9/prebuilt/windows-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin\ld: error: cannot find -l-lcxa_demangle
	ProcessResult.StdErr:   clang++.exe: error: linker command failed with exit code 1 (use -v to see invocation)
	ProcessResult.StdErr:   ERROR: UBT ERROR: Failed to produce item: G:\Source\Work\project2\ue4_proj\WarSoul\Binaries\Android\WarSoul-armv7-es2.so
	ProcessResult.StdErr:   Total build time: 79.29 seconds (Local executor: 0.00 seconds)
	CommandUtils.Run: Took 79.5196648s to run UnrealBuildTool.exe, ExitCode=5

原因：自己的工程中使用了stl相关api（其实自己代码中没有使用stl、但是有个第三方plugin中使用了stl），但是ue4编译android版本时链接stl有bug。  
解决办法：将android-ndk-r12b\sources\cxx-stl\stlport\libs\armeabi\下的libstlport_static.a拷贝出来，放在工程的某个目录下并再Build.cs中链接此lib文件。这是ndk链接stl的bug，nkd 15版本据说已修复，但是ue4编译android版本只支持ndk 12即其以下版本。  
网上其他人说的解决办法（但是对我无效）：执行GenerateProjectFiles.bat重新生成UE4.sln，并打开VS后clean再rebuild。然后再build Android/Development。  

