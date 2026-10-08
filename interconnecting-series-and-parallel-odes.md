---
title: "Interconnecting Series and Parallel ODEs"
subtitle: "Local equations, connection constraints and phasors"
author: "Hob Nilre & Bo C. Herlin"
date: "2026-10-08"
abstract: |
  ODE blocks connect by sharing one terminal variable and summing the
  other. A mixed series/parallel connection yields four state equations,
  a scalar fourth-order ODE, and exact phasor formulas. Reconstruction
  preserves the internal coordinates and their initial values.
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

Let $D=d/dt$. Each block has terminal voltage $e_j$ and current $i_j$.
Orient series voltage drops along the common current, and parallel currents
in the same direction between common terminals. All $L,R,C$ parameters
are positive constants.

The same algebra applies wherever the ODEs and connection balances correspond.
Translate variables, coefficients and units with [the ODE template][template],
Sections 2--3. Its force--voltage map sends electrical series to mechanical
parallel, and electrical parallel to mechanical series.

A series LRC block $\mathcal S$ uses charge $q$:
\begin{equation}
e_s=L_sD^2q+R_sDq+\frac q{C_s},\qquad i_s=Dq.
\label{eq:series-block}
\end{equation}
A parallel CRL block $\mathcal P$ uses flux linkage $\lambda$:
\begin{equation}
i_p=C_pD^2\lambda+\frac{D\lambda}{R_p}+\frac\lambda{L_p},
\qquad e_p=D\lambda.
\label{eq:parallel-block}
\end{equation}
Either block can enter either connection. Series imposes
\begin{equation}
\boxed{i_1=i_2=i,\qquad e=e_1+e_2,}
\label{eq:series-connection}
\end{equation}
and parallel imposes
\begin{equation}
\boxed{e_1=e_2=e,\qquad i=i_1+i_2.}
\label{eq:parallel-connection}
\end{equation}
For more blocks, extend the sums and retain each internal coordinate.
These orientations also fix the signs for the terminal-power accounts in
[*Energy Ledgers for Forced Harmonic ODEs*][energy], Sections 1--2.

# A mixed interconnection

Connect $\mathcal S$ and $\mathcal P$ in series. With total voltage $e$,
common current $i$, and internal voltage $e_p$, substitute $e_s=e-e_p$
and $i_s=i_p=i$ into the local equations:
\begin{align}
L_sD^2q+R_sDq+\frac q{C_s}+D\lambda&=e,
\label{eq:mixed-first}\\
C_pD^2\lambda+\frac{D\lambda}{R_p}+\frac\lambda{L_p}&=Dq.
\label{eq:mixed-second}
\end{align}
Each block supplies the other's terminal driving quantity: $D\lambda=e_p$
and $Dq=i$.

![Schematic of the mixed connection. The series block receives $e-e_p$ and determines $i$; the parallel block receives $i$ and determines $e_p$.](figures/interconnection.pdf){#fig:connection width=95%}

\FloatBarrier

Keeping those terminal variables gives four first-order equations:
\begin{align}
Dq&=i, \nonumber\\
L_sDi&=e-R_si-\frac q{C_s}-e_p, \nonumber\\
C_pD e_p&=i-\frac{e_p}{R_p}-\frac\lambda{L_p}, \nonumber\\
D\lambda&=e_p.
\label{eq:state}
\end{align}
The state and initial data are
\begin{equation}
\boldsymbol{x}=(q,i,e_p,\lambda)^{\mathsf T},\qquad
\boldsymbol{x}(t_0)=(q_0,i_0,e_{p,0},\lambda_0)^{\mathsf T}.
\label{eq:initial-state}
\end{equation}
Connecting the terminals couples the two ODEs while retaining all four
initial coordinates.

# The connection in phasor form

For $x(t)=\operatorname{Re}(\widehat x e^{\mathrm i\omega t})$,
$\mathrm i^2=-1$ and $\omega>0$, substitute $D=\mathrm i\omega$:
\nopagebreak[4]
\begin{align}
Z_s&=\mathrm i\omega L_s+R_s+\frac1{\mathrm i\omega C_s},
&\widehat e_s&=Z_s\widehat i, \nonumber\\*
Y_p&=\mathrm i\omega C_p+\frac1{R_p}+\frac1{\mathrm i\omega L_p},
&\widehat i&=Y_p\widehat e_p.
\label{eq:local-phasors}
\end{align}
Here $Z_s$ converts current to voltage and $Y_p$ converts voltage to current.
The series constraints remain
\begin{equation}
\widehat e=Z_s\widehat i+\widehat e_p,\qquad
\widehat i=Y_p\widehat e_p.
\label{eq:phasor-connection}
\end{equation}
Writing $\Delta=1+Z_sY_p$ gives
\begin{equation}
\boxed{\widehat e_p=\frac{\widehat e}{\Delta},\qquad
\widehat i=\frac{Y_p\widehat e}{\Delta},}
\qquad \Delta\ne0.
\label{eq:phasor-solution}
\end{equation}
Recover $\widehat q=\widehat i/(\mathrm i\omega)$ and
$\widehat\lambda=\widehat e_p/(\mathrm i\omega)$. The parallel currents are
\begin{equation}
\widehat i_C=\mathrm i\omega C_p\widehat e_p,\qquad
\widehat i_R=\frac{\widehat e_p}{R_p},\qquad
\widehat i_L=\frac{\widehat e_p}{\mathrm i\omega L_p},\qquad
\widehat i_C+\widehat i_R+\widehat i_L=\widehat i.
\label{eq:branch-phasors}
\end{equation}
These are harmonic components. The full solution still needs the initial
state in \eqref{eq:initial-state}.

## Further blocks

Series voltages give $Z_{\mathrm{eq}}=\sum_jZ_j$; parallel currents give
$Y_{\mathrm{eq}}=\sum_jY_j$. Thus
\begin{equation}
\widehat e_j=\frac{Z_j}{\sum_\ell Z_\ell}\widehat e
\quad\text{(series)},\qquad
\widehat i_j=\frac{Y_j}{\sum_\ell Y_\ell}\widehat i
\quad\text{(parallel)}.
\label{eq:division}
\end{equation}
Use these quotients only with nonzero denominators. Where finite and
nonzero, $Y=1/Z$ lets a nested series/parallel group be combined from its
inner branches outward. Sum complex phasors before taking magnitudes;
at a zero denominator, check compatibility in the original linear equations.

# Elimination without losing initial data

Assume $e(t)$ is twice continuously differentiable and define
\begin{equation}
A(s)=L_ss^2+R_ss+\frac1{C_s},\qquad
B(s)=C_ps^2+\frac s{R_p}+\frac1{L_p}.
\label{eq:local-polynomials}
\end{equation}
The coupled equations are $A(D)q+D\lambda=e$ and $B(D)\lambda=Dq$.
Apply $B(D)$ to the first and use constant coefficients to commute it
with $D$:
\begin{equation}
\boxed{K(D)q=B(D)e,\qquad K(s)=A(s)B(s)+s^2.}
\label{eq:scalar}
\end{equation}
This fourth-order equation contains both local polynomials and the $s^2$
term from connecting their terminal derivatives.

Reconstruct the eliminated variables by
\begin{equation}
i=Dq,\qquad e_p=e-A(D)q,\qquad
\lambda=L_p\left(i-C_pD e_p-\frac{e_p}{R_p}\right).
\label{eq:reconstruction}
\end{equation}
The scalar equation implies $B(D)e_p=D^2q$, so differentiating the last
formula gives $D\lambda=e_p$. All original equations are recovered.

To recover the original initial state, set $q(t_0)=q_0$, $(Dq)(t_0)=i_0$ and
\begin{align}
(D^2q)(t_0)&=\frac{e(t_0)-R_si_0-q_0/C_s-e_{p,0}}{L_s}, \nonumber\\
(D^3q)(t_0)&=\frac{(De)(t_0)-R_s(D^2q)(t_0)-i_0/C_s-(D e_p)(t_0)}{L_s},
\label{eq:initial-derivatives}
\end{align}
where $(D e_p)(t_0)=(i_0-e_{p,0}/R_p-\lambda_0/L_p)/C_p$.
The four scalar initial values encode the same four internal coordinates.

Since $Z_s=A(\mathrm i\omega)/(\mathrm i\omega)$ and
$Y_p=B(\mathrm i\omega)/(\mathrm i\omega)$,
\begin{equation}
K(\mathrm i\omega)=(\mathrm i\omega)^2\Delta.
\label{eq:phasor-agreement}
\end{equation}
Hence $\widehat q=B(\mathrm i\omega)\widehat e/K(\mathrm i\omega)$ and
reconstruction give \eqref{eq:phasor-solution} wherever the denominator is nonzero.

To extend a suitable local equation, choose higher-order coefficients from
[*ODE Coefficient Synthesis*][synthesis], Sections 1--4, and reuse the terminal
constraints. Once the local equations are known, this assembles the system
without repeating mesh analysis for the full network. Phasors still use
$D=\mathrm i\omega$; added differential orders require corresponding initial
data consistent with the connection.

# References {-}

1. H. Nilre and B. C. Herlin (2026). [The ODE Template and Its Domain Equivalents][template].
2. H. Nilre and B. C. Herlin (2026). [ODE Coefficient Synthesis][synthesis].
3. H. Nilre and B. C. Herlin (2026). [Energy Ledgers for Forced Harmonic ODEs][energy].

[template]: https://github.com/hobnilre/physics-ode-template
[synthesis]: https://github.com/hobnilre/physics-ode-coefficient-synthesis
[energy]: https://github.com/hobnilre/physics-ode-energy
