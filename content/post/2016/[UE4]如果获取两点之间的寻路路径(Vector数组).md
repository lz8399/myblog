+++
title= "[UE4]如果获取两点之间的寻路路径(Vector数组)"
date= "2016-06-13T12:18:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

代码：

    UNavigationPath *tpath;
    UNavigationSystem* NavSys = UNavigationSystem::GetCurrent(GetWorld());
     
    tpath = NavSys->FindPathToLocationSynchronously(GetWorld(), GetActorLocation(), end_point);
         
    if (tpath != NULL)
    {
         for (int pointiter = 0; pointiter < tpath->PathPoints.Num(); pointiter++)
         {
             DrawDebugSphere(GetWorld(), tpath->PathPoints[pointiter], 10.0f, 12, FColor(255, 0, 0));
         }
    }

参考：https://answers.unrealengine.com/questions/102126/how-do-i-get-the-navigation-path-to-a-point.html