About
=====

Quantum++ is a modern C++11 general purpose quantum computing library, composed 
solely of template header files. Quantum++ is written in standard C++11 and 
has very low external dependencies, using only the 
[Eigen 3](http://eigen.tuxfamily.org) linear algebra header-only template 
library and, if available, the [OpenMP](http://openmp.org/) multi-processing 
library. 

Quantum++ is not restricted to qubit systems or specific quantum 
information processing tasks, being capable of simulating arbitrary quantum 
processes. The main design factors taken in consideration were the ease of 
use, high portability, and high performance. The library's simulation
capabilities are only restricted by the amount of available physical memory. 
On a typical machine (Intel i5 8Gb RAM) Quantum++ can successfully simulate 
the evolution of 25 qubits in a pure state or of 12 qubits in a mixed state 
reasonably fast.

To report any bugs or ask for additional features/enhancements, please 
[submit an issue](https://github.com/vsoftco/qpp/issues) with an appropriate 
label.

If you are interesting in contributing to this project, feel free to contact
me. Alternatively, create a custom branch, add your contribution, then 
finally create a pull request. If I accept the pull request, I will merge 
your custom branch with the latest development branch. The latter will 
eventually be merged into a future release version.
To contribute, you need to have a solid knowledge of C++ (preferably C++11), 
including templates and the standard library, a basic knowledge of 
quantum computing and linear algebra, and working experience with 
[Eigen 3](http://eigen.tuxfamily.org).

For additional [Eigen 3](http://eigen.tuxfamily.org) documentation 
see <http://eigen.tuxfamily.org/dox/>. For a simple 
[Eigen 3](http://eigen.tuxfamily.org) quick ASCII reference see
<http://eigen.tuxfamily.org/dox/AsciiQuickReference.txt>.

Copyright (c) 2013 - 2018 Vlad Gheorghiu, vgheorgh AT gmail DOT com.

---
Quantum++ is licensed under the MIT license, see COPYING for the full terms 
and conditions of the license.

Acknowledgements
================
I acknowledge financial support from Industry Canada and from the
Natural Sciences and Engineering Research Council of Canada (NSERC). I
thank Kassem Kalach for carefully reading this documentation and providing
useful suggestions.