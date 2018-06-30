+++
title= "[C++]non-static member function as callback function and achieve inheritance"
date= "2018-06-30T17:19:40+08:00"
categories= ["C++"]
tags= ["C++"]
keywords= ["C++", "non-static member function", "inheritance polymorphism"]
+++

keywords：C++ 非静态成员函数作为回调函数并实现继承多态

Base.hpp

    #pragma once

    class Base
    {
    public:

        virtual void TestFun1(int Param) {}

        virtual void TestFun2(int Param) {}
    };

Child.hpp

    #pragma once

    #include <iostream>
    #include "Base.hpp"

    class Child : public Base
    {
    public:

        void TestFun1(int Param) override
        {
            printf("Fun1 : %d\n", Param);
        }

        void TestFun2(int Param) override
        {
            printf("Fun2 : %d\n", Param);
        }
    };

EventManager.h

    // Fill out your copyright notice in the Description page of Project Settings.

    #pragma once

    #include <map>
    #include <vector>
    #include "Base.hpp"

    enum EventDefine
    {
        EVENT_TEST = 1,
    };


    #define ADD_EVENT(EventID, Object, pCbFun) EventManager::Instance()->AddEvent(EventID,  Object, pCbFun);

    #define REMOVE_EVENT(EventID, Object, pCbFun) EventManager::Instance()->RemoveEvent(EventID, Object, pCbFun);

    #define BROADCAST_EVENT(EventID, Param) EventManager::Instance()->Broadcast(EventID, Param);


    class Base;

    typedef void (Base::*CallbackFun)(int);

    struct EventExecInfo
    {
        Base* Object;
        CallbackFun Function;
    };


    /**
     *  
     */
    class EventManager
    {
    private:

        EventManager();
        ~EventManager();

    public:

        static EventManager* Instance();

        void AddEvent(EventDefine EventID, Base* Object, CallbackFun pCbFun);

        void RemoveEvent(EventDefine EventID, const Base* Object, const CallbackFun pCbFun);

        void Broadcast(EventDefine EventID, int Param);

    private:

        static EventManager* Instance_;

        typedef std::map<EventDefine, std::vector<EventExecInfo>>::iterator MAP_ITER;
        std::map<EventDefine, std::vector<EventExecInfo>> EventMap;
    };

EventManager.cpp

    // Fill out your copyright notice in the Description page of Project Settings.

    #include "EventManager.h"

    EventManager* EventManager::Instance_ = nullptr;

    EventManager::EventManager()
    {
    }

    EventManager::~EventManager()
    {
    }

    EventManager* EventManager::Instance()
    {
        if (!Instance_)
        {
            Instance_ = new EventManager();
        }
        return Instance_;
    }

    void EventManager::AddEvent(EventDefine EventID, Base* Object, CallbackFun pCbFun)
    {
        MAP_ITER Iter = EventMap.find(EventID);
        if (EventMap.end() == Iter)
        {
            std::vector<EventExecInfo> vec;
            EventMap.insert(make_pair(EventID, vec));
            Iter = EventMap.find(EventID);
        }

        std::vector<EventExecInfo>& ExecArray = Iter->second;

        EventExecInfo Exec;
        Exec.Object = Object;
        Exec.Function = pCbFun;
        ExecArray.push_back(Exec);
    }

    void EventManager::RemoveEvent(EventDefine EventID, const Base* Object, const CallbackFun pCbFun)
    {
        MAP_ITER Iter = EventMap.find(EventID);
        if (EventMap.end() != Iter)
        {
            for (auto i = Iter->second.begin(); i != Iter->second.end();)
            {
                EventExecInfo& ExecInfo = *i;
                if (Object == ExecInfo.Object && ExecInfo.Function == pCbFun)
                {
                    i = Iter->second.erase(i);
                }
                else
                {
                    i++;
                }
            }
        }
    }

    void EventManager::Broadcast(EventDefine EventID, int Param)
    {
        MAP_ITER Iter = EventMap.find(EventID);
        if (EventMap.end() != Iter)
        {
            for (EventExecInfo& ExecInfo : Iter->second)
            {
                if (ExecInfo.Object && ExecInfo.Function)
                {
                    (ExecInfo.Object->*(ExecInfo.Function))(Param);
                }
            }
        }
    }
    
测试代码 Main.cpp
    
    #pragma once

    #include "EventManager.h"
    #include "Child.hpp"

    int main(char** args, int argc)
    {
        Child C;
        
        ADD_EVENT(EventDefine::EVENT_TEST, (Base*)(&C), &Base::TestFun1);
        ADD_EVENT(EventDefine::EVENT_TEST, (Base*)(&C), &Base::TestFun2);
        
        BROADCAST_EVENT(EventDefine::EVENT_TEST, 111);
        BROADCAST_EVENT(EventDefine::EVENT_TEST, 222);

        REMOVE_EVENT(EventDefine::EVENT_TEST, (Base*)(&C), &Base::TestFun1);
        REMOVE_EVENT(EventDefine::EVENT_TEST, (Base*)(&C), &Base::TestFun2);

        system("pause");
    }

***
` 世上只有一种英雄主义，就是在认清生活真相之后依然热爱生活。---罗曼•罗兰《巨人三传》`