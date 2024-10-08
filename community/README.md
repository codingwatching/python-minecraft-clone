# Community

*TODO* It would be cool to make a video to showcase community at some point and link it here!

The `community` directory is for experiments & contributions made by other people on the latest tutorial's code (see PR [#29](https://github.com/obiwac/python-minecraft-clone/pull/29)).
It more generally extends the project with functionality I've yet to cover in a tutorial or that I don't intend on covering at all.

Anyone (you included!) is more than welcome to open a PR to add their own contribution, be it a bug fix, a new build in the world save, or a new feature entirely!

Characteristic contributions are contributions which add something to the code -- bugfixes will get merged to the source of all episodes if relevant to them.

The community has several features and options that can be toggled in `src/options.py`:

- Render Distance: At what distance (in chunks) should chunks stop being rendered
- FOV: Camera field of view

- Indirect Rendering: Alternative way of rendering that has less overhead but is only supported on devices supporting OpenGL 4.2
- Advanced OpenGL: Rudimentary occlusion culling using hardware occlusion queries, however it is not performant and will cause pipeline stalls and decrease performance on most hardware - mostly for testing if it improves framerate
- Chunk Updates: Chunk updates per chunk every tick - 1 gives the best performance and best framerate, however, as Python is an slow language, 1 may increase chunk building time by an ludicrous amount
- Vsync: Vertical sync, may yield smoother framerate but bigger frame times and input lag
- Max CPU Ahead frames: Number of frames that the CPU can go ahead of a frame before syncing with the GPU by waiting for it to complete the execution of the command buffer, using `glClientWaitSync()`
- Smooth FPS: Legacy CPU/GPU sync by forcing the flushing and completion of command buffer using `glFinish()`, not recommended - similar to setting Max CPU Ahead Frames to 0. Mostly for testing whether it makes any difference with `glClientWaitSync()`

- Smooth lighting: Smoothes the light of each vertex to achieve a linear interpolation of light on each fragment, hence creating a smoother light effect - it also adds ambient occlusion, to simulate light blocked by opaque objects (chunk update/build time will be severely affected by this feature)
- Fancy translucency: Better translucency blending, avoid weird looking artefacts - disable on low-end hardware
- Mipmap (minification filtering): Texture filtering used on higher distances. Default is `GL_NEAREST` (no filtering) (more info in `options.py`)
- Colored lighting: Uses an alternative shader program to achieve a more colored lighting; it aims to look similar to Beta 1.8+ (no performance loss should be incurred)
- Antialiasing: Experimental feature
