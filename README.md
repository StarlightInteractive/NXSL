# NXSL
NXSL (Nexus Shader Language) is an open intermediate format for storing unified GLSL shaders for use in the Nexus platform.

## Is it actually a "shader language"?
No. By definition, NXSL is not a shader language. Rather, NXSL is simply a wrapper for storing multiple shaders (in our case, Fragment, Vertex and Compute shaders in GLSL) in a single unified file for ease of storage and organisational purposes

## NXSL Format
NXSL's formatting was designed from the ground up to be simple, yet modular. As a result we chose a directive-oriented approach. This design choice allows shader developers to focus more on writing their shaders, and less on writing unneccessary lines of code.

Take this unlit, constant color shader as an example.

```nxsl
::shaderfmt GLSL/4.6 // The format of the shader in Type/Version format.
::shader "Example/Unlit Color" // The path where a user will be able to find your shader in the Platform's UI

::region fragment // Inform the compiler that the upcoming shader is a Fragment shader.
out vec4 FragColor;
void main()
{
    FragColor = vec4(1.0f, 0.5f, 0.2f, 1.0f);
}
::region vertex // Inform the compiler that the upcoming shader is a Vertex shader.
layout (location = 0) in vec3 aPos;
void main()
{
    gl_Position = vec4(aPos.x, aPos.y, aPos.z, 1.0);
}
::endregion // Inform the compiler that we're at the end of the file. This can be used between regions too.
```
