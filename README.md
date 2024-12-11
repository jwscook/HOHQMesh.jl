# HOHQMesh.jl

[![Docs-stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://trixi-framework.github.io/HOHQMesh.jl/stable)
[![Docs-dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://trixi-framework.github.io/HOHQMesh.jl/dev)
[![Build Status](https://github.com/trixi-framework/HOHQMesh.jl/workflows/CI/badge.svg)](https://github.com/trixi-framework/HOHQMesh.jl/actions?query=workflow%3ACI)
[![Coveralls](https://coveralls.io/repos/github/trixi-framework/HOHQMesh.jl/badge.svg?branch=main)](https://coveralls.io/github/trixi-framework/HOHQMesh.jl?branch=main)
[![License: MIT](https://img.shields.io/badge/License-MIT-success.svg)](https://opensource.org/licenses/MIT)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.13959071.svg)](https://doi.org/10.5281/zenodo.13959071)

This package is a Julia frontend to the Fortran-based *High Order Hex-Quad Mesher*
(a.k.a. [**HOHQMesh**](https://github.com/trixi-framework/HOHQMesh)) created and developed by
[David A. Kopriva](https://www.math.fsu.edu/~kopriva/). It augments HOHQMesh with
[interactive functionality](https://trixi-framework.github.io/HOHQMesh.jl/stable/interactive_overview/)
that gives a user the ability to create, visualize,
and generate high-order meshes.
It further allows one to seamlessly integrate meshes generated by HOHQMesh into a Julia-based simulation workflow.
For example, running a simulation on an unstructured quadrilateral mesh
with [Trixi.jl](https://trixi-framework.github.io/Trixi.jl/stable/tutorials/hohqmesh_tutorial/).
HOHQMesh.jl is available on Linux, MacOS, and Windows.


## Installation
If you have not yet installed Julia, please [follow the instructions for your
operating system](https://julialang.org/downloads/platform/). HOHQMesh.jl works
with Julia v1.6 and above.

HOHQMesh.jl is a registered Julia package. Hence, you can install it by executing
the following commands in the Julia REPL:
```julia
julia> import Pkg; Pkg.add("HOHQMesh")
```
HOHQMesh.jl depends on the binary distribution of the
[HOHQMesh](https://github.com/trixi-framework/HOHQMesh)
mesh generator, which is available via the Julia package
[HOHQMesh_jll.jl](https://github.com/JuliaBinaryWrappers/HOHQMesh_jll.jl)
and which is automatically installed as a dependency.

## Usage
In the Julia REPL, you can load HOHQMesh with
```julia
julia> using HOHQMesh
```
and then happily generate away!

Two 2D examples `GingerbreadMan` and `NACA0012` and a 3D example `Snake` (all
from HOHQMesh itself) come delivered with this package. You can generate a
mesh for them by executing
```julia
julia> control_file = joinpath(HOHQMesh.examples_dir(), "GingerbreadMan.control")

julia> output = generate_mesh(control_file)
```
You will then find the resulting output files (mesh, plot file, statistics) in
the designated output directory, which defaults to `out`. The
`GingerbreadMan.control` file will yield the following mesh,

![gingerbreadman_with_edges_400px](https://user-images.githubusercontent.com/3637659/117241938-80f4ee80-ae34-11eb-854a-ebebcd0b9d88.png)

while the 3D file `Snake.control` produces this mesh:

![snake_400px](https://user-images.githubusercontent.com/3637659/117241963-8ce0b080-ae34-11eb-9b79-d091807d9a23.png)

Examples scripts of interactive mesh generation tools are available in the
[examples/](https://github.com/trixi-framework/HOHQMesh.jl/tree/main/examples) subdirectory.
These example scripts are prefaced with the phrase `interactive_`.
There is a brief summary at the top of each `interactive` example script that describes
the mesh it will create and the features of HOHQMesh it uses.
An example script can be executed from a Julia REPL session with an `include(...)` statement, e.g.,
```julia
julia> include(joinpath(HOHQMesh.examples_dir(), "interactive_outer_box_two_circles.jl"))
```
The resulting output mesh and plot files are saved in the output directory `out` as
designated in the example script. Mesh statistics are printed to the screen.

The interactive functionality uses [Makie.jl](https://github.com/JuliaPlots/Makie.jl/)
to visualize the boundary curves and mesh from the interactive tool. A Makie backend, such as
[GLMakie](https://github.com/JuliaPlots/GLMakie.jl/), can
be loaded in addition to HOHQMesh
```julia
julia> using Pkg; Pkg.add("GLMakie")
julia> using GLMakie
```
Now, running the example script produces a figure in addition to the mesh and plot
files that are saved and the output of mesh statistics to the screen.

![box_two_circles](https://user-images.githubusercontent.com/25242486/174244295-40d31df3-981e-4375-bc3a-af0a43737710.png)

Further explanation of the interactive functionality can be found [here](https://trixi-framework.github.io/HOHQMesh.jl/stable/interactive_overview/).
Additional examples are available in the [Tutorials](https://trixi-framework.github.io/HOHQMesh.jl/stable/tutorials/introduction/).


## Referencing
If you use HOHQMesh.jl in your own research, please cite the following article:
```bibtex
@article{kopriva2024hohqmesh:joss,
  title={{HOHQM}esh: An All Quadrilateral/Hexahedral Unstructured Mesh Generator for High Order Elements},
  author={David A. Kopriva and Andrew R. Winters and Michael Schlottke-Lakemper
          and Joseph A. Schoonover and Hendrik Ranocha},
  year={2024},
  journal={Journal of Open Source Software},
  doi={10.21105/joss.07476},
  volume = {9},
  number = {104},
  pages = {7476},
  publisher = {The Open Journal}
}
```
In addition, you can also directly refer to this repository as
```bibtex
@misc{kopriva2024hohqmeshjl,
  title={{HOHQM}esh.jl: A Julia frontend to the Fortran-based HOHQMesh mesh generator for high order elements},
  author={Kopriva, David A and Winters, Andrew R and Schlottke-Lakemper, Michael and Ranocha, Hendrik},
  year={2024},
  howpublished={\url{https://github.com/trixi-framework/HOHQMesh.jl}},
  doi={10.5281/zenodo.13959071}
}
```


## Authors
HOHQMesh.jl is maintained by the
[Trixi.jl authors](https://github.com/trixi-framework/Trixi.jl/blob/main/AUTHORS.md).
Its principal developers are [Andrew Winters](https://liu.se/en/employee/andwi94)
(Linköping University, Sweden) and [David A. Kopriva](https://www.math.fsu.edu/~kopriva/).
The *HOHQMesh* mesh generator itself is developed by David A. Kopriva.


## License and contributing
HOHQMesh.jl is licensed under the MIT license (see [LICENSE.md](LICENSE.md)).
*HOHQMesh* itself is also available under the MIT license.
Since HOHQMesh is an open-source project, we are very happy to accept contributions
from the community. Please refer to [CONTRIBUTING.md](CONTRIBUTING.md) for more details.
To get in touch with the developers,
[join us on Slack](https://join.slack.com/t/trixi-framework/shared_invite/zt-sgkc6ppw-6OXJqZAD5SPjBYqLd8MU~g)
or [create an issue](https://github.com/trixi-framework/HOHQMesh.jl/issues/new).


## Acknowledgements
The authors would like to thank David A. Kopriva for making the sources of
*HOHQMesh* available as open source, and for assisting with making it work with
Julia.
