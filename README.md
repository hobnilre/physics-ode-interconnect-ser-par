# Interconnecting Series and Parallel ODEs

[Read the article (PDF)](interconnecting-series-and-parallel-odes.pdf) · [Manuscript](interconnecting-series-and-parallel-odes.md)

Connect ODE blocks by sharing one terminal variable and summing the other.
A mixed connection gives four state equations, exact phasor formulas and
a scalar fourth-order ODE that retains all initial coordinates.

The [domain mappings](https://github.com/hobnilre/physics-ode-template)
carry the same rules into corresponding mechanical equations.
[Coefficient synthesis](https://github.com/hobnilre/physics-ode-coefficient-synthesis)
can extend suitable local blocks without repeating mesh analysis for the
full network. The chosen terminal orientations also set the signs for
[power and work](https://github.com/hobnilre/physics-ode-energy).

## Build

Install GNU Make, GNU Coreutils, Pandoc, XeLaTeX, the TeX Gyre fonts and the
LaTeX packages used by the included preambles and figures. Run `make pdf`;
all build inputs are in this repository.

The title date stays fixed; the PDF creation timestamp advances on rebuild.
Use `make -B pdf` to force a rebuild. Intermediates go to ignored `build/`,
or to the path set by `BUILD_DIR`. `make clean` removes that directory and
keeps the article PDF and figure assets.
