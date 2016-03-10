# Normal Mapping Tutorial

This program serves to demonstrate the concept of ray tracing.

# About

This builds off a previous Intermediate Ray Tracer, adding in reflections. There are four point lights, specular and diffuse lighting, and shadows. It is important to note that the light positions and triangles being rendered are all hardcoded in the shader itself. Usually, you would pass those values into the Fragment Shader via a Uniform Buffer.

WARNING: Framerate may suffer depending on your hardware. This is a normal problem with Ray Tracing. If it runs too slowly, try removing the second cube from the triangles array in the Fragment Shader (and also adjusting NUM_TRIANGLES accordingly). There are many optimization techniques out there, but ultimately Ray Tracing is not typically used for Real-Time rendering.

# Setup

In order to setup, run the following in a shell, then open the project in your preferred editor. Windows setup has been configured for use with Visual Studio.

Windows:
```
cd path/to/folder
setup.cmd
```
Linux:
```
cd path/to/folder
./setup
```

# Credits

For more reading, check out [ray tracing with compute shaders](https://github.com/LWJGL/lwjgl3-wiki/wiki/2.6.1.-Ray-tracing-with-OpenGL-Compute-Shaders-(Part-I))
