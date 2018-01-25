+++
title= "[UE4]NavigationSystem寻路相关的API"
date= "2016-06-21T12:02:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++

检测某个坐标点是否在navmesh内，即可以作为寻路的坐标点。
UNavigationSystem::TestPathSync 实例用法：

    UNavigationSystem* const NavSys = GetWorld()->GetNavigationSystem();
    const ANavigationData* NavData = NavSys->GetNavDataForProps(YourCharacter->GetNavAgentPropertiesRef());
    FPathFindingQuery Query1(YourCharacter, *NavData, YourCharacter->GetNavAgentLocation(), TestLocation);
    bool qrs1 = NavSys->TestPathSync(Query1);


UNavigationSystem::FindPathSync也可以判断，但是他会返回寻路结果，效率上没有TestPathSync快。
其他的API还有：

    UNavigationSystem::ProjectPointToNavigation