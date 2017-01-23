# TopologyTracer
MPI-parallelized postprocessor for instrumented grain growth simulations of polycrystals

* Collect growth curves of individual grains
* Correlate the evolution of single grains with those of their neighbors

run command

$mpiexec -n 1 topotracer2d3d_intel16 simid paramters.xml

Use matlab scripts to reload binary files and plot grain traces etc.
