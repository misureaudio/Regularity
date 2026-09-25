# Regularity: Where Measure Theory, Geometric Measure Theory, and Partial Differential Equations Meet

*An essay for readers in mathematical physics, functional analysis, and numerical analysis.*

---

## 1. Three faces of a single word

The word *regularity* does three different jobs in analysis, and the purpose of this essay is to show that they are not parallel subjects but one subject viewed from three sides.

The first face is **regularity of functions and solutions**: a weak solution of an elliptic or parabolic equation is, in fact, Hölder continuous, smooth, even analytic, under mild hypotheses on the coefficients and the domain. This is the home of Schauder theory, the $L^p$ theory of Agmon–Douglis–Nirenberg [6], the De Giorgi–Nash–Moser program [7,8,9], and the semigroup theory of parabolic problems.

The second face is **regularity of sets and measures**: a set whose boundary is only assumed to be rectifiable, or a function whose gradient is a measure, carries hidden geometric structure. The structure theorem for functions of bounded variation, the theory of sets of finite perimeter, and the rectifiability theorems of De Giorgi [1,2] and Federer [4] belong here.

The third face is **regularity of the singular set itself**: once one has proved that an object is smooth *outside a set*, the natural next question is *how small, and how structured, is the exceptional set?* For area-minimizing hypersurfaces the answer is a Hausdorff-dimension bound (at most $m-7$ for an $m$-dimensional hypersurface in codimension one [5]); for suitable weak solutions of the Navier–Stokes equations it is a parabolic-Hausdorff-dimension bound (at most $1$ [10]); for free boundaries it is a stratification together with, in the best cases, a sharp generic dimension bound.

The unifying observation is this. In all three faces the same *machine* is at work:

> **A variational or differential principle, combined with a measure-theoretic compactness (blow-up) argument and a scale-invariant quantity, upgrades a weak object to a smooth one outside a singular set of controlled Hausdorff dimension.**

Measure theory supplies the *language and the weak objects* (the perimeter as a measure, Hausdorff measure, rectifiability). Geometric measure theory (GMT) supplies the *framework for surfaces* and the *dimension-reduction machinery* that turns "smooth outside a small set" into a dimension-sharp statement. The PDE supplies the *engine*: the elliptic and parabolic regularity theorems, the monotonicity formulas, and the maximal-regularity results that actually force the upgrade.

A useful dictionary (here $m$ denotes the dimension of the hypersurface/current; the ambient dimension is $m+1$):

| Question | Measure-theoretic answer | GMT answer | PDE answer |
|---|---|---|---|
| How smooth is the *object*? | rectifiable, countably rectifiable | $C^{1,\beta}$-embedded outside $\operatorname{Sing}$ | $C^{k,\alpha}$, $C^\infty$, analytic |
| How large is the *exceptional set*? | $\mathcal H^{m}$-measurable, $\sigma$-finite | $\dim_{\mathcal H}\operatorname{Sing}\le m-7$ (codim. 1) | free boundary: stratified, generically $\le n-4$ [29]; Navier–Stokes: $\dim_{\mathcal H^{\mathrm{par}}}\operatorname{Sing}\le 1$ [10] |
| What *tool* gives the bound? | differentiation of measures, density theorem | $\varepsilon$-regularity + dimension reduction (Federer/Almgren) | monotonicity formula, Caccioppoli inequality, maximal regularity |

The rest of the essay walks the three faces in order and then, in §5, shows the concrete place where they all meet: the singular-perturbation / $\Gamma$-convergence bridge between a sharp interface and its diffuse (phase-field) approximation, where the regularity of the limit is exactly what controls the accuracy of a numerical method.

---

## 2. Measure-theoretic regularity: BV, sets of finite perimeter, rectifiability

### 2.1 The structure theorem for BV

Let $\Omega\subset\mathbb R^n$ be open. A function $u\in L^1_{\mathrm{loc}}(\Omega)$ is of *bounded variation* if its distributional gradient $Du$ is an $\mathbb R^n$-valued Radon measure of finite total variation on compact subsets. The structure theorem (see [3,11]) decomposes

$$
Du \;=\; \nabla u\,dx \;+\; D^c u \;+\; (u^+ - u^-)\,\nu_u\,\mathcal H^{n-1}\!\!\lfloor_{S_u} ,
$$

into an *absolutely continuous* part $\nabla u\,dx$, a *Cantor* part $D^c u$ (singular with respect to Lebesgue measure and mutually singular with the jump part), and a *jump* part $D^s u$ supported on the *jump set* $S_u$, on which $u$ has two one-sided traces $u^\pm$. The key measure-theoretic regularity fact is that

$$
S_u \text{ is countably } \mathcal H^{n-1}\text{-rectifiable},
$$

i.e. up to an $\mathcal H^{n-1}$-negligible set it is covered by the images of countably many $C^1$ Lipschitz maps from open subsets of $\mathbb R^{n-1}$. So a function whose derivative is merely a *measure* already has a *geometric* boundary of codimension one. This is regularity in the measure-theoretic sense: no differentiability of $u$ is assumed, yet the singular set is rectifiable.

### 2.2 Sets of finite perimeter

A Borel set $E$ has *finite perimeter* in $U$ if $\chi_E\in BV(U)$; the *perimeter* is

$$
P(E,U) \;=\; |D\chi_E|(U).
$$

The Gauss–Green formula takes the form

$$
\int_E \operatorname{div}\varphi\,dx \;=\; \int \varphi\cdot\nu_E\,d|D\chi_E|, \qquad \varphi\in C^1_c(U;\mathbb R^n),
$$

where $\nu_E$ is the measure-theoretic *outer* normal (with the inner normal the right-hand side carries a minus sign). The point is that the perimeter is a *measure* — the total variation of the distributional derivative — and the "boundary" of $E$ is the support of this measure.

### 2.3 De Giorgi's program: the perimeter measure and the reduced boundary

De Giorgi [1,2] (building on Caccioppoli's integration of differential forms and on the Hausdorff measure of Carathéodory) introduced the *reduced boundary* $\partial^* E$: a point $x\in\partial^* E$ is one at which the normalized rescaled measures converge,

$$
\lim_{r\downarrow 0}\frac{1}{|D\chi_E|(B_r(x))}\int_{B_r(x)} \frac{y-x}{|y-x|}\,dD\chi_E(y) \;=\; \nu_E(x), \qquad |\nu_E(x)|=1 .
$$

Two facts, now classical, follow from a *blow-up* argument (rescale $E$ about $x$, pass to the limit, and identify the limit as a half-space):

1. **Concentration.** The perimeter measure is carried by the reduced boundary: $D\chi_E = -\nu_E\,\mathcal H^{n-1}\!\lfloor_{\partial^* E}$ when $\nu_E$ is the *outer* normal (equivalently $D\chi_E = \nu_E\,\mathcal H^{n-1}\!\lfloor_{\partial^* E}$ with the inner normal). In particular $|D\chi_E| = \mathcal H^{n-1}\!\lfloor_{\partial^* E}$.

2. **Rectifiability (De Giorgi, 1958).** $\partial^* E$ is countably $\mathcal H^{n-1}$-rectifiable.

The proof is the prototype for everything that follows. At $\mathcal H^{n-1}$-almost every point of $\partial^* E$, a monotonicity formula for the *density*

$$
r^{1-n}\,|D\chi_E|(B_r(x))
$$

(which is non-decreasing in $r$) forces the blow-up to be a half-space; the Preiss–Mattila / density criterion then promotes "flat tangent measure a.e." to *countable rectifiability*. No PDE is invoked — this is pure measure theory (the differentiation of measures, the Lebesgue density theorem, blow-up limits) producing a *geometric* conclusion. This is the foundation on which GMT and PDE regularity are built: it tells us that the *a priori* regularity of a perimeter-minimizing object is already rectifiability, and it gives the *method* (blow-up + monotonicity) that the PDE will later sharpen to smoothness.

The *coarea formula* and the *area formula* (see [3]) are the measure-theoretic backbone that makes this program work for *functions* as well as for sets: for $u\in W^{1,1}$,

$$
\int_{\mathbb R} \mathcal H^{n-1}\big(\{u=t\}\big)\,dt \;=\; \int_\Omega |\nabla u|\,dx,
$$

so the "size" of the level sets of $u$ is controlled by the $L^1$ norm of $\nabla u$. This is what allows one to talk about the perimeter of a level set $\{u>0\}$ of a merely $W^{1,1}$ function — and hence what makes *free-boundary problems* measurable at all.

**Takeaway.** Measure theory gives the *weak objects* (BV functions, perimeter measures) and the *a priori regularity* (rectifiability), and it does so by measure-theoretic means (differentiation, density, blow-up). It also gives the *method* — the monotonicity/blow-up argument — that the PDE will inherit and sharpen.

---

## 3. Geometric measure theory: surfaces, varifolds, $\varepsilon$-regularity, and dimension reduction

### 3.1 From sets to currents and varifolds

Federer and Fleming [12] replaced a set $E$ by the *integer multiplicity rectifiable current* $T=\partial[\mathbf E]$ it bounds, with mass $\mathbf M(T)=|D\chi_E|$. Almgren's *varifolds* (Radon measures on the Grassmann bundle of tangent planes) are a weaker, more flexible object: a $k$-dimensional varifold $V$ records, at each point and each tangent $k$-plane, how much mass is present. The *mass* $|V|$ is the push-forward of $V$ to the ambient manifold. Classical smooth submanifolds embed as *integral rectifiable varifolds*, and compactness (sequential compactness under varifold convergence with bounded mass) holds.

### 3.2 The first variation and weak mean curvature

Allard [13] defined the *first variation* of a varifold. For a test vector field $g$,

$$
\delta V(g) \;=\; -\int \operatorname{div}_{T} g\,dV ,
$$

where $\operatorname{div}_T$ is the tangential divergence (the divergence of $g$ projected onto the tangent plane, averaged over the Grassmann fiber). When $\delta V$ is representable by integration against a vector field $H$ with respect to the mass,

$$
\delta V(g) \;=\; -\int H\cdot g\,d|V| ,
$$

the field $H$ is the (weak) *mean curvature vector*. The hierarchy is

$$
\text{area-minimizing} \;\Longrightarrow\; \text{stationary }(\delta V=0) \;\Longrightarrow\; \text{finite first variation}.
$$

A stationary varifold is the weak notion of a *minimal surface*: it satisfies the minimal-surface equation in the sense of distributions, with the second fundamental form integrable. This is precisely the GMT analog of "a weak solution of an elliptic PDE."

### 3.3 The $\varepsilon$-regularity theorem

The central regularity statement (Allard, De Giorgi, Federer — see [4,13]) is an $\varepsilon$-regularity theorem:

> **$\varepsilon$-regularity.** There exist $\varepsilon_0>0$, $\beta_0\in(0,1)$, $C>0$ such that if a stationary integral $k$-varifold $V$ in $B_1$ satisfies $|V|(B_1)\le C$ and the concentration
> $$\int_{B_1} |\mathbf A|^2\,d|V| \;\le\; \varepsilon_0$$
> (equivalently, the first variation $\delta V$ is small in $L^1$), then $V\lfloor_{B_{1/2}}$ is the varifold of a single $C^{1,\beta_0}$ embedded submanifold (a graph over a $k$-plane).

Here $|\mathbf A|$ is the norm of the second fundamental form. The statement is the GMT counterpart of elliptic $\varepsilon$-regularity: *smallness of a scale-invariant curvature quantity in a ball implies smoothness in a smaller ball.* It is the single most important regularity principle in GMT, and it is what makes the dimension-reduction below possible.

### 3.4 Dimension reduction and the sharp singular-set bound

$\varepsilon$-regularity gives *partial* regularity: the regular set $\operatorname{Reg}(V)$ is open, and the singular set $\operatorname{Sing}(V)=\operatorname{spt}V\setminus\operatorname{Reg}(V)$ is closed. To bound its *size*, Federer's *dimension-reduction principle* (and Almgren's *generalized stratification*) iterate the argument at the *tangent cones*:

- The tangent cone of a stationary varifold is again stationary, and the $\varepsilon$-regularity theorem applies to it.
- If the singular set had Hausdorff dimension $>m-d$ for some $d$, one could find a point whose tangent cone is singular in a $d$-dimensional family of directions, contradicting the (inductively known) regularity of cones of dimension $<m$.
- Induction on dimension yields $\dim_{\mathcal H}\operatorname{Sing}(V)\le m-d$.

In codimension one the sharp result is due to Federer [5]:

> **Theorem (Federer).** If $T$ is an area-minimizing $m$-dimensional integral current in a Riemannian $(m+1)$-manifold, then $\operatorname{Sing}(T)$ has $\mathcal H^{m-7+\alpha}$-measure zero for every $\alpha>0$; in particular $\dim_{\mathcal H}\operatorname{Sing}(T)\le m-7$.

The *threshold* $m-7$ is where the PDE enters decisively. The dimension-reduction reduces the question to: *does there exist a non-flat stable (or minimizing) cone with an isolated singularity?* The answer is:

- $m\le 6$: **no** — Simons [14] proved that every stable minimal cone in $\mathbb R^{m+1}$ for $m\le 6$ is a plane (his argument builds on De Giorgi and Fleming, and on Almgren's earlier extension of Bernstein's theorem [42], which settles the $m=4$ case). Hence $\operatorname{Sing}=\varnothing$ for $m\le 6$.
- $m=7$: **yes** — Simons [14] constructed the cone over $S^3\times S^3\subset\mathbb R^8$,
  $$\mathcal S=\{x\in\mathbb R^8: x_1^2+x_2^2+x_3^2+x_4^2=x_5^2+x_6^2+x_7^2+x_8^2\},$$
  a $7$-dimensional minimal hypersurface with an isolated singularity at the origin; Bombieri–De Giorgi–Giusti [15] proved it is in fact **area-minimizing**, giving the first non-planar area-minimizing hypersurface with a singularity. This shows the $m-7$ threshold is **sharp**: for $m=7$ the bound $m-7=0$ (isolated singular points) is attained, and no regularity theorem for stable minimal hypersurfaces can improve on $m-7$.
- $m\ge 8$: products $\mathcal S\times\mathbb R^{m-7}$ give area-minimizing hypersurfaces with $\mathcal H^{m-7}(\operatorname{Sing})>0$.

For *stable* (not necessarily minimizing) hypersurfaces the same $m-7$ bound holds (Schoen–Simon [16]), and the singular set is *countably $(m-7)$-rectifiable with locally finite $(m-7)$-measure* (Simon [18]; for stationary varifolds, Naber–Valtorta [17]). See also the survey of De Lellis [19].

**Takeaway.** GMT turns the qualitative "smooth outside a small set" into a *dimension-sharp* statement. The measure-theoretic object (current/varifold) is what provides compactness and makes the blow-up and dimension-reduction rigorous; the PDE (the minimal-surface equation, the second variation, the stability inequality) is what is actually used *at the tangent-cone level* to rule out (or allow) singular cones. The number $m-7$ is not geometric bookkeeping — it is the output of an elliptic-PDE computation (Simons' second-variation estimate on the second fundamental form).

---

## 4. PDEs as the regularity engine

### 4.1 Elliptic regularity of functions, and the De Giorgi–Nash–Moser paradigm

Classical elliptic regularity (Schauder estimates for $C^{k,\alpha}$ data; the $L^p$ estimates of Agmon–Douglis–Nirenberg [6]) says that if $u$ solves $Lu=f$ with $L$ uniformly elliptic and the data are smooth, then $u$ is as smooth as the data. The *paradigm* for the measure-theoretic flavor of PDE regularity is the **De Giorgi–Nash–Moser** program [7,8,9]:

- *De Giorgi (1957)* [7] proved Hölder continuity of weak solutions of divergence-form elliptic equations $-\operatorname{div}(A\nabla u)=0$ with merely *bounded measurable* $A$, using a *level-set / capacity argument*: the Caccioppoli inequality controls the measure of the super-level sets, and a measure-theoretic *iteration* (a "contraction" of the oscillation) yields $u\in C^{0,\alpha}$.
- *Nash (1958)* [8] extended the argument to parabolic equations via an $L^2$ energy plus an $L^\infty$ bound.
- *Moser (1960)* [9] gave the clean iteration proof and the Harnack inequality.

This is the direct ancestor of every modern "measure-theoretic PDE regularity" result: the *Caccioppoli (energy) inequality* is a *measure-theoretic* estimate on the solution, and the *iteration* is a *measure-theoretic* bootstrap. The same template — a scale-invariant quantity small in an $L^p$ norm or as a measure implies regularity — underlies the $\varepsilon$-regularity criteria for the Navier–Stokes equations and for drift-diffusion equations (Caffarelli–Vasseur), where the singular set of a suitable weak solution is controlled by a dimension-reduction argument exactly as in GMT.

### 4.2 Free boundaries: the interface is the unknown

A *free-boundary problem* asks for a function $u$ that solves an elliptic PDE in two regions $\Omega^+=\{u>0\}$ and $\Omega^-=\{u\le 0\}$, together with an *overdetermined* condition on the interface $F(u)=\partial\Omega^+\cap\Omega$. The interface is the *unknown*; its regularity is the central question. Two model problems:

**One-phase (obstacle problem).** Find $u$ minimizing $\tfrac12\int|\nabla v|^2$ among $v\ge\varphi$; equivalently,
$$
\Delta u\le 0\text{ in }\Omega,\quad u\ge\varphi,\quad (\Delta u)(u-\varphi)=0.
$$
$u$ is harmonic in the free region $\{u>\varphi\}$ and *quadratic* (to leading order) in the contact set. Kinderlehrer–Nirenberg [21] and Kinderlehrer–Nirenberg–Spruck [22,23] proved that, under thickness/non-degeneracy conditions, the free boundary is real-analytic.

**Two-phase (Bernoulli / Alt–Caffarelli–Friedman).** Minimize
$$
J(u)=\int_\Omega |\nabla u|^2 + q^2(x)\,\lambda^2(u)\,dx,
$$
so that $u$ is harmonic in $\Omega^+\cup\Omega^-$ and satisfies a *jump condition* on $F(u)$,
$$
|\nabla u^+|^2-|\nabla u^-|^2 = c \quad\text{on }F(u).
$$
Alt–Caffarelli–Friedman [24] introduced the *monotonicity formula*
$$
\Phi(r)=r^{-4}\left(\int_{B_r}\frac{|\nabla u^+|^2}{|x|^{n-2}}\,dx\right)\left(\int_{B_r}\frac{|\nabla u^-|^2}{|x|^{n-2}}\,dx\right)
$$
(the *product* of the two weighted Dirichlet energies, one per phase), which is non-decreasing in $r$ and forces *uniqueness of the blow-up* at a free-boundary point.

**Caffarelli's program** [20,25,26] is the PDE counterpart of De Giorgi's GMT regularity:

1. *Blow-up.* Rescale about a free-boundary point; the monotonicity formula (Alt–Caffarelli–Friedman [24]; Weiss [27]) gives uniqueness of the blow-up, which is classified (half-plane, two-plane, or a degenerate quadratic).
2. *Flatness $\Rightarrow$ Lipschitz $\Rightarrow C^{1,\alpha}\Rightarrow$ analytic.* A compactness/linearization argument (Caffarelli [25,26]) upgrades flatness to full $C^{1,\alpha}$ regularity of the interface, and then to analyticity (Kinderlehrer–Nirenberg [21]).
3. *Singular set.* At points where the blow-up is a *degenerate* quadratic (the kernel of the Hessian has positive dimension), the interface may be singular. The regular part is $C^{1,\alpha}$ (indeed analytic). The singular part is *stratified*: Caffarelli [28] showed the $m$-th stratum (points where the blow-up quadratic has an $m$-dimensional kernel) is locally contained in a $C^1$ $m$-dimensional manifold. Crucially, the top stratum can in general be $(n-1)$-dimensional — as large as the regular part — so the singular set need not be small in dimension. The deep recent result of Figalli–Ros-Oton–Serra [29] shows that, *generically* (in a parameter-dependent family of solutions), the singular set has Hausdorff dimension at most $n-4$ — i.e. codimension at least $3$ inside the free boundary — which proves Schaeffer's 1974 conjecture in dimensions $n\le 4$.

The deep point for our audience is that the free boundary $F(u)$ is, *a priori*, only a set of *finite perimeter* (hence $\mathcal H^{n-1}$-rectifiable, by §2) — a *measure-theoretic* object — and its *smoothness* is a *PDE* conclusion obtained by the GMT-style monotonicity/blow-up method. This is the precise sense in which PDE and GMT are the same subject: the PDE in each phase plus the boundary condition on the interface, combined with a scale-invariant monotonicity formula, is the "engine" that upgrades a rectifiable interface to a smooth one outside a small singular set.

### 4.3 Maximal regularity for parabolic problems (the functional-analytic thread)

This is where the *functional-analysis* audience connects most directly. Consider the abstract Cauchy problem

$$
u' + A u = f \text{ in } X,\qquad u(0)=u_0,
$$

where $A$ is the generator of an analytic $C_0$-semigroup on a Banach space $X$ (e.g. $A=-\Delta$ with Dirichlet/Neumann/Robin conditions on $L^p$). The **maximal $L^p$-regularity** property says:

> **Maximal regularity.** For $f\in L^p(0,T;X)$ and $u_0$ in the real interpolation space $(X,D(A))_{1-1/p,p}$, there is a unique solution
> $$u\in W^{1,p}(0,T;X)\cap L^p(0,T;D(A))$$
> satisfying
> $$\|u'\|_{L^p} + \|Au\|_{L^p} \;\le\; C\big(\|f\|_{L^p} + \|u_0\|_{(X,D(A))_{1-1/p,p}}\big).$$

The word *maximal* is literal: the solution has the *maximal* regularity compatible with the data — the time-derivative $u'$ and the operator-applied quantity $Au$ lie in the *same* space $L^p$, and the compatibility condition on $u_0$ is *necessary and sufficient*. This is a *functional-analytic* regularity statement, stated in the interpolation / Bessel-potential / Triebel–Lizorkin spaces that are the same spaces appearing in the *fine properties of functions* (the measure-theoretic theory of Evans–Gariepy [3]).

The history is a long one:

- *Lions [30]* and *Lions–Magenes [31]* established the $L^2$ theory.
- The general $L^p$ result for the Laplacian on smooth domains was a long-standing open problem; the full *$L^p$ maximal regularity problem* (for arbitrary sectorial operators / Banach spaces) was settled by *Weis [32]*, who showed that the *$H^\infty$-functional calculus* (equivalently, $R$-boundedness of the associated resolvent family) is the right condition: it is sufficient for maximal regularity, and Kalton–Lancien showed it is essentially necessary (a counterexample on general Banach spaces).
- *Denk–Hieber–Prüss [33]* extended the theory to *operator-valued* coefficients via vector-valued Fourier multipliers.
- *Prüss [34]* gave the classical parabolic results; Amann's monograph [35] develops the anisotropic / nonlinear theory.

Why this matters to the other two faces: (i) maximal regularity is the *time-regularity* statement that convergence proofs for time-discretization (backward Euler, Crank–Nicolson) need — the bound $\|u'\|_{L^p}$ is what controls the temporal error; (ii) the sharp *compatibility conditions* on $u_0$ are the functional-analytic home of the *trace theorems* that connect boundary data to the interior; and (iii) the interpolation spaces in the estimate are precisely the spaces whose *fine properties* (quasicontinuity, absolute continuity on lines, traces on sets of finite measure) are the subject of measure theory. Maximal regularity is thus "regularity" in the functional-analytic sense, and it is the backbone of parabolic well-posedness and of the convergence theory of numerical schemes.

---

## 5. The $\Gamma$-convergence / singular-perturbation bridge: where all three meet

This is the concrete, quantitative place where measure theory, GMT, and PDE interact, and where the regularity of the limit determines the accuracy of a numerical method. It is the natural home of the mathematical-physics and numerical-analysis reader.

### 5.1 Sharp versus diffuse interfaces

A *sharp interface* is a geometric object — a hypersurface (possibly singular) separating two phases, evolving by *mean curvature flow*. A *diffuse interface* replaces the sharp hypersurface by an *order parameter* $\varphi$ that transitions smoothly between two wells (say $\pm1$) over a layer of thickness $O(\varepsilon)$. The diffuse description is governed by a PDE (Allen–Cahn / Ginzburg–Landau), and it is the object one actually *numerically approximates*.

The relevant energy is the **Modica–Mortola** functional [36,37]:

$$
E_\varepsilon(u) \;=\; \int_\Omega \Big(\tfrac{\varepsilon}{2}|\nabla u|^2 + \tfrac{1}{\varepsilon}W(u)\Big)\,dx,
$$

where $W$ is a double-well potential with minima at $\pm1$. As $\varepsilon\downarrow0$, the two competing terms — the gradient (which wants $u$ constant) and the potential (which wants $u=\pm1$) — produce a transition layer of thickness $O(\varepsilon)$ in which the *interface energy* is concentrated.

### 5.2 The $\Gamma$-limit: the diffuse energy converges to the perimeter

The **Modica–Mortola theorem** [37] (and the minimal-interface criterion of Modica [36]) is a $\Gamma$-convergence result:

> As $\varepsilon\downarrow0$, $E_\varepsilon$ $\Gamma$-converges (in $L^1$) to
> $$E_0(u) \;=\; \begin{cases} c_W\,\mathcal H^{n-1}\big(\partial^* E\big) & \text{if }u=\chi_E-\chi_{\Omega\setminus E}\text{ a.e. for some set }E,\\ +\infty & \text{otherwise,}\end{cases}$$
> where $c_W>0$ depends only on $W$ (the *interface energy* $c_W=\int_{-1}^{1}\sqrt{2W(s)}\,ds$).

This is a statement about the *convergence of minimizers and of energies*: the smooth, PDE-governed diffuse energy converges to the *sharp, measure-theoretic perimeter* (the object of §2). The $\Gamma$-limit $E_0$ is *not* a function of $u$ in any classical sense — it is an *integral-geometric* functional of the jump set of $u$. The "regularity" here is the regularity of the *limit*: the limit of smooth minimizers is a set of finite perimeter, and (if one minimizes in a fixed class) a perimeter-minimizer, whose reduced boundary is rectifiable (§2) and, for minimizers, smooth outside a singular set of dimension $\le m-7$ (§3).

### 5.3 The dynamics: Allen–Cahn approximates mean curvature flow

The $L^2$-gradient flow of $E_\varepsilon$ (the *Allen–Cahn equation*; the precise constant in front of $\Delta$ is conventional) is

$$
\partial_t u \;=\; \varepsilon\,\Delta u - \tfrac{1}{\varepsilon}W'(u).
$$

The sharp-interface limit of this PDE is *motion by mean curvature* (the $L^2$-gradient flow of the perimeter). The rigorous convergence was proved by *Evans–Soner–Souganidis [38]* and *Barles–Soner–Souganidis [39]*: the zero level set $\{u_\varepsilon=0\}$ converges (in the sense of the associated *generalized* motion) to the generalized motion by mean curvature. The method is a *comparison principle* for the limiting *Hamilton–Jacobi* equation for the distance function — a PDE for the interface — combined with the *viscosity-solution* theory. The convergence holds *beyond the onset of singularities*, provided one uses the *generalized* (level-set) motion.

### 5.4 The quantitative side: error estimates, and why regularity of the limit controls accuracy

The convergence above is *qualitative* (topological / in the level-set sense). The *quantitative* question — *how far is the diffuse interface from the sharp one?* — is a numerical-analysis question, and its answer is governed by the *regularity of the limit interface*:

- *Chen [40]* obtained **first-order** $O(\varepsilon)$ estimates for the Hausdorff distance between the diffuse and sharp interfaces, via *comparison* (sub/supersolutions), valid *before the onset of singularities*.
- *Nochetto–Paolini–Verdi [41]* obtained **optimal second-order** $O(\varepsilon^2)$ estimates for a *thin / double-obstacle* formulation, by constructing explicit sub/supersolutions from the *asymptotic expansion* of $u_\varepsilon$.

The mechanism is exactly the interplay of the three faces. The sub/supersolutions are built from an *asymptotic expansion*
$$
u_\varepsilon(x,t) \;=\; \tanh\!\Big(\frac{d(x,t)}{\sqrt{2}\,\varepsilon}\Big) + \varepsilon\,u_1(x,t)+O(\varepsilon^2),
$$
where $d(x,t)$ is the signed distance to the *sharp* interface. (The leading profile is the one-dimensional Modica–Mortola minimizer $u_0(z)=\tanh(z/\sqrt2)$ for the standard well $W(s)=\tfrac14(1-s^2)^2$; it satisfies $u_0''=W'(u_0)$, i.e. the steady Allen–Cahn profile equation.) This expansion *requires the limit interface to be smooth* (the distance function $d$ must be differentiable, the curvature must be bounded). Where the limit develops a *singularity* (a corner, a cusp, a multiplicity point — the singular set of §3/§4), the expansion breaks down, the sub/supersolutions cease to exist, and the $O(\varepsilon^2)$ estimate fails. The *regular part* of the limit (the $C^{1,\alpha}$ / analytic free boundary of §4.2, the smooth part of the minimizing hypersurface of §3) is precisely where the numerical method is accurate; the *singular set* is precisely where it is not.

This is the cleanest statement of the thesis: **the regularity of the limit (a GMT/PDE question) is exactly what determines the accuracy of the numerical approximation (a numerical-analysis question), and the bridge between them is a $\Gamma$-convergence / singular-perturbation argument (a measure-theoretic question).**

---

## 6. Synthesis and open problems

### 6.1 The "regularity trinity"

The three disciplines are interlocking, not parallel:

- **Measure theory** provides the *language and the weak objects*: the perimeter as a measure, Hausdorff measure, rectifiability, the BV structure theorem. It gives the *a priori* regularity (rectifiability) and the *method* (blow-up + monotonicity of the density).
- **Geometric measure theory** provides the *framework for surfaces* (currents, varifolds) and the *dimension-reduction / stratification machinery* that turns "smooth outside a small set" into a dimension-sharp bound. The measure-theoretic object is what makes compactness and the induction rigorous.
- **PDEs** provide the *engine*: elliptic/parabolic regularity (De Giorgi–Nash–Moser, Schauder, $L^p$), the *monotonicity formulas* that force uniqueness of blow-ups, the *second variation* that rules out singular cones, and *maximal regularity* that gives the sharp time-regularity of parabolic solutions.

The common method, in every case, is:

> **a scale-invariant quantity (energy, density, frequency/monotonicity function) + compactness (blow-up) + a PDE at the tangent level $\;\Longrightarrow\;$ regularity outside a singular set of controlled Hausdorff dimension.**

### 6.2 Open problems

- **The optimal dimension of the singular set of free boundaries.** For the obstacle problem the singular set is stratified [28] and can in general be $(n-1)$-dimensional; the generic result of Figalli–Ros-Oton–Serra [29] gives codimension at least $3$ ($\dim\le n-4$) for $n\le 4$, proving Schaeffer's conjecture. The precise structure at branch points and the optimal bound in higher dimensions remain open. The two-phase Bernoulli problem has analogous open questions at *branch points*.
- **The regularity of stationary varifolds.** Allard's theorem gives regularity up to a *meager closed* set; it is *not* known that the singular set of a stationary (not minimizing, not stable) integral varifold is $\mathcal H^m$-negligible — not even for stationary $2$-varifolds in $3$ dimensions. This is one of the deepest open problems in GMT.
- **The $L^p$ maximal regularity problem in full generality.** Weis [32] settled the autonomous case; the *non-autonomous*, *operator-valued*, and *rough-coefficient* cases (e.g. parabolic problems with merely measurable time-dependent coefficients, or on domains with corners) remain active. The connection to the *fine properties* of the solution (quasicontinuity, traces on sets of finite measure) is still being worked out.
- **The Navier–Stokes singular set.** Caffarelli–Kohn–Nirenberg [10] proved the singular set of a *suitable* weak solution has *parabolic Hausdorff dimension at most $1$* (indeed $\mathcal H^1_{\mathrm{par}}(\operatorname{Sing})=0$). Whether the singular set is empty (full regularity) is the *Millennium problem*; the measure-theoretic $\varepsilon$-regularity criterion and the dimension-reduction argument are the current best tools, and any progress is expected to come from sharpening them.
- **Quantitative regularity of phase-field approximations past singularities.** The $O(\varepsilon^2)$ estimates of [41] are valid only *before* singularities. A quantitative theory that tracks the diffuse interface *through* a topological change or a singularity (where the generalized motion takes over) is open and is of direct interest to the numerical community.

### 6.3 A closing remark

Modern regularity theory is, at its core, *measure-theoretic*. The $\varepsilon$-regularity criteria — "smallness of a scale-invariant quantity, measured in an $L^p$ space or as a measure, implies smoothness" — are the common currency of elliptic PDE, GMT, and free-boundary theory, and the dimension-reduction / stratification argument is the common conclusion. The three faces of the word *regularity* — of functions, of sets and measures, and of the singular set — are not three subjects. They are one subject, in which measure theory speaks, GMT keeps the geometry, and the PDE does the work.

---

## References

1. E. De Giorgi, *Su una teoria generale della misura $(r-1)$-dimensionale in uno spazio ad $r$ dimensioni*, Ann. Mat. Pura Appl. (4) **36** (1954), 191–213.
2. E. De Giorgi, *Nuovi teoremi relativi alle misure $(r-1)$-dimensionali in uno spazio ad $r$ dimensioni*, Ricerche Mat. **4** (1955), 95–113.
3. L. C. Evans, R. F. Gariepy, *Measure Theory and Fine Properties of Functions*, 2nd ed., CRC Press, 2015.
4. H. Federer, *Geometric Measure Theory*, Grundlehren der mathematischen Wissenschaften **153**, Springer, 1969.
5. H. Federer, *The singular sets of area minimizing rectifiable currents with codimension one and of area minimizing flat chains modulo two with arbitrary codimension*, Bull. Amer. Math. Soc. **76** (1970), 767–771.
6. S. Agmon, A. Douglis, L. Nirenberg, *Estimates near the boundary for solutions of elliptic partial differential equations satisfying boundary conditions of zeroth and first order*, Comm. Pure Appl. Math. **12** (1959), 623–727.
7. E. De Giorgi, *Sulla differenziabilità e l'analiticità delle estremali degli integrali multipli regolari*, Mem. Accad. Sci. Torino Cl. Sci. Fis. Mat. Nat. (3) **3** (1957), 25–43.
8. J. Nash, *Continuity of solutions of parabolic and elliptic equations*, Amer. J. Math. **80** (1958), 931–954.
9. J. Moser, *A new proof of De Giorgi's theorem concerning the regularity problem for elliptic partial differential equations*, Comm. Pure Appl. Math. **13** (1960), 457–468.
10. L. Caffarelli, R. Kohn, L. Nirenberg, *Partial regularity of suitable weak solutions of the Navier–Stokes equations*, Comm. Pure Appl. Math. **35** (1982), 771–831.
11. L. Ambrosio, N. Fusco, D. Pallara, *Functions of Bounded Variation and Free Discontinuity Problems*, Oxford University Press, 2000.
12. H. Federer, W. H. Fleming, *Normal and integral currents*, Ann. of Math. (2) **72** (1960), 458–486.
13. W. K. Allard, *On the first variation of a varifold*, Ann. of Math. (2) **95** (1972), 417–491.
14. J. Simons, *Minimal varieties in Riemannian manifolds*, Ann. of Math. (2) **88** (1968), 62–105.
15. E. Bombieri, E. De Giorgi, E. Giusti, *Minimal cones and the Bernstein problem*, Invent. Math. **7** (1969), 243–268.
16. R. Schoen, L. Simon, *Regularity of stable minimal hypersurfaces*, Comm. Pure Appl. Math. **34** (1981), 741–797.
17. A. Naber, D. Valtorta, *The singular structure and regularity of stationary varifolds*, J. Eur. Math. Soc. **22** (2020), 3305–3382.
18. L. Simon, *Rectifiability of the singular sets of multiplicity one minimal surfaces and energy minimizing maps*, in *Surveys in Differential Geometry, Vol. II* (Cambridge, MA, 1993), 246–305, Int. Press, 1995.
19. C. De Lellis, *The size of the singular set of area-minimizing currents*, Surveys in Differential Geometry **21** (2016), 1–83.
20. L. A. Caffarelli, *The regularity of free boundaries in higher dimensions*, Acta Math. **139** (1977), 155–184.
21. D. Kinderlehrer, L. Nirenberg, *Regularity in free boundary problems*, Ann. Scuola Norm. Sup. Pisa Cl. Sci. (4) **4** (1977), 373–391.
22. D. Kinderlehrer, L. Nirenberg, J. Spruck, *Regularity in elliptic free boundary problems. I*, J. Analyse Math. **34** (1978), 86–119.
23. D. Kinderlehrer, L. Nirenberg, J. Spruck, *Regularity in elliptic free boundary problems. II. Equations of higher order*, Ann. Scuola Norm. Sup. Pisa Cl. Sci. (4) **6** (1979), 637–683.
24. H. W. Alt, L. A. Caffarelli, A. Friedman, *Variational problems with two phases and their free boundaries*, Trans. Amer. Math. Soc. **282** (1984), 431–461.
25. L. A. Caffarelli, *A Harnack inequality approach to the regularity of free boundaries. Part I: Lipschitz free boundaries are $C^{1,\alpha}$*, Rev. Mat. Iberoam. **3** (1987), 139–162.
26. L. A. Caffarelli, *A Harnack inequality approach to the regularity of free boundaries. Part II: Flat free boundaries are Lipschitz*, Comm. Pure Appl. Math. **42** (1989), 55–78.
27. G. S. Weiss, *A homogeneity improvement approach to the obstacle problem*, Invent. Math. **138** (1999), no. 1, 23–50.
28. L. A. Caffarelli, *The obstacle problem revisited*, J. Fourier Anal. Appl. **4** (1998), 383–402.
29. A. Figalli, X. Ros-Oton, J. Serra, *Generic regularity of free boundaries for the obstacle problem*, Publ. Math. IHÉS **132** (2020), 181–292.
30. J.-L. Lions, *Équations différentielles opérationnelles et problèmes aux limites*, Grundlehren der mathematischen Wissenschaften **111**, Springer, 1961.
31. J.-L. Lions, E. Magenes, *Problèmes aux limites non homogènes et applications*, 2 vols., Dunod, Paris, 1972.
32. L. Weis, *Operator-valued Fourier multiplier theorems and maximal $L^p$-regularity*, Math. Ann. **319** (2001), 735–758.
33. R. Denk, M. Hieber, J. Prüss, *$R$-boundedness, Fourier multipliers and problems of elliptic and parabolic type*, Mem. Amer. Math. Soc. **166** (2003), no. 788.
34. J. Prüss, *Maximal regularity for parabolic problems*, J. Math. Soc. Japan **39** (1987), 441–460.
35. H. Amann, *Linear and Quasilinear Parabolic Problems. Volume I: Abstract Linear Theory*, Monographs in Mathematics **89**, Birkhäuser, 1995.
36. L. Modica, *The gradient theory of phase transitions and the minimal interface criterion*, Arch. Ration. Mech. Anal. **98** (1987), 123–142.
37. L. Modica, S. Mortola, *Un esempio di $\Gamma$-convergenza*, Boll. Un. Mat. Ital. B (5) **14** (1977), 285–299.
38. L. C. Evans, H. M. Soner, P. E. Souganidis, *Phase transitions and generalized motion by mean curvature*, Comm. Pure Appl. Math. **45** (1992), 1097–1123.
39. G. Barles, H. M. Soner, P. E. Souganidis, *Front propagation and phase field theory*, SIAM J. Control Optim. **31** (1993), 439–469.
40. X. Chen, *Convergence of Ginzburg–Landau equations with applications to anisotropic interface motions in crystals*, Differential Integral Equations **6** (1993), 1653–1676.
41. R. H. Nochetto, M. Paolini, C. Verdi, *Optimal interface error estimates for the mean curvature flow*, Ann. Scuola Norm. Sup. Pisa Cl. Sci. (4) **21** (1994), 193–212.
42. F. J. Almgren Jr., *Some interior regularity theorems for minimal surfaces and an extension of Bernstein's theorem*, Ann. of Math. (2) **84** (1966), 277–292.
