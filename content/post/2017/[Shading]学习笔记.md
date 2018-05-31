---
title: "[Shading]学习笔记"
date: "2017-01-13T14:28:40+08:00"
categories:
- Shading
tags:
- Graphics
- OpenGL
---

《OpenGL 4 Shading Language Cookbook, Second Edition》
书中的代码：
https://github.com/daw42/glslcookbook

##### 术语解释：
* `GLEW` (OpenGL Extension Wrangler).
* `GLM` (OpenGL Mathematics)
* `GLFW` is an Open Source, multi-platform library for OpenGL, OpenGL ES and Vulkan development on the desktop. It provides a simple API for creating windows, contexts and surfaces, receiving input and events.


#### Shader类型
* vertex shader
* fragment shader
* geometry shader
* tess_control shader
* tess_evaluation shader
* compute shader

##### Uniform blocks意义和作用

If your program involves multiple shader programs that use the same uniform variables, one has to manage the variables separately for each program. Uniform locations are generated when a program is linked, so the locations of the uniforms may change from one program to the next.
The data for those uniforms may have to be regenerated and applied to the new locations.
Uniform blocks were designed to ease the sharing of uniform data between programs.
With uniform blocks, one can create a buffer object for storing the values of all the uniform variables, and bind the buffer to the uniform block. When changing programs, the same buffer object need only be re-bound to the corresponding block in the new program.

##### glBufferData的作用

Create the buffer object and copy the data into it:

    GLuint uboHandle;
    glGenBuffers( 1, &uboHandle );
    glBindBuffer( GL_UNIFORM_BUFFER, uboHandle );
    glBufferData( GL_UNIFORM_BUFFER, blockSize, blockBuffer, GL_DYNAMIC_DRAW );

The space is allocated within the buffer object and the data is copied when glBufferData is called.


##### glBindBufferBase的索引问题

glBindBufferBase函数参数的索引（第二个参数）必须与定义uniform时设定的layout(binding=)相同，例如：

    glBindBufferBase(GL_UNIFORM_BUFFER, 0, uboHandle);

对应的uniform定义

    layout (binding = 0) uniform BlobSettings {
        vec4 InnerColor;
        vec4 OuterColor;
        float RadiusInner;
        float RadiusOuter;
    };


##### glBindBuffer与glBindBufferBase的区别

You might be wondering why we use glBindBuffer and glBindBufferBase with GL_UNIFORM_BUFFER. Aren't these the same binding points used in two different contexts? The answer is that the GL_UNIFORM_BUFFER point can be used in each function with a slightly different meaning. With glBindBuffer, we bind to a point that can be used for filling or modifying a buffer, but can't be used as a source of data for the shader. When we use glBindBufferBase, we are binding to an index within a location that can be directly sourced by the shader. Granted, that's a bit confusing.


##### uniform layout类型：

std140
shared
packed
row_major
column_major

例如：

    layout( std140 ) uniform BlobSettings {
    };

 

多个修饰符可以组合使用：

    layout( row_major, shared ) uniform BlobSettings {
    };

##### fragment shader到vertex shader之间的工作流程（page 58）
{{< figure src="/img/20170113-[Shading]学习笔记/[Shading]学习笔记-01.jpg">}}

Between the vertex and fragment shader, the vertices are assembled into primitives, clipping takes place, and the viewport transformation is applied (among other operations). The rasterization process then takes place and the polygon is filled (if necessary). The fragment shader is executed once for each fragment (pixel) of the polygon being rendered (typically in parallel). Data provided from the vertex shader is (by default) interpolated in a perspective correct manner, and provided to the fragment shader via shader input variables. The fragment shader determines the appropriate color for the pixel and sends it to the frame buffer using output variables. The depth information is handled automatically.

***
`莫道不消魂？帘卷西风，人比黄花瘦。---李清照《醉花阴》`