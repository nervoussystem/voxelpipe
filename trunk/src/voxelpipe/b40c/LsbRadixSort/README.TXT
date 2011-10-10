
BUILD NOTES:
	
	Important notes when building or integrating this code:

	1) Device specialization and kernel bloat.  For performance, it is 
	   critically important to have your compiler target specific compute-
	   capabilities (i.e., using -gencode to generate specific versions of PTX 
	   or cubin).  We aggressively optimize for different SM versions and 
	   input key/value types.  For example, letting the compiler target PTX 
	   1.0 (often the default for many projects) will result in a ~37% 
	   slowdown for SM 2.0 devices because the SM1.0 generated code is 
	   inappropriately tuned for SM2.0 devices.
	   
	   Ideally you should generate your code for the specific compute-
	   capability(ies) (or SM architectures) that you will ultimately target.  
	   When they are not knowable, the alternative of compiling for all 
	   platforms (e.g., compute_10, 13, 20, etc.) unfortunately results in 
	   kernel (and binary bloat). Template expansion also generates separate 
	   sorting kernels for each unique key type (or key-value type pairing) 
	   used by the encompassing application.   
	   
	2) Register pressure.  This code is aggressively tuned to match register-
	   file sizes, particularly codepaths designed for GF10x (Fermi) devices.  
	   Register pressure is pushed to the limit, and we obtain our published 
	   performance results by compiling for:
	
		- 32-bit device pointers (even for 64-bit hosts).  When compiled for 
		  64-bit device pointers, the launch bounds result in the register 
		  allocator having to make some spills to lmem in order to maintain 
		  our desired occupancy.  This currently incurs a ~10% performance 
		  overhead.
		  
		- Disabling the ABI for CUDA 3.1+.  The ABI introduces a calling-
		  convention for kernel-code that introduces a program stack (allowing 
		  function pointers, recursion, etc.).  Unfortunately this imposes an 
		  additional register overhead (1 register).  We note that the ABI is 
		  unnecessary for our implementation because it aggressively inlines 
		  all subroutines.  If the ABI is enabled, however, the resultant spills 
		  to lmem currently incur a ~3% overhead. 
	
	3) ECC on Fermi (e.g., Tesla C2050).  Unaligned or partial writes are 
	   prohibitively expensive when ECC is enabled on SM2.0 (e.g., the default 
	   SM2.0 code will experience up to a 50% slowdown).  For a workaround, see 
	   the example Makefile for a compiler-define that enables logic that 
	   programmatically coalesces unaligned scatters on SM2.0 (i.e., -DFERMI_ECC
	   flag).  This is non-ideal, but only results in a ~35% slowdown.
	   
	
	The accompanying sorting examples should build under most Linux 
	platforms using CUDA Toolkit 3.0 or higher.
	
	For more information, see our Google Code project site: 
	http://code.google.com/p/back40computing/

AUTHORS' REQUEST: 

	If you use|reference|benchmark this code, please cite our Technical 
	Report (http://www.cs.virginia.edu/~dgm4d/papers/RadixSortTR.pdf):
	
	@TechReport{ Merrill:Sorting:2010,
       	author = "Duane Merrill and Andrew Grimshaw",
       	title = "Revisiting Sorting for GPGPU Stream Architectures",
       	year = "2010",
       	institution = "University of Virginia, Department of Computer Science",
       	address = "Charlottesville, VA, USA",
       	number = "CS2010-03"
	}
	
	Thanks!
