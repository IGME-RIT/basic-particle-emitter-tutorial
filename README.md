# Basic Particle Emitter Tutorial

This examples uses the code established in the OBJ Loading example to demonstrate a basic particle effect.

# About

On the CPU side, the	program tracks arrays of particles stored in particle systems managed by the particle manager. Every frame, the program updates the positions and ages of the particles being emitted and sends that data to a buffer on the GPU. The GPU runs a shader program	that uses a geometry stage to take each of the particles represented by positions and makes them into renderable quads (or culls them depending on their age) to be sent on to the fragment shader.

There are 6 static component classes that make up the base functionality for this example:

1. RenderManager
	- This class maintains the display list for the scene being rendered and thus handles the processes of updating and drawing all of the RenderObjects that have been instantiated in the scene.

2. CameraManager
	- This class maintains data relating to the view and projection matrices used in the rendering pipeline. It also handles updating this data based on user input.

3. InputManager
	- This class maintains data for the current state of user input for the mouse and keyboard.

4. LightingManager
	- This class maintains data for an array of eight lights, each possessing a transform, color and power, handles the updating thereof and maintains GPU-side buffers reflecting this data for use in the shaders.

5. ResourceManager
	- This class maintains all the data from external sources necessary to run the program. In this instance, this includes OBJ loading, parsing, and storage, VAO, VBO, and EBO generation and storage, shader loading, compiling and linking, and uniform buffer object generation, binding and storage.

6. ParticleManager
	- This class maintains all of the data relating to the particle effects in the scene. It contains an array of particle systems which in turn hold arrays of particles which contain the positions, colors, ages, and velocities of each particle in the system.

RenderObject
	- Tracks the instance of an object that can be drawn to the screen. Contains data for transforms, a mesh, a shader, drawing mode (eg triangles, lines), and a layer. The layer is a value that can be used to mask certain objects from a draw call. The object has a layer which is some power	of 2 and then there is a mask for the draw call which is a 32 bit number. A bit-wise & between these numbers decides whether or not the object in question is drawn.

###Shaders
- Now use uniform buffer objects for receiving uniform data.

- vShader.glsl
	- Through shader, nothing fancy

- fShader.glsl
	- Applies a Phong lighting model based on the data sent from the lighting manager, functions the same as the Phong shader from the geometric lighting improved example.

- particleVert.glsl
	- Applies projection and view matrices to the particle positions, does not use the model matrix as it was already applied on the CPU side.

- particleGeo.glsl
	- Receives position values from the vertex shader and converts them into quads and adds texture coordinates.

- particleFrag.glsl
	- Samples the bound texture based on coordinates from the geometry shader and adds the color from the vertex buffer.

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
