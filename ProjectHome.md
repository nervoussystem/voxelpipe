VoxelPipe is a real-time CUDA voxelization library published by NVIDIA Research.

The library provides a highly flexible and efficient software pipeline for programmable triangle voxelization.
The pipeline, entirely written in CUDA, supports both fully conservative and thin voxelizations, multiple boolean, floating point, vector-typed render targets, user-defined vertex and fragment shaders, and a bucketing mode which can be used to generate 3D A-buffers containing the entire list of fragments belonging to each voxel.

The algorithms it relies on are described in:

"VoxelPipe: A Programmable Pipeline for 3d Voxelization", Jacopo Pantaleoni, High Performance Graphics 2011 - August 2011

http://research.nvidia.com/publication/voxelpipe-programmable-pipeline-3d-voxelization