# Sammankoppling av serie- och parallellkopplade ODE-block

[Läs artikeln (PDF)](interconnecting-series-and-parallel-odes-sv.pdf) · [Artikeltext](interconnecting-series-and-parallel-odes-sv.md) · [Engelskt original](../interconnecting-series-and-parallel-odes.md)

Koppla samman ODE-block genom att låta en terminalstorhet vara
gemensam och summera den andra. En blandad koppling ger fyra
tillståndsekvationer, exakta fasorformler och en skalär ODE
av fjärde ordningen som bevarar alla begynnelsekoordinater.

[Domänavbildningarna](https://github.com/hobnilre/physics-ode-template)
för över samma regler till motsvarande mekaniska ekvationer.
[Koefficientsyntes](https://github.com/hobnilre/physics-ode-coefficient-synthesis)
kan utvidga lämpliga lokala block utan att maskanalysen behöver
upprepas för hela nätverket. De valda terminalorienteringarna
bestämmer också tecknen för
[effekt och arbete](https://github.com/hobnilre/physics-ode-energy).
