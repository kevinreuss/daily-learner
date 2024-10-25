# Shader Programming in Graphics

Shader programming is a specialized form of programming used to control the rendering pipeline in graphics processing units (GPUs). This technique allows developers to customize the way 3D objects are drawn on screens, which is a key aspect of modern computer graphics.

## Types of Shaders

Shaders in graphics programming typically come in two main types:

- **Vertex Shaders**: These manipulate the properties (such as position, color, texture coordinates) of individual vertices. A simple example of vertex shader code in GLSL (OpenGL Shading Language) might look like this:

    ```glsl
    #version 330 core
    layout (location = 0) in vec3 aPos;

    void main()
    {
       gl_Position = vec4(aPos.x, aPos.y, aPos.z, 1.0);
    }
    ```
- **Fragment Shaders** (or Pixel Shaders): These determine how the pixels within each fragment are colored and displayed. A basic fragment shader might look like:

    ```glsl
    #version 330 core
    out vec4 FragColor;

    void main()
    {
       FragColor = vec4(1.0f, 0.5f, 0.2f, 1.0f);
    }
    ```

## Shader Compilation

Shaders are compiled at runtime, which means they can be dynamically generated and modified. This provides a lot of flexibility in rendering effects. After a shader source code is written, it must be compiled and attached to a shader program as shown below:

```cpp
GLuint vertexShader = glCreateShader(GL_VERTEX_SHADER);
glShaderSource(vertexShader, 1, &vertexShaderSource, NULL);
glCompileShader(vertexShader);

GLuint fragmentShader = glCreateShader(GL_FRAGMENT_SHADER);
glShaderSource(fragmentShader, 1, &fragmentShaderSource, NULL);
glCompileShader(fragmentShader);

GLuint shaderProgram = glCreateProgram();
glAttachShader(shaderProgram, vertexShader);
glAttachShader(shaderProgram, fragmentShader);
glLinkProgram(shaderProgram);

glUseProgram(shaderProgram);
```

## Shader Pipelines

Modern GPUs use a pipeline architecture for rendering, where each stage of the pipeline can be controlled by a different kind of shader. These stages include vertex processing, tessellation, geometry processing, and fragment processing. Understanding this pipeline is essential for optimizing shader code and achieving desired rendering effects.

To learn more about this topic, you can visit the [Wikipedia page on Shaders](https://en.wikipedia.org/wiki/Shader).
