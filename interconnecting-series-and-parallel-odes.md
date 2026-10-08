---
title: "Interconnecting Series and Parallel ODEs"
subtitle: "Local equations, connection constraints and phasors"
author: "Hob Nilre & Bo C. Herlin"
date: "2026-10-08"
abstract: |
  Series and parallel ODE blocks connect through shared terminal variables
  and signed sums. We derive these constraints, assemble a mixed connection,
  and retain its four initial coordinates. Substitution of
  $D=\mathrm i\omega$ gives the corresponding phasor equations.
  Exact elimination recovers the same result as a scalar ODE.
keywords:
  - ordinary differential equations
  - series and parallel interconnection
  - phasors
  - elimination
---

\begingroup\scriptsize
\noindent PDF created: \pdfbuildtimestamp\par
\noindent Latest on GitHub: \url{https://github.com/hobnilre/physics-ode-interconnect-ser-par}\par
\endgroup

# Local equations and connection rules

Use electrical connection names and let $D=d/dt$. A block has terminal
voltage $e_j$ and current $i_j$. Orient series voltage drops along the
common current; orient parallel branch currents in the same direction
between the common terminals. All $L,R,C$ parameters below are positive
constants.

The interconnection algebra applies in any domain with corresponding ODEs
and connection balances. Map the variables, coefficients and units using
[*The ODE Template and Its Domain Equivalents*][template], Sections 2--3;
higher-order extensions and phasor substitution then follow the same algebra.
Follow the mapped common and summed quantities: electrical series corresponds
to mechanical parallel, and vice versa, under the template's force--voltage
correspondence.

For a series LRC block $\mathcal S$, charge $q$ gives
\begin{equation}
e_s=L_sD^2q+R_sDq+\frac{q}{C_s},\qquad i_s=Dq.
\label{eq:series-block}
\end{equation}
For a parallel CRL block $\mathcal P$, flux linkage $\lambda$ gives
\begin{equation}
i_p=C_pD^2\lambda+\frac{D\lambda}{R_p}
+\frac{\lambda}{L_p},\qquad e_p=D\lambda.
\label{eq:parallel-block}
\end{equation}
The terminal driving quantity of either ODE is supplied by the rest
of the connected system.

For two blocks, a series connection imposes
\begin{equation}
\boxed{i_1=i_2=i,\qquad e=e_1+e_2,}
\label{eq:series-connection}
\end{equation}
whereas a parallel connection imposes
\begin{equation}
\boxed{e_1=e_2=e,\qquad i=i_1+i_2.}
\label{eq:parallel-connection}
\end{equation}
The same balances apply to any finite number of blocks.

Either block type can enter either connection. Apply the common-variable
and sum constraints at each junction, retaining the internal coordinates.

# A mixed interconnection

Connect $\mathcal S$ and $\mathcal P$ in series, with total voltage
$e(t)$, common current $i(t)$ and internal voltage $e_p(t)$.
Thus $e_s=e-e_p$ and $i_s=i_p=i$. Inserting these relations into
\eqref{eq:series-block}--\eqref{eq:parallel-block} gives
\begin{align}
L_sD^2q+R_sDq+\frac q{C_s}+D\lambda&=e,
\label{eq:mixed-first}\\
C_pD^2\lambda+\frac{D\lambda}{R_p}+\frac\lambda{L_p}&=Dq.
\label{eq:mixed-second}
\end{align}
The term $D\lambda$ in the first equation is the common voltage of
the parallel block. The term $Dq$ in the second is the common current
of the series block.

![Schematic of the equation interconnection. The series block receives $e-e_p$ and determines $i$; the parallel block receives $i$ and determines $e_p$. The return path enforces $e_s=e-e_p$.](figures/interconnection.pdf){#fig:connection width=95%}

\FloatBarrier

To retain all initial coordinates, put $i=Dq$ and $e_p=D\lambda$.
The coupled equations become
\begin{align}
Dq&=i, \nonumber\\
L_sDi&=e-R_si-\frac q{C_s}-e_p, \nonumber\\
C_pD e_p&=i-\frac{e_p}{R_p}-\frac\lambda{L_p}, \nonumber\\
D\lambda&=e_p.
\label{eq:state}
\end{align}
This is an explicit system of four first-order ODEs for
\begin{equation}
\boldsymbol{x}=(q,i,e_p,\lambda)^{\mathsf T},\qquad
\boldsymbol{x}(t_0)=(q_0,i_0,e_{p,0},\lambda_0)^{\mathsf T}.
\label{eq:initial-state}
\end{equation}
The connection passes one block's output into the other block's
equation. Their derivatives and the four initial coordinates remain
part of the assembled system.

# The same connection using phasors

Use the template's convention
$x(t)=\operatorname{Re}(\widehat x e^{\mathrm i\omega t})$, $\omega>0$,
so $D\mapsto\mathrm i\omega$. The two local equations give
\nopagebreak[4]
\begin{align}
Z_s(\omega)&=\mathrm i\omega L_s+R_s+\frac1{\mathrm i\omega C_s},
&\widehat e_s&=Z_s\widehat i, \nonumber\\*
Y_p(\omega)&=\mathrm i\omega C_p+\frac1{R_p}
+\frac1{\mathrm i\omega L_p},
&\widehat i&=Y_p\widehat e_p.
\label{eq:local-phasors}
\end{align}
Here $Z_s$ multiplies current to give voltage, while $Y_p$ multiplies
voltage to give current. The connection equations retain their form:
\begin{equation}
\widehat e=Z_s\widehat i+\widehat e_p,\qquad
\widehat i=Y_p\widehat e_p.
\label{eq:phasor-connection}
\end{equation}
Substituting the second into the first gives
\begin{equation}
\Delta(\omega)=1+Z_sY_p,\qquad
\boxed{\widehat e_p=\frac{\widehat e}{\Delta},\qquad
\widehat i=\frac{Y_p\widehat e}{\Delta},}
\quad \Delta\ne0.
\label{eq:phasor-solution}
\end{equation}
The internal coordinate phasors are
$\widehat q=\widehat i/(\mathrm i\omega)$ and
$\widehat\lambda=\widehat e_p/(\mathrm i\omega)$.
Within the parallel block the three currents are
\begin{equation}
\widehat i_C=\mathrm i\omega C_p\widehat e_p,\qquad
\widehat i_R=\frac{\widehat e_p}{R_p},\qquad
\widehat i_L=\frac{\widehat e_p}{\mathrm i\omega L_p},
\qquad
\widehat i_C+\widehat i_R+\widehat i_L=\widehat i.
\label{eq:branch-phasors}
\end{equation}
These formulas describe the harmonic component. Initial coordinates
for the full time-dependent solution remain those of \eqref{eq:state}.

## Combining further blocks

For any series group with $\widehat e_j=Z_j\widehat i$, summation
gives $Z_{\mathrm{eq}}=\sum_j Z_j$. For any parallel group with
$\widehat i_j=Y_j\widehat e$, summation gives
$Y_{\mathrm{eq}}=\sum_jY_j$. The individual phasors follow as
\begin{equation}
\widehat e_j=\frac{Z_j}{\sum_\ell Z_\ell}\widehat e
\quad\text{(series)},\qquad
\widehat i_j=\frac{Y_j}{\sum_\ell Y_\ell}\widehat i
\quad\text{(parallel)}.
\label{eq:division}
\end{equation}
These quotients require nonzero denominators. Where finite and
nonzero, $Y=1/Z$ converts between the two descriptions, so a nested
series/parallel group can be combined from its inner branches outward.
Sum complex phasors before taking magnitudes. At a zero denominator,
retain the original linear equations and check their compatibility.

# Eliminating the internal coordinates

For a scalar reduction, assume that $e(t)$ is twice continuously
differentiable. Define the two local polynomials
\begin{equation}
A(s)=L_ss^2+R_ss+\frac1{C_s},\qquad
B(s)=C_ps^2+\frac s{R_p}+\frac1{L_p}.
\label{eq:local-polynomials}
\end{equation}
Equations \eqref{eq:mixed-first}--\eqref{eq:mixed-second} read
$A(D)q+D\lambda=e$ and $B(D)\lambda=Dq$.
Apply $B(D)$ to the first. Constant coefficients allow $B(D)$ and
$D$ to commute, giving
\begin{equation}
\boxed{K(D)q=B(D)e,\qquad K(s)=A(s)B(s)+s^2.}
\label{eq:scalar}
\end{equation}
The fourth-order polynomial is
\begin{align}
K(s)={}&L_sC_ps^4+
\left(\frac{L_s}{R_p}+R_sC_p\right)s^3 \nonumber\\*
&+\left(\frac{L_s}{L_p}+\frac{R_s}{R_p}
+\frac{C_p}{C_s}+1\right)s^2 \nonumber\\*
&+\left(\frac{R_s}{L_p}+\frac1{C_sR_p}\right)s
+\frac1{C_sL_p}.
\label{eq:expanded}
\end{align}
Its product term comes from the two local ODEs; the additional $s^2$
comes from connecting their terminal derivatives.

Working with ODE blocks also makes higher-order extensions easier to
assemble where suitable. Construct coefficients using
[*ODE Coefficient Synthesis*][synthesis], Sections 1--4, and insert them
into a block's local equation. Once the local block equations are known,
assemble and extend the system using the series/parallel ODE connection
rules instead of repeating mesh analysis for the full network.
For phasors, substitute $D=\mathrm i\omega$ in the extended
polynomial. Any increase in differential order requires the corresponding
initial data, consistent with the connection constraints.

For the mixed connection above, the eliminated variables are reconstructed by
\begin{equation}
i=Dq,\qquad e_p=e-A(D)q,\qquad
\lambda=L_p\left(i-C_pD e_p-\frac{e_p}{R_p}\right).
\label{eq:reconstruction}
\end{equation}
Equation \eqref{eq:scalar} implies $B(D)e_p=D^2q$; differentiating
the last formula then gives $D\lambda=e_p$. Thus reconstruction
satisfies the original coupled equations.

To match the initial state in \eqref{eq:initial-state}, set
$q(t_0)=q_0$ and $(Dq)(t_0)=i_0$, then use
\begin{align}
(D^2q)(t_0)&=\frac{e(t_0)-R_si_0-q_0/C_s-e_{p,0}}{L_s}, \nonumber\\
(D^3q)(t_0)&=\frac{(De)(t_0)-R_s(D^2q)(t_0)-i_0/C_s-(D e_p)(t_0)}{L_s},
\label{eq:initial-derivatives}
\end{align}
where $(D e_p)(t_0)=(i_0-e_{p,0}/R_p-\lambda_0/L_p)/C_p$.
The four scalar initial values therefore encode the same four
coordinates as the coupled system.

Finally, $Z_s=A(\mathrm i\omega)/(\mathrm i\omega)$ and
$Y_p=B(\mathrm i\omega)/(\mathrm i\omega)$ imply
\begin{equation}
K(\mathrm i\omega)=(\mathrm i\omega)^2\Delta(\omega).
\label{eq:phasor-agreement}
\end{equation}
Consequently $\widehat q=B(\mathrm i\omega)\widehat e/K(\mathrm i\omega)$,
together with \eqref{eq:reconstruction}, gives exactly
\eqref{eq:phasor-solution} whenever its denominator is nonzero.
The scalar ODE and the phasor formulas are two reductions of the
same local equations and connection constraints. The additional step
from signed voltage-current products to work is developed in
[*Energy Ledgers for Forced Harmonic ODEs*][energy], Parts 1 and 2.

# References {-}

1. H. Nilre and B. C. Herlin (2026). [The ODE Template and Its Domain Equivalents][template].
2. H. Nilre and B. C. Herlin (2026). [ODE Coefficient Synthesis][synthesis].
3. H. Nilre and B. C. Herlin (2026). [Energy Ledgers for Forced Harmonic ODEs][energy].

[template]: https://github.com/hobnilre/physics-ode-template
[synthesis]: https://github.com/hobnilre/physics-ode-coefficient-synthesis
[energy]: https://github.com/hobnilre/physics-ode-energy
