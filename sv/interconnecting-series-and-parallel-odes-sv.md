---
title: "Sammankoppling av serie- och parallellkopplade ODE-block"
subtitle: "Lokala ekvationer, kopplingsvillkor och fasorer"
author: "Hob Nilre & Bo C. Herlin"
date: "2026-10-08"
lang: sv
abstract: |
  ODE-block kopplas samman genom att en terminalstorhet är gemensam
  och den andra summeras. En blandad serie- och parallellkoppling ger
  fyra tillståndsekvationer, en skalär ODE av fjärde ordningen och
  exakta fasorformler. Rekonstruktion bevarar de interna koordinaterna
  och deras begynnelsevärden.
keywords:
  - ordinära differentialekvationer
  - serie- och parallellkoppling
  - fasorer
  - elimination
---

\begingroup\scriptsize
\noindent PDF created: \pdfbuildtimestamp\par
\noindent Latest on GitHub: \url{https://github.com/hobnilre/physics-ode-interconnect-ser-par}\par
\noindent Svensk översättning av \href{https://github.com/hobnilre/physics-ode-interconnect-ser-par/blob/main/interconnecting-series-and-parallel-odes.md}{den engelska originalartikeln}.\par
\endgroup

# Lokala ekvationer och kopplingsregler

Låt $D=d/dt$. Varje block har terminalspänningen $e_j$ och strömmen $i_j$.
Orientera seriekopplingens spänningsfall längs den gemensamma strömmen
och parallellkopplingens strömmar i samma riktning mellan de gemensamma
terminalerna. Alla $L,R,C$-parametrar är positiva konstanter.

Samma algebra gäller överallt där ODE:erna och kopplingsbalanserna
motsvarar varandra. Omvandla variabler, koefficienter och enheter med
[ODE-mallen][template], avsnitt 2--3. Dess kraft–spänningsavbildning för
elektrisk seriekoppling till mekanisk parallellkoppling och elektrisk
parallellkoppling till mekanisk seriekoppling.

Ett seriekopplat LRC-block $\mathcal S$ använder laddningen $q$:
\begin{equation}
e_s=L_sD^2q+R_sDq+\frac q{C_s},\qquad i_s=Dq.
\label{eq:series-block}
\end{equation}
Ett parallellkopplat CRL-block $\mathcal P$ använder flödeslänkningen
$\lambda$:
\begin{equation}
i_p=C_pD^2\lambda+\frac{D\lambda}{R_p}+\frac\lambda{L_p},
\qquad e_p=D\lambda.
\label{eq:parallel-block}
\end{equation}
Båda blocktyperna kan ingå i båda kopplingarna. Seriekoppling kräver
\begin{equation}
\boxed{i_1=i_2=i,\qquad e=e_1+e_2,}
\label{eq:series-connection}
\end{equation}
och parallellkoppling kräver
\begin{equation}
\boxed{e_1=e_2=e,\qquad i=i_1+i_2.}
\label{eq:parallel-connection}
\end{equation}
För fler block utvidgas summorna och varje intern koordinat behålls.
Dessa orienteringar bestämmer också tecknen i redovisningen av
terminaleffekt i [*Energy Ledgers for Forced Harmonic ODEs*][energy],
avsnitt 1--2.

# En blandad sammankoppling

Koppla $\mathcal S$ och $\mathcal P$ i serie. Med totalspänningen $e$,
den gemensamma strömmen $i$ och den interna spänningen $e_p$, sätt in
$e_s=e-e_p$ och $i_s=i_p=i$ i de lokala ekvationerna:
\begin{align}
L_sD^2q+R_sDq+\frac q{C_s}+D\lambda&=e,
\label{eq:mixed-first}\\
C_pD^2\lambda+\frac{D\lambda}{R_p}+\frac\lambda{L_p}&=Dq.
\label{eq:mixed-second}
\end{align}
Varje block ger den storhet som driver det andra blockets terminal:
$D\lambda=e_p$ och $Dq=i$.

![Schema över den blandade kopplingen. Serieblocket tar emot $e-e_p$ och bestämmer $i$; parallellblocket tar emot $i$ och bestämmer $e_p$.](figures/interconnection.pdf){#fig:connection width=95%}

\FloatBarrier

Om dessa terminalvariabler behålls fås fyra ekvationer av första ordningen:
\begin{align}
Dq&=i, \nonumber\\
L_sDi&=e-R_si-\frac q{C_s}-e_p, \nonumber\\
C_pD e_p&=i-\frac{e_p}{R_p}-\frac\lambda{L_p}, \nonumber\\
D\lambda&=e_p.
\label{eq:state}
\end{align}
Tillståndet och begynnelsedata är
\begin{equation}
\boldsymbol{x}=(q,i,e_p,\lambda)^{\mathsf T},\qquad
\boldsymbol{x}(t_0)=(q_0,i_0,e_{p,0},\lambda_0)^{\mathsf T}.
\label{eq:initial-state}
\end{equation}
Sammankopplingen av terminalerna kopplar ihop de två ODE:erna
och behåller samtidigt alla fyra begynnelsekoordinater.

# Kopplingen i fasorform

För $x(t)=\operatorname{Re}(\widehat x e^{\mathrm i\omega t})$,
$\mathrm i^2=-1$ och $\omega>0$, sätt $D=\mathrm i\omega$:
\nopagebreak[4]
\begin{align}
Z_s&=\mathrm i\omega L_s+R_s+\frac1{\mathrm i\omega C_s},
&\widehat e_s&=Z_s\widehat i, \nonumber\\*
Y_p&=\mathrm i\omega C_p+\frac1{R_p}+\frac1{\mathrm i\omega L_p},
&\widehat i&=Y_p\widehat e_p.
\label{eq:local-phasors}
\end{align}
Här omvandlar $Z_s$ ström till spänning och $Y_p$ spänning till ström.
Seriekopplingens villkor är fortfarande
\begin{equation}
\widehat e=Z_s\widehat i+\widehat e_p,\qquad
\widehat i=Y_p\widehat e_p.
\label{eq:phasor-connection}
\end{equation}
Sätt $\Delta=1+Z_sY_p$. Då fås
\begin{equation}
\boxed{\widehat e_p=\frac{\widehat e}{\Delta},\qquad
\widehat i=\frac{Y_p\widehat e}{\Delta},}
\qquad \Delta\ne0.
\label{eq:phasor-solution}
\end{equation}
Återfå $\widehat q=\widehat i/(\mathrm i\omega)$ och
$\widehat\lambda=\widehat e_p/(\mathrm i\omega)$.
Parallellgrenarnas strömmar är
\begin{equation}
\widehat i_C=\mathrm i\omega C_p\widehat e_p,\qquad
\widehat i_R=\frac{\widehat e_p}{R_p},\qquad
\widehat i_L=\frac{\widehat e_p}{\mathrm i\omega L_p},\qquad
\widehat i_C+\widehat i_R+\widehat i_L=\widehat i.
\label{eq:branch-phasors}
\end{equation}
Detta är harmoniska komponenter. Den fullständiga lösningen kräver
fortfarande begynnelsetillståndet i \eqref{eq:initial-state}.

## Fler block

Seriekopplingens spänningar ger $Z_{\mathrm{eq}}=\sum_jZ_j$;
parallellkopplingens strömmar ger $Y_{\mathrm{eq}}=\sum_jY_j$.
Alltså
\begin{equation}
\widehat e_j=\frac{Z_j}{\sum_\ell Z_\ell}\widehat e
\quad\text{(serie)},\qquad
\widehat i_j=\frac{Y_j}{\sum_\ell Y_\ell}\widehat i
\quad\text{(parallell)}.
\label{eq:division}
\end{equation}
Använd dessa kvoter endast när nämnarna är skilda från noll.
När storheterna är ändliga och skilda från noll gör $Y=1/Z$ det möjligt
att sammanföra en nästlad serie- och parallellkoppling från de innersta
grenarna och utåt. Summera komplexa fasorer innan beloppen tas;
vid en nämnare som är noll kontrolleras förenligheten i de ursprungliga
linjära ekvationerna.

# Elimination med bevarade begynnelsedata

Anta att $e(t)$ är två gånger kontinuerligt deriverbar och definiera
\begin{equation}
A(s)=L_ss^2+R_ss+\frac1{C_s},\qquad
B(s)=C_ps^2+\frac s{R_p}+\frac1{L_p}.
\label{eq:local-polynomials}
\end{equation}
De kopplade ekvationerna är $A(D)q+D\lambda=e$ och $B(D)\lambda=Dq$.
Applicera $B(D)$ på den första och använd de konstanta koefficienterna
för att låta operatorn kommutera med $D$:
\begin{equation}
\boxed{K(D)q=B(D)e,\qquad K(s)=A(s)B(s)+s^2.}
\label{eq:scalar}
\end{equation}
Denna ekvation av fjärde ordningen innehåller båda lokala polynomen
och termen $s^2$ från kopplingen mellan deras terminalderivator.

Rekonstruera de eliminerade variablerna genom
\begin{equation}
i=Dq,\qquad e_p=e-A(D)q,\qquad
\lambda=L_p\left(i-C_pD e_p-\frac{e_p}{R_p}\right).
\label{eq:reconstruction}
\end{equation}
Den skalära ekvationen medför $B(D)e_p=D^2q$, så derivering av den
sista formeln ger $D\lambda=e_p$. Alla ursprungliga ekvationer återfås.

För att återfå det ursprungliga begynnelsetillståndet, sätt
$q(t_0)=q_0$, $(Dq)(t_0)=i_0$ och
\nopagebreak[4]
\begin{align}
(D^2q)(t_0)&=\frac{e(t_0)-R_si_0-q_0/C_s-e_{p,0}}{L_s}, \nonumber\\*
(D^3q)(t_0)&=\frac{(De)(t_0)-R_s(D^2q)(t_0)-i_0/C_s-(D e_p)(t_0)}{L_s},
\label{eq:initial-derivatives}
\end{align}
där $(D e_p)(t_0)=(i_0-e_{p,0}/R_p-\lambda_0/L_p)/C_p$.
De fyra skalära begynnelsevärdena kodar samma fyra interna koordinater.

Eftersom $Z_s=A(\mathrm i\omega)/(\mathrm i\omega)$ och
$Y_p=B(\mathrm i\omega)/(\mathrm i\omega)$ gäller
\begin{equation}
K(\mathrm i\omega)=(\mathrm i\omega)^2\Delta.
\label{eq:phasor-agreement}
\end{equation}
Därmed ger $\widehat q=B(\mathrm i\omega)\widehat e/K(\mathrm i\omega)$
och rekonstruktionen \eqref{eq:phasor-solution} överallt där nämnaren
är skild från noll.

För att utvidga en lämplig lokal ekvation, välj koefficienter av högre
ordning ur [*ODE Coefficient Synthesis*][synthesis], avsnitt 1--4,
och återanvänd terminalvillkoren. När de lokala ekvationerna är kända
kan systemet på så sätt byggas upp utan att maskanalysen upprepas
för hela nätverket. Fasorer använder fortfarande $D=\mathrm i\omega$;
tillkommande derivataordningar kräver motsvarande begynnelsedata
som är förenliga med kopplingen.

# Referenser {-}

1. H. Nilre och B. C. Herlin (2026). [The ODE Template and Its Domain Equivalents][template].
2. H. Nilre och B. C. Herlin (2026). [ODE Coefficient Synthesis][synthesis].
3. H. Nilre och B. C. Herlin (2026). [Energy Ledgers for Forced Harmonic ODEs][energy].

[template]: https://github.com/hobnilre/physics-ode-template
[synthesis]: https://github.com/hobnilre/physics-ode-coefficient-synthesis
[energy]: https://github.com/hobnilre/physics-ode-energy
