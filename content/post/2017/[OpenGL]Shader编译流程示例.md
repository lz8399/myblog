+++
title= "[OpenGL]Shader编译流程示例"
date= "2017-09-29T18:04:28+08:00"
categories= ["OpenGL"]
tags= ["Shading", "Graphics", "OpenGL"]
+++

这里以演示如何编译Vertex Shader为例，其他类型的Shader类似。

1，先用io流读取shader文件

    std::stringstream code;
    code << inFile.rdbuf();
    inFile.close();
    string codeStr(code.str());

2，创建空白Shader对象

    GLuint vertShader = glCreateShader( GL_VERTEX_SHADER );

3，编译Shader代码到Shader对象中

    // Load the source code into the shader object
    const GLchar* codeArray[] = {codeStr.c_str()};
    glShaderSource(vertShader, 1, codeArray, NULL);

    // Compile the shader
    glCompileShader( fragShader );

4，Shader链接  
4.1 创建program对象

    // Create the program object
    GLuint programHandle = glCreateProgram();

4.2 附加Shader对象到program对象中

    // Attach the shaders to the program object
    glAttachShader( programHandle, vertShader );
    glAttachShader( programHandle, fragShader );

4.3 链接program

    // Link the program
    glLinkProgram( programHandle );

4.4 使用program对象

    glUseProgram( programHandle );


5，创建并绑定buffer对象

绑定buffer的意义：当渲染（Rendering）的时候，着色器(shader)每当被执行时，OpenGL从这些buffer中拉取属性(attribute)数据给这些着色器。

    // Create and populate the buffer objects
    GLuint vboHandles[2];
    glGenBuffers(2, vboHandles);
    GLuint positionBufferHandle = vboHandles[0];
    GLuint colorBufferHandle = vboHandles[1];

    glBindBuffer(GL_ARRAY_BUFFER, positionBufferHandle);
    glBufferData(GL_ARRAY_BUFFER, 9 * sizeof(float), positionData, GL_STATIC_DRAW);

    glBindBuffer(GL_ARRAY_BUFFER, colorBufferHandle);
    glBufferData(GL_ARRAY_BUFFER, 9 * sizeof(float), colorData, GL_STATIC_DRAW);

6，开辟Array数组并填充其数据

    // Create and set-up the vertex array object
    glGenVertexArrays( 1, &vaoHandle );
    glBindVertexArray(vaoHandle);

    glEnableVertexAttribArray(0);  // Vertex position
    glEnableVertexAttribArray(1);  // Vertex color

    glBindBuffer(GL_ARRAY_BUFFER, positionBufferHandle);
    glVertexAttribPointer( 0, 3, GL_FLOAT, GL_FALSE, 0, (GLubyte *)NULL );

    glBindBuffer(GL_ARRAY_BUFFER, colorBufferHandle);
    glVertexAttribPointer( 1, 3, GL_FLOAT, GL_FALSE, 0, (GLubyte *)NULL );
    glBindVertexArray(0);
        
***
`只愿君心似我心，定不负，相思意。---李之仪《卜算子》`