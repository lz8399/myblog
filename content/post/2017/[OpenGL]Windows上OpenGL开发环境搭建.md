+++
title= "[OpenGL]Windows上OpenGL开发环境搭建"
date= "2017-09-05T16:38:28+08:00"
categories= ["OpenGL"]
tags= ["Graphics", "OpenGL"]
+++


转载请注明出处：http://www.dawnarc.com/

网上资料很多都是基于Cygwin来搭建的环境，这里介绍一种非Cygwin搭建Windows上的OpenGL开发环境。

1，OpenGL Loader Generator下载安装  
OpenGL Loader是一个标准规范，定义了如何在运行时期间加载OpenGL相关函数的指针。 
这是windows上开发OpenGL程序才需要的lib，因为从1.1版本开始，windows不在对OpenGL
后续版本的 ABI(application binary interface)提供支持（可能是微软的DX出来后与OGL商业竞争吧），所以开发者无法直接获取OGL新版本的相关函数，不过有好心人写了工具，在运行时期间获取OGL的新版函数，这里介绍两个开源库：  
glad  
https://github.com/Dav1dde/glad  
glloadgen  
https://bitbucket.org/alfonse/glloadgen/wiki/Home

我是用的是glad，这个开源库的开发者还提供了在线生成工具，可以不用下载安装Load Generator，直接在线生成指定版本的OpenGL Loader： 
http://glad.dav1d.de/

2，编译OpenGL Loader的静态库  
通过glad生成的代码，编译一个lib， 以便后面的的示例工程调用。因为这些代码开发者不用做修改，只是调用，所以最好编译成lib，而不要直接加到自己的项目代码中。

3，下载GLM（OpenGL Mathematics）  
这是OpenGL的数学库  
https://github.com/g-truc/glm/releases

4，下载GLFW  
这是一个提供了OpenGL, OpenGL ES和Vulkan相关接口的跨平台的开源库，有这个库你就可以访问他们的最新API。
https://github.com/glfw/glfw/releases

5，新建一个C++工程并设置OpenGL相关的头文件和静态库

指定头文件的目录
{{< figure src="/img/20170905-[OpenGL]Windows上OpenGL开发环境搭建/[OpenGL]Windows上OpenGL开发环境搭建-01.jpg">}}

指定静态库的目录
{{< figure src="/img/20170905-[OpenGL]Windows上OpenGL开发环境搭建/[OpenGL]Windows上OpenGL开发环境搭建-02.jpg">}}

在代码需要包含的头文件以及lib：

    #include <KHR/khrplatform.h>
    #include <glad/glad.h>
    #include <GLFW/glfw3.h>

    #pragma comment(lib, "opengl32.lib")
    #pragma comment(lib, "glad.lib")
    #pragma comment(lib, "glfw3.lib")

新建的测试工程叫GLTest，目录结构如下：
新加了两个分别叫include和lib的目录，用于存放第三方库的头文件和库文件
{{< figure src="/img/20170905-[OpenGL]Windows上OpenGL开发环境搭建/[OpenGL]Windows上OpenGL开发环境搭建-03.jpg">}}

完整的测试的代码：

    #pragma once

    #include <iostream>
    #include <windows.h>

    #include <fstream>
    #include <sstream>
    #include <string>

    #include <KHR/khrplatform.h>
    #include <glad/glad.h>
    #include <GLFW/glfw3.h>

    #pragma comment(lib, "opengl32.lib")
    #pragma comment(lib, "glad.lib")
    #pragma comment(lib, "glfw3.lib")

    using std::string;
    using std::ifstream;

    GLFWwindow *window;

    static HMODULE libGL;

    GLuint vaoHandle;

    int width, height;

    void update(float t);

    void render();

    void mainLoop() {
        while (!glfwWindowShouldClose(window) && !glfwGetKey(window, GLFW_KEY_ESCAPE)) {

            update(float(glfwGetTime()));
            render();
            glfwSwapBuffers(window);
            glfwPollEvents();
        }
    }

    static void key_callback(GLFWwindow* window, int key, int scancode, int action, int mods)
    {
    }

    void dumpGLInfo(bool dumpExtensions) {
        const GLubyte *renderer = glGetString(GL_RENDERER);
        const GLubyte *vendor = glGetString(GL_VENDOR);
        const GLubyte *version = glGetString(GL_VERSION);
        const GLubyte *glslVersion = glGetString(GL_SHADING_LANGUAGE_VERSION);

        GLint major, minor;
        glGetIntegerv(GL_MAJOR_VERSION, &major);
        glGetIntegerv(GL_MINOR_VERSION, &minor);

        printf("-------------------------------------------------------------\n");
        printf("GL Vendor    : %s\n", vendor);
        printf("GL Renderer  : %s\n", renderer);
        printf("GL Version   : %s\n", version);
        printf("GL Version   : %d.%d\n", major, minor);
        printf("GLSL Version : %s\n", glslVersion);
        printf("-------------------------------------------------------------\n");

        if (dumpExtensions) {
            GLint nExtensions;
            glGetIntegerv(GL_NUM_EXTENSIONS, &nExtensions);
            for (int i = 0; i < nExtensions; i++) {
                printf("%s\n", glGetStringi(GL_EXTENSIONS, i));
            }
        }
    }

    void linkMe(GLint vertShader, GLint fragShader)
    {
        // Create the program object
        GLuint programHandle = glCreateProgram();
        if (0 == programHandle) {
            fprintf(stderr, "Error creating program object.\n");
            exit(1);
        }

        // Bind index 0 to the shader input variable "VertexPosition"
        //glBindAttribLocation(programHandle, 0, "VertexPosition");
        // Bind index 1 to the shader input variable "VertexColor"
        //glBindAttribLocation(programHandle, 1, "VertexColor");

        // Attach the shaders to the program object
        glAttachShader(programHandle, vertShader);
        glAttachShader(programHandle, fragShader);

        // Link the program
        glLinkProgram(programHandle);

        // Check for successful linking
        GLint status;
        glGetProgramiv(programHandle, GL_LINK_STATUS, &status);
        if (GL_FALSE == status) {

            fprintf(stderr, "Failed to link shader program!\n");

            GLint logLen;
            glGetProgramiv(programHandle, GL_INFO_LOG_LENGTH, &logLen);

            if (logLen > 0) {
                char * log = (char *)malloc(logLen);

                GLsizei written;
                glGetProgramInfoLog(programHandle, logLen, &written, log);

                fprintf(stderr, "Program log: \n%s", log);

                free(log);
            }
        }
        else {
            glUseProgram(programHandle);
        }
    }

    void initScene(){
        //////////////////////////////////////////////////////
        /////////// Vertex shader //////////////////////////
        //////////////////////////////////////////////////////

        // Load contents of file
        ifstream inFile("shader/basic.vert");
        if (!inFile) {
            fprintf(stderr, "Error opening file: shader/basic.vert\n");
            exit(1);
        }

        std::stringstream code;
        code << inFile.rdbuf();
        inFile.close();
        string codeStr(code.str());

        // Create the shader object
        GLuint vertShader = glCreateShader(GL_VERTEX_SHADER);
        if (0 == vertShader) {
            fprintf(stderr, "Error creating vertex shader.\n");
            exit(EXIT_FAILURE);
        }

        // Load the source code into the shader object
        const GLchar* codeArray[] = { codeStr.c_str() };
        glShaderSource(vertShader, 1, codeArray, NULL);

        // Compile the shader
        glCompileShader(vertShader);

        // Check compilation status
        GLint result;
        glGetShaderiv(vertShader, GL_COMPILE_STATUS, &result);
        if (GL_FALSE == result) {
            fprintf(stderr, "Vertex shader compilation failed!\n");

            GLint logLen;
            glGetShaderiv(vertShader, GL_INFO_LOG_LENGTH, &logLen);

            if (logLen > 0) {
                char * log = (char *)malloc(logLen);

                GLsizei written;
                glGetShaderInfoLog(vertShader, logLen, &written, log);

                fprintf(stderr, "Shader log: \n%s", log);

                free(log);
            }
        }

        //////////////////////////////////////////////////////
        /////////// Fragment shader //////////////////////////
        //////////////////////////////////////////////////////

        // Load contents of file into shaderCode here
        ifstream fragFile("shader/basic.frag");
        if (!fragFile) {
            fprintf(stderr, "Error opening file: shader/basic.frag\n");
            exit(1);
        }

        std::stringstream fragCode;
        fragCode << fragFile.rdbuf();
        fragFile.close();
        codeStr = fragCode.str();

        // Create the shader object
        GLuint fragShader = glCreateShader(GL_FRAGMENT_SHADER);
        if (0 == fragShader) {
            fprintf(stderr, "Error creating fragment shader.\n");
            exit(1);
        }

        // Load the source code into the shader object
        codeArray[0] = codeStr.c_str();
        glShaderSource(fragShader, 1, codeArray, NULL);

        // Compile the shader
        glCompileShader(fragShader);

        // Check compilation status
        glGetShaderiv(fragShader, GL_COMPILE_STATUS, &result);
        if (GL_FALSE == result) {
            fprintf(stderr, "Fragment shader compilation failed!\n");

            GLint logLen;
            glGetShaderiv(fragShader, GL_INFO_LOG_LENGTH, &logLen);

            if (logLen > 0) {
                char * log = (char *)malloc(logLen);

                GLsizei written;
                glGetShaderInfoLog(fragShader, logLen, &written, log);

                fprintf(stderr, "Shader log: \n%s", log);

                free(log);
            }
        }

        linkMe(vertShader, fragShader);

        /////////////////// Create the VBO ////////////////////
        float positionData[] = {
            -0.8f, -0.8f, 0.0f,
            0.8f, -0.8f, 0.0f,
            0.0f,  0.8f, 0.0f };
        float colorData[] = {
            1.0f, 0.0f, 0.0f,
            0.0f, 1.0f, 0.0f,
            0.0f, 0.0f, 1.0f };


        // Create and populate the buffer objects
        GLuint vboHandles[2];
        glGenBuffers(2, vboHandles);
        GLuint positionBufferHandle = vboHandles[0];
        GLuint colorBufferHandle = vboHandles[1];

        glBindBuffer(GL_ARRAY_BUFFER, positionBufferHandle);
        glBufferData(GL_ARRAY_BUFFER, 9 * sizeof(float), positionData, GL_STATIC_DRAW);

        glBindBuffer(GL_ARRAY_BUFFER, colorBufferHandle);
        glBufferData(GL_ARRAY_BUFFER, 9 * sizeof(float), colorData, GL_STATIC_DRAW);

        // Create and set-up the vertex array object
        glGenVertexArrays(1, &vaoHandle);
        glBindVertexArray(vaoHandle);

        glEnableVertexAttribArray(0);  // Vertex position
        glEnableVertexAttribArray(1);  // Vertex color

		////break current vertex array object binding.
        glBindBuffer(GL_ARRAY_BUFFER, positionBufferHandle);
        glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 0, (GLubyte *)NULL);

        glBindBuffer(GL_ARRAY_BUFFER, colorBufferHandle);
        glVertexAttribPointer(1, 3, GL_FLOAT, GL_FALSE, 0, (GLubyte *)NULL);
        glBindVertexArray(0);
    }

    void update(float t)
    {

    }

    void render()
    {
        glClear(GL_COLOR_BUFFER_BIT);

        glBindVertexArray(vaoHandle);
        glDrawArrays(GL_TRIANGLES, 0, 3);
        glBindVertexArray(0);
    }

    void resize(int w, int h)
    {
        width = w;
        height = h;
        glViewport(0, 0, w, h);
    }


    void initializeGL() {
        glClearColor(0.5f, 0.5f, 0.5f, 1.0f);
        initScene();
    }


    int main(int argc, char* argv[])
    {
        // Initialize GLFW
        if (!glfwInit()) exit(EXIT_FAILURE);

    #ifdef __APPLE__
        // Select OpenGL 4.1
        glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 4);
        glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 1);
    #else
        // Select OpenGL 4.3
        glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 4);
        glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);
    #endif
        glfwWindowHint(GLFW_OPENGL_FORWARD_COMPAT, true);
        glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);
        glfwWindowHint(GLFW_RESIZABLE, false);
        glfwWindowHint(GLFW_OPENGL_DEBUG_CONTEXT, true);

        // Open the window
        string title = "OpenGLTest";
        window = glfwCreateWindow(500, 500, title.c_str(), NULL, NULL);
        if (!window) {
            glfwTerminate();
            exit(EXIT_FAILURE);
        }
        glfwMakeContextCurrent(window);
        glfwSetKeyCallback(window, key_callback);

        // Get framebuffer size
        int fbw, fbh;
        glfwGetFramebufferSize(window, &fbw, &fbh);

        // Load the OpenGL functions.
        if (!gladLoadGL()) { exit(-1); }

        dumpGLInfo(false);

        // Initialization
        initializeGL();

        // Enter the main loop
        mainLoop();

        // Close window and terminate GLFW
        glfwTerminate();
        // Exit program
        exit(EXIT_SUCCESS);

        return 0;
    }

最终效果：
{{< figure src="/img/20170905-[OpenGL]Windows上OpenGL开发环境搭建/[OpenGL]Windows上OpenGL开发环境搭建-04.jpg">}}

测试工程下载地址：  
http://pan.baidu.com/s/1nvp6kUt  
只保证Release模式下正常运行，Debug版本需要指定第三方库的debug版本

示例代码参考自：  
https://github.com/daw42/glslcookbook/blob/master/chapter01/scenebasic.cpp

***
`只愿君心似我心，定不负，相思意。---李之仪《卜算子》`