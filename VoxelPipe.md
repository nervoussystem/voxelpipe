# Introduction #

This is **VoxelPipe**, a voxelization library built in CUDA by
**NVIDIA Research**.

Details about the employed algorithms are given in:

  * "VoxelPipe: A Programmable Pipeline for 3d Voxelization", Jacopo Pantaleoni, High Performance Graphics 2011 - August 2011<br>   <a href='http://research.nvidia.com/publication/voxelpipe-programmable-pipeline-3d-voxelization'>http://research.nvidia.com/publication/voxelpipe-programmable-pipeline-3d-voxelization</a></li></ul>

VoxelPipe references the <a href='http://code.google.com/p/slash-sandbox/source/browse/#svn%2Ftrunk%2F%20slash-sandbox%2Fnih'>nih</a> library available at:<br>
<a href='http://code.google.com/p/slash-sandbox/'>http://code.google.com/p/slash-sandbox/</a>

The main header file defining the high level API for the library is<br>
<a href='http://code.google.com/p/voxelpipe/source/browse/trunk/src/voxelpipe/voxelpipe.h'>src/voxelpipe/voxelpipe.h</a>.<br>
The rest of the top-level [src/voxelpipe](http://code.google.com/p/voxelpipe/source/browse/#svn%2Ftrunk%2Fsrc%2Fvoxelpipe) directory is implementation specific, and is not for the weak of heart.<br>
The <a href='http://code.google.com/p/voxelpipe/source/browse#svn%2Ftrunk%2Fvoxelpipe_test%2Fsrc'>voxelpipe_test</a> subdirectory contains a minimal test program showing how to use the library.