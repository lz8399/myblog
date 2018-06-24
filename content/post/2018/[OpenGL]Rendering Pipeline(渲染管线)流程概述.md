+++
title= "[OpenGL]Rendering Pipeline(渲染管线)流程概述"
date= "2018-06-24T20:58:40+08:00"
categories= ["OpenGL"]
tags= ["Rendering", "OpenGL", "Pipeline"]
keywords= ["Rendering", "OpenGL", "Pipeline"]
+++

##### Pipeline

{{< figure src="/img/20180624-[OpenGL]Rendering Pipeline(渲染管线)流程概述/[OpenGL]Rendering Pipeline(渲染管线)流程概述-01.png">}}
(The blue boxes are programmable shader stages.)

The OpenGL rendering pipeline works in the following order:

1. Prepare vertex array data, and then render it
2. Vertex Processing:
	1. Each vertex is acted upon by a Vertex Shader. Each vertex in the stream is processed in turn into an output vertex.
	2. Optional primitive tessellation stages.
	3. Optional Geometry Shader primitive processing. The output is a sequence of primitives.
3. Vertex Post-Processing, the outputs of the last stage are adjusted or shipped to different locations.
	1. Transform Feedback happens here.
	2. Primitive Clipping, the perspective divide, and the viewport transform to window space.
4. Primitive Assembly
5. Scan conversion and primitive parameter interpolation, which generates a number of Fragments.
6. A Fragment Shader processes each fragment. Each fragment generates a number of outputs.
7. Per-Sample_Processing:
	1. Scissor Test
	2. Stencil Test
	3. Depth Test
	4. Blending
	5. Logical Operation
	6. Write Mask

参考自：Rendering Pipeline Overview  
https://www.khronos.org/opengl/wiki/Rendering_Pipeline_Overview

##### 流程实例
有了上述概念后，再来以一个简单实例演示管线流程：从一个 vertex shader 到一个 fragment shader 最简单流程。

basic.vert

	#version 410

	layout (location=0) in vec3 VertexPosition;
	layout (location=1) in vec3 VertexColor;

	out vec3 Color;

	void main()
	{
		Color = VertexColor;

		gl_Position = vec4(VertexPosition,1.0);
	}

basic.frag

	#version 410

	in vec3 Color;
	layout (location=0) out vec4 FragColor;

	void main() {
		FragColor = vec4(Color, 1.0);
	}

basic.vert中的VertexColor是绑定的顶点属性(即：vertex attribute，输入参数)，由OpenGL的库函数（一般都是编译型语言实现，例如C++）`glBindBuffer`、`glBufferData`等接口绑定，然后直接赋值给输出参数Color，这个Color会被渲染管线自动传递给fragment shader，fragement shader计算完毕后，然后再输出给`FragColor`。如果 fragment shader 只有一个输出参数，那么在你的OpenGL程序中可以不用`glBindFragDataLocation`、`glGetFragDataLocation`等库函数来指定输出参数。  
`gl_Position`是OpenGL提供的属性，用来存储当前vertex的position，以供管线流程中的 tessellation shader 和 geometry shader 运行时使用。

***
`谁都可能出个错儿，你在一件事情上越琢磨得多就越容易出错。---《好兵帅克历险记》`
