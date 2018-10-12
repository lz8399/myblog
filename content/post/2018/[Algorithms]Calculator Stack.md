+++
title= "[Algorithms]Calculator Stack"
date= "2018-10-12T14:36:28+08:00"
categories= ["Algorithms"]
tags= ["Algorithms"]
+++

keywords：计算器代码、Calculator

    #include "stdio.h"
    #include "string.h"
    #define MAX 1001
     
    double stack[MAX];
    int tail;
     
    int main(){
        int a;
        while(scanf("%d ",&a)&&a!=0){
            tail=0;
            stack[++tail]=1.0*a;//tail始终指向末尾数字位置
            //1.入栈所有数据（如果遇到*/号，只更新栈尾）
            char ch1,ch2;
            while(scanf("%c %d%c",&ch1,&a,&ch2)!=EOF){
                if(ch1=='+'){
                    stack[++tail]=1.0*a;//push
                }else if(ch1=='-'){
                    stack[++tail]=-1.0*a;//push neg
                }else if(ch1=='*'){
                    stack[tail]=stack[tail]*a;//update tail
                }else if(ch1=='/'){
                    stack[tail]=stack[tail]/(double)a;//updata tail
                }
                if(ch2!=' ')
                    break; 
            }
            //2.把栈里头的东西全部加起来，求和
            double result=0;
            for(int i=1;i<=tail;i++)
                result+=stack[i];
            printf("%.2lf\n",result);
        }
        return 1;
    }
   
原文：https://blog.csdn.net/JIEJINQUANIL/article/details/51405381