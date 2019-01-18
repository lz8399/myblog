+++
title= "[UE4][Build.cs]Get the current Project Directory"
date= "2019-01-14T14:25:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Sequencer"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-016.jpg"
+++

.

<!--more-->

##### New way


	public string ProjectRoot
	{
		get
		{
			return System.IO.Path.GetFullPath(System.IO.Path.Combine(ModuleDirectory, "../../"));
		}
	}

https://answers.unrealengine.com/questions/237166/how-can-i-get-the-current-project-path-within-the.html


##### Old way (Removed in 4.21)

	using System.IO;  
	using UnrealBuildTool;  
	  
	public class MyProject : ModuleRules  
	{  
		RulesAssembly r;  
	  
		private string ModulePath  
		{  
			get { return Path.GetDirectoryName( r.GetModuleFileName(this.GetType().Name).CanonicalName); }  
		}  
	  
		private string ThirdPartyPath  
		{  
			get { return Path.GetFullPath(Path.Combine(ModulePath, "../../ThirdParty/")); }  
		}  
	  
		public MyProject(TargetInfo Target)  
		{  
	  
			FileReference CheckProjectFile;  
			UProjectInfo.TryGetProjectForTarget("MyProject", out CheckProjectFile);  
			r = RulesCompiler.CreateProjectRulesAssembly(CheckProjectFile);  
		}  
	}

***
`我年轻时，听一位教授讲：“人生都只有一个想法，终其一生不过是不断丰富它。”我当时觉得：“一辈子只围绕一个念头转？这未免也太反动了！”五十岁时，我明白他是对的：我这一辈子都在追随一个想法，问题是我从来都不知道是哪个。`──翁贝托·埃科《密涅瓦火柴盒》