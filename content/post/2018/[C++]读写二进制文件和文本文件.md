+++
title= "[C++]读写二进制文件和文本文件"
date= "2018-04-20T17:45:40+08:00"
categories= ["C++"]
tags= ["C++", "read and write binary"]
+++

### ifstream,ofstream读写二进制文件

    #include <iostream>  
    #include <fstream>  
    using namespace std;  
      
    int main(int argc, char** argv)  
    {  
      
      int a[5] = {1,2,3,4,5};  
      int b[5];  
      
      ofstream ouF;  
      ouF.open("./me.dat", std::ofstream::binary);  
      ouF.write(reinterpret_cast<const char*>(a), sizeof(int)*5);  
      ouF.close();  
      
      ifstream inF;  
      inF.open("./me.dat", std::ifstream::binary);  
      inF.read(reinterpret_cast<char*>(b), sizeof(int)*5);  
      inF.close();  
      
      for (int i = 0; i < 5; i++)  
      {  
        cout << b[i] << endl;  
      }  
      return 0;  
    }  

参考自：https://blog.csdn.net/bendanban/article/details/30039193

### C模式读写二进制文件

    //采用C模式写二进制文件  
    void DataWrite_CMode()  
    {  
        //准备数据  
        double pos[200];  
        for(int i = 0; i < 200; i ++ )  
            pos[i] = i ;  
        //写出数据  
        FILE *fid;  
        fid = fopen("binary.dat","wb");  
        if(fid == NULL)  
        {  
            printf("写出文件出错");  
            return;  
        }  
        int mode = 1;  
        printf("mode为1，逐个写入；mode为2，逐行写入\n");  
        scanf("%d",&mode);  
        if(1==mode)  
        {  
            for(int i = 0; i < 200; i++)  
                fwrite(&pos[i],sizeof(double),1,fid);  
        }  
        else if(2 == mode)  
        {  
            fwrite(pos, sizeof(double), 200, fid);  
        }  
        fclose(fid);  
    }
    
    //采用C模式读二进制文件  
    void DataRead_CMode()  
    {  
        FILE *fid;  
        fid = fopen("binary.dat","rb");  
        if(fid == NULL)  
        {  
            printf("读取文件出错");  
            return;  
        }  
        int mode = 1;  
        printf("mode为1，知道pos有多少个；mode为2，不知道pos有多少个\n");  
        scanf("%d",&mode);  
        if(1 == mode)  
        {  
            double pos[200];  
            fread(pos,sizeof(double),200,fid);  
            for(int i = 0; i < 200; i++)  
                printf("%lf\n", pos[i]);  
            free(pos);  
        }  
        else if(2 == mode)  
        {  
            //获取文件大小  
            fseek (fid , 0 , SEEK_END);         
            long lSize = ftell (fid);    
            rewind (fid);   
            //开辟存储空间  
            int num = lSize/sizeof(double);  
            double *pos = (double*) malloc (sizeof(double)*num);    
            if (pos == NULL)    
            {    
                printf("开辟空间出错");     
                return;   
            }   
            fread(pos,sizeof(double),num,fid);  
            for(int i = 0; i < num; i++)  
                printf("%lf\n", pos[i]);  
            free(pos);     //释放内存  
        }  
        fclose(fid);  
    }

参考自：https://blog.csdn.net/nichengwuxiao/article/details/78789225


### ifstream,ofstream读写文本文件

    // writing on a text file
    #include <fiostream.h>

    int main () 
    {
        ofstream examplefile   ("example.txt");
        if (examplefile.is_open()) 
        {
            examplefile <<   "This is a line.\n";
            examplefile <<   "This is another line.\n";
            examplefile.close();
        }
        return 0;
    }
    
    // reading a text file
    #include <iostream.h>
    #include <fstream.h>
    #include <stdlib.h>

    int main () 
    {
        char buffer[256];
        ifstream examplefile   ("example.txt");
        if (! examplefile.is_open())
        {
            cout << "Error   opening file"; exit (1); 
        }
        while (! examplefile.eof() ) 
        {
            examplefile.getline   (buffer,100);
            cout << buffer   << endl;
        }
        return 0;
    }
    
参考自：http://www.cnblogs.com/azraelly/archive/2012/04/14/2446914.html

### C模式读写文本文件

    #include <stdio.h>  
  
    int main()  
    {  
        //下面是写数据，将数字0~9写入到data.txt文件中  
        FILE *fpWrite=fopen("data.txt","w");  
        if(fpWrite==NULL)  
        {  
            return 0;  
        }  
        for(int i=0;i<10;i++)  
            fprintf(fpWrite,"%d ",i);  
        fclose(fpWrite);  
        //下面是读数据，将读到的数据存到数组a[10]中，并且打印到控制台上  
        int a[10]={0};  
        FILE *fpRead=fopen("data.txt","r");  
        if(fpRead==NULL)  
        {  
            return 0;  
        }  
        for(int i=0;i<10;i++)  
        {  
            fscanf(fpRead,"%d ",&a[i]);  
            printf("%d ",a[i]);  
        }  
        getchar();//等待  
      
        return 1;  
    }
    
参考自：https://blog.csdn.net/hjl240/article/details/47132477

***
`为天地立心，为生民立命，为往圣继绝学，为万世开太平。 ----北宋·张载`