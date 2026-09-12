# Tiny Fixed Function GPU
Repo for the gpu project 👍

A project made by CDI club members, a fixed function 3d graphics accelerator designed in Verilog/SystemVerilog for FPGA's on a VGA output

## Project Overview 
this is a modular, FPGA based graphics hardware project designed to be a multiphase-increased complexity of this GPU project -- future design decisions past Phase 1 are to be decided as this project is near completion 

### Things team members should learn/know 

**Phase 1** 

+ Parsing the raw 2d .obj file vertices into fixed-point (Q8.8) Look up tables (LUTs)
+ this is done through a python script so then,
+ this currently would be put into vivado directly to be read from the FPGA

+ this new information is streamed from the Geometry Engine where it preforms Matrix Transformations on each + vertex triangle. this can then be used to transform 3D points to 2D VGA-pixel coordinates 
+ Scaling, Rotation, Translation, and Perspective projection is all on the list of completion for phase 1

+ then the rasterization engine accepts these 2D coordinates from the Geometry Engine through a handshake between the Geometry and Rasterization engine. it evaluates the pixels and interpolates depth and color (more information provided form the python script before synthesis)

+ Framebuffering would be required (using BRAM) to be written over from the rasterizer, 
+ then stores the current frame/data inside said BRAM (block ram) 

+ The vGA continously reads frame data from the BRAM
+ Driving active video data and hvsync to display in 640 x 480 @ 60Hz


## Repository Structure

Will fill later


## Possible goals for phase 1 

* Python Scripting - Pre-processing stuff -- Being able to convert an .obj file into synthesized Q8.8 Fixed point LUTs into Vivado's BRAM

* Geometry Engine - Implment Matrix math for 3D-to-2D operations
Successfully execute translation scaling rotation perspective in projection

* Intermodule communication / a wrapper module : Being able to have a sort of Ready handshake interface connecting the geometry engine to the Rasterizer

* Multi-Archetecture for Rasterization:
  If there is enough time or demand, we could try and implement multi-archetectures like Bresenham, Scanline, Pineda/Edge Function, and Hierarchical/tile based. These different options to go with all have their own challenges but if here is a big enough reason to split our team up we could go for more than just one. However Pineda is most likely our choice at first.

* Memory & VGA Output:
* Instantiating a dual-port BRAM frame buffer to handle the writing from the rasterizer and then the VGA controller can read it.
* Being able to generaet stable H-V Syncs and display a rendered 3D mesh live on VGA

* Phase 2 or Further down would be - Soft core CPUs, prorammable shaders (like a cuda core) all math fixed directly inside rasterizers - No AXI streaming yet since there is no CPU or programming core yet as this project is fixed functions . 
