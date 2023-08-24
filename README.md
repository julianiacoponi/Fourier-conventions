# FOURIER CONVENTIONS
This is all heavily based on the links given, but I've added some extra expressions + intuitions to help connect the ideas better!

---
## (1) https://mathworld.wolfram.com/FourierTransform.html

"_In general, the Fourier transform pair may be defined using two arbitrary constants_ $(a, b)$_:_

$$ \text{FT} \lbrace f(t) \rbrace = f(ω) = \sqrt{ \frac{|b|}{(2π)^{1 - a}} } \int_{-∞}^{∞} f(t) e^{i b ω t} dt $$

$$ \text{FT}^{-1} \lbrace f(ω) \rbrace = f(t) = \sqrt{ \frac{|b|}{(2π)^{1 + a}} } \int_{-∞}^{∞} f(ω) e^{-i b ω t} d ω $$

_The Fourier transform_ $f(ω)$ _of a function_ $f(t)$ _is implemented by the Wolfram Language as `FourierTransform[f, t, ω]`, and different choices of_ $a$ _and_ $b$ _can be used by passing the optional `FourierParameters → {a, b}` option._

_By default, the Wolfram Language takes `FourierParameters` as `{a, b} = {0,1}`*._"

*This convention is described later as 'modern physics'.


---
## (2) https://www.johndcook.com/blog/fourier-theorems/

This link shows a lot of handy theorems and how they convert between the different definitions!

"_There are several slightly different ways to define a Fourier transform. This means that when you look up a theorem about the Fourier transform you have to ask yourself which convention the source is using. All the common conventions can be summarized in the following definition:_"

$$ \text{FT} \lbrace f(t) \rbrace = f(ω) = \frac{1}{\sqrt{m}} \int_{-∞}^{∞} f(t) \exp(i σ q ω t) dt $$

Implying

$$ \text{FT}^{-1} \lbrace f(ω) \rbrace = f(t) = \frac{\sqrt{m} |σ q|}{2π} \int_{-∞}^{∞} f(ω) \exp(-i σ q ω t) dω $$

where
- _Sign convention_ $σ = +1$ or $-1$,
- _Frequency convention_ $q = 2π$ or $1$,
- _Scaling convention_ $m = 1$ or $2π$,

"_This means there are eight potential definitions, one for each choice of_ $σ$_,_ $q$_, and_ $m$_, though only six* of these are widely used._"

*As will become clear, there are in fact more than 6 commonly used definitions...


---
## (3) Understanding the parameters defining different conventions
An intuituion on the presence of these arbitrary parameters is that they represent two independent free choices to be made when defining the Fourier transform pair:


### Normalisation parameter, $a \in \mathbb{R}$
- Choosing parameter $a$ can be seen as an arbitrary choice of how to satisfy the only actual meaningful constraint:

$$ C_- \ C_+ = |b|/2π $$

defining $C_± = \sqrt{ |b| / (2π)^{1 ± a} }$ as the normalisation constants outside the forward ($C_-$) and inverse ($C_+$) transforms.


### Frequency/Rotation parameter, $b \in \ ?$*
- Choosing parameter $b$ can be seen as another arbitrary decision of how much one would like to define the transforms in:
    - angular frequency terms ($b = ±1$, with angles measured in radians), or
    - ordinary frequency terms ($b = ±2π$, with angles measured in degrees).

- The arbitrary sign of $b$ represents the ambiguity in defining a positive rotational direction of an angular frequency.

- Even in defining the transforms in fully ordinary frequency terms ($b = ±2π$), the sign choice reflects the fact that $t$ is as much the _angular frequency_ of $ω$ (and hence requires a directional definition) as $ω$ is to $t$; even if, linguistically, the latter relationship is heavily favoured.

- This sign decision does not have any bearing on the normalisation constraint since it affects each definition oppositely and cancels. Hence, $b$ appears as $|b|$ in that constraint.

\* While it seems clear any $a \in \mathbb{R}$ satisfies the normalisation constraint, it is unclear to me what the full range of valid values for $b$ are.

For example, in a computed (and therefore discrete) Fourier transform, https://reference.wolfram.com/language/ref/FourierParameters.html describes how "_the second parameter needs to be relatively prime to the data length to guarantee invertibility_".

It gives the warning "_the discrete Fourier transform may not be invertible unless [_$b$_] is an integer having no factors in common with the length of the input_".


### Sign convention, $σ = ±1 → b = ±1$
- Choosing $σ = +1$ (and hence $b = 1$) means the _forward_ transform uses $e^{i ω t}$ (and hence rotates anti-clockwise when defining angles in the common, Cartesian plane / Argand diagram, convention), and the _inverse_ transform uses $e^{-i ω t}$.
- Using the reverse $σ = b = -1$ is arguably a lot less intuitive from this perspective.


### Frequency convention, $q = 1$ or $2π → b = 1$ or $2π$
- $q = 1 → b = 1$ results in an "angular frequency transform", using $e^{i ω t}$.
- $q = 2π → b = 2π$ results in an "ordinary frequency transform", using $e^{i 2π ω t}$.

- If choosing $q = b = 2π$, it seems sensible to use a different symbol for frequency, to thoroughly avoid adding any more confusion to this whole matter! ($f$ being the natural choice in physics; although $ξ$ is used in the [wiki](https://en.wikipedia.org/wiki/Fourier_transform#Other_conventions) to, presumably, avoid clashing with the even more commonly used, in maths at least, function symbol.)


### Scaling convention, $m = 1$ or $2π → a = 1$ or $0$
- $m = 1 → a = 1$
- $m = 2π → a = 0$

- This determines how to share, amongst the normalisation constants outside the forward and inverse transform definitions, the necessary $1 / 2π$ that must be their product (assuming $|b| = 1$).


### Converting between $(a, b)$ and $(σ q, m)$
- Despite being perhaps a bit more intuitive, Cook's definitions clearly have a redundant parameter, since it is really only the product $b = σ q$ that is independent.
- A small bit of algebra shows:

$$ (a,b) = (1 - \log_{2π}(m|σ q|), σ q) $$

$$ (σ q, m) = (b, {2π}^{1 - a} / |b|) $$


---
## (4) Common conventions

Adapted from https://mathworld.wolfram.com/FourierTransform.html:

__Unfortunately__, a number of conventions are in widespread use.

For example:

#### Modern physics
- $(a, b) = (0,1)$
- $b = σ q = ±1 × ±1 = 1$
- $(σ, q, m) = (±1, ±1, 2π) = (±, ±1, τ)$

$$ f(ω) = \frac{1}{ \sqrt{2π} } \int_{-∞}^{∞} f(t) e^{i ω t} dt $$

$$ f(t) = \frac{1}{ \sqrt{2π} } \int_{-∞}^{∞} f(ω) e^{-i ω t} d ω $$

#### Pure mathematics / Systems engineering
- $(a, b) = (1,-1)$
- $b = σ q = ±1 × \mp 1 = -1$
- $(σ, q, m) = (±1, \mp 1, 1) = (±, \mp 1, 1)$

$$ f(ω) = \int_{-∞}^{∞} f(t) e^{-i ω t} dt $$

$$ f(t) = \frac{1}{2π} \int_{-∞}^{∞} f(ω) e^{i ω t} d ω $$

- also for 'signal processing', according to https://reference.wolfram.com/language/ref/FourierParameters.html



#### Probability theory
- For computing the "characteristic function"
- $(a, b) = (1,1)$
- $b = σ q = ±1 × ±1 = 1$
- $(σ, q, m) = (±1, ±1, 1) = (±, ±1, 1)$

$$ f(ω) = \int_{-∞}^{∞} f(t) e^{i ω t} dt $$

$$ f(t) = \frac{1}{2π} \int_{-∞}^{∞} f(ω) e^{-i ω t} d ω $$


#### Classical physics
- $(a,b) = (-1,1)$
- $b = σ q = ±1 × ±1 = 1$
- $(σ, q, m) = (±1, ±1, 4π^2) = (±, ±1, τ^2)$


$$ f(ω) = \frac{1}{2π} \int_{-∞}^{∞} f(t) e^{i ω t} dt $$

$$ f(t) = \int_{-∞}^{∞} f(ω) e^{-i ω t} d ω $$ 
- also for 'data analysis', according to https://reference.wolfram.com/language/ref/FourierParameters.html

#### Signal processing
- $(a,b) = (0,-2π)$
- $b = σ q = ±1 × \mp 2π = -2π$
- $(σ, q, m) = (±1, \mp 2π, 2π) = (±, ±τ, τ)$

$$ f(ω) = \int_{-∞}^{∞} f(t) e^{-2π i ω t} dt $$

$$ f(t) = \int_{-∞}^{∞} f(ω) e^{2π i ω t} d ω $$


---
## (5) Handy theorems

Adapted from https://www.johndcook.com/blog/fourier-theorems/


### Integration (depends only on $m$):
- _"The integral of a function is proportional to its Fourier transform evaluated at 0"_

- In general

$$ \int_{-∞}^{∞} f(t) dt = \sqrt{m} \ f(ω = 0) $$

- In particular for the 'modern physics' convention, $m = 2π$

$$ f(ω = 0) = \frac{1}{ \sqrt{2π} } \int_{-∞}^{∞} f(t) dt $$


### Shift (depends only on $b = σ q$):
- _"Shifting the argument of a function rotates its Fourier transform"_

- In general

$$ \text{FT}_{a b}\lbrace f(t - h) \rbrace  = e^{i b h ω} f(ω) $$

$$\text{FT}_{σ q m}\lbrace f(t - h) \rbrace = \exp(i σ q h ω) f(ω) $$

- In particular for the 'modern physics' convention, $b = 1$

$$ \text{FT}_{0,1}\lbrace f(t - h) \rbrace = e^{i h ω} f(ω) $$


### Parseval's theorem
- Defined using the inner product $\braket{•,•}$ of functions $f, g \in \mathbb{C}$

$$ \braket{f, g} = \int_{-∞}^{∞} f(t) \ g^{*}(t) dt $$

- It can then be stated, using the 'modern physics' convention $(a,b) = (0, 1)$, very nicely as

$$ \braket{f(t), g(t)} = \braket{f(ω), g(ω)} $$

- Other conventions often include factors of $2π$ or $1 / 2π$


### Plancherel's theorem
- A special case of Parseval's where $g = f$, hence is also stated nicely under the 'modern physics' convention as

$$ \int_{-∞}^{∞} |f(t)|^2 dt = \int_{-∞}^{∞} |f(ω)|^2 dω $$

- In this case, other conventions often include factors of $\sqrt{2π}$ or $1 / \sqrt{2π}$


### Convolution (depends only on $m$)
- _"The Fourier Transform of a convolution of two functions is proportional to the product of the Fourier transforms of each function"_

- Defined for two functions $f, g$ as

$$ (f * g)(t) = \int_{-∞}^{∞} f(t - t')g(t') dt' $$

- In general

$$ \text{FT} \lbrace (f * g) \rbrace = \sqrt{m} f(ω)g(ω) $$

- In particular for the 'modern physics' convention, $m = 2π$
  
$$ \text{FT} \lbrace (f * g) \rbrace = \sqrt{2π} f(ω)g(ω) $$


### Derivative (depends only on $b = σ q$):
- Commonly used for time derivative to derive equations of motion
- Derived below (adapted from [this StackExchange](https://math.stackexchange.com/questions/430858/fourier-transform-of-derivative) that uses [integration by parts](https://en.wikipedia.org/wiki/Integration_by_parts)):

$$ \int u \ dv = uv - \int v \ du $$

$$ u = C \ e^{i b ω t}; \ C = \sqrt{ \frac{|b|}{(2π)^{1 - a}} } $$

$$ du = i b ω \ u \ dt $$

$$ v = f(t) $$

$$ dv = \dot{f}(t) \ dt $$

$$ \therefore $$

$$ \dot{f}(ω) = C \int_{-∞}^{∞} \dot{f}(t) e^{i b ω t} dt $$

$$ \dot{f}(ω) = \int_{-∞}^{∞} u \ dv $$

$$ \dot{f}(ω) = u \ f(t) - \int_{-∞}^{∞} f(t) \ i b ω \ u \ dt $$

$$ \dot{f}(ω) = 0 - i b ω C \int_{-∞}^{∞} e^{i b ω t} f(t) \ dt  $$

$$ \dot{f}(ω) = - i b ω f(ω) $$ 

- Noting the _key_ assumption: $f(t → ±∞) = 0$

- Thus, the result of this handy theorem only relies on the choice of convention parameter $b$

$$ \dot{f}(ω) = -i b ω f(ω) $$

- In particular for the 'modern physics' convention, $b = 1$

$$ \dot{f}(ω) = -i ω f(ω) $$

- This generalises iteratively for multiple derivatives

$$ \frac{d^n}{dt^n} f(ω) = (-i b ω)^n f(ω) $$

- Notably, this result means the choice of convention affects the susceptibility for a damped harmonic oscillator, i.e. from the equation of motion
  
$$ \ddot{x}(t) + Γ\dot{x}(t) + ω_0^2 x(t) = \frac{1}{m} F(t) $$
    
The Fourier transform becomes
    
$$ (-i b ω)^2 x(ω) + (-i b ω) Γ x(ω) + ω_0^2 x(ω) = \frac{1}{m} F(ω) $$
    
Hence, the susceptiblity/response function $\chi$, defined by $x(ω) = \chi(ω)F(ω)$, becomes
    
$$ \chi(ω) = \frac{1/m}{ω_0^2 - b^2 ω^2 - i b Γ ω} $$

## (6) Examples in the wild

[Optomechanical sideband asymmetry explained by stochastic electrodynamics, L. Novotny, M. Frimmer, A. Militaru, A. Norrman, O. Romero-Isart, and P. Maurer; Phys. Rev. A 106, 043511 – Published 17 October 2022](https://journals.aps.org/pra/pdf/10.1103/PhysRevA.106.043511)

- Defined before Eq. (24):

$$ \textbf{E}( \textbf{r}, ω) = (2π)^{-1} \int_\mathbb{R} dt \ \textbf{E}( \textbf{r}, t) \exp(i ω t) $$

- which implies the 'classical physics' convention:
    - $(a, b) = (-1, 1)$ or
    - $b = σ q = ±1 × ±1 = 1$
    - $(σ, q, m) = (±1, ±1, 4π^2) = (±, ±1, τ^2)$.

- Interestingly, this one isn't listed in John Cook's blog!

- This also means that the suscpetibility function they reportin Eq. (6) is

$$ \chi(ω) = [m(ω_0^2 - ω^2 - i \gamma ω)]^{-1} $$

[Error Correction for Continuous Quantum Variables, Samuel L. Braunstein, Phys. Rev. Lett. 80, 4084 – Published 4 May 1998](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.80.4084)

 "_We shall find it convenient to use a units-free notation where_

$$ \text{position} = x \times (\text{scale length}) $$

$$ \text{momentum} = p / (\text{scale length}) $$

_where_ $x$ _is a scaled length,_ $p$ _is a scaled momentum, and we have taken_ $\hbar =­ \frac{1}{2}$ _. (We henceforth drop the modifier “scaled".)_

_The position basis eigenstates_ $\ket{x}$ _are normalized according to_ $\braket{x' | x} = δ(x' - x)$ _­with the momentum basis given by_

$$ \ket{x} = \frac{1}{\sqrt{π}} \int dp \  e^{-2i x p} \ket{p} $$

_To avoid confusion we shall work in the position basis throughout and so define the Fourier transform as an active operation on a state by_

$$ \hat{\mathbb{F}} \ket{x} = \frac{1}{\sqrt{π}} \int dy \  e^{2i x y} \ket{y} $$

_where both_ $x$ _and_ $y$ _are variables in the position basis. Note that Eqs. (3) and (4) correspond to a change of representation and a physical change of the state, respectively._"

- This implies $m = π$ and $b = 2$, overall implying:
    - $(a, b) = (0, 2)$ or
    - $(σ q, m) = (2, π) = (2, τ/2)$.

- This one isn't listed in Wolfram MathWorld __or__ John Cook's blog!

[Quantum Theory of Optical Homodyne and Heterodyne Detection, M.J. Collett , R. Loudon  & C.W. Gardiner, Pages 881-902 | Received 03 Dec 1986, Published online: 01 Mar 2007](https://www.tandfonline.com/doi/abs/10.1080/09500348714550811)

"_The time-dependent input operators are defined by_"

$$ \hat{a}(t) = (2π)^{-1/2} \int dω \exp(-i ω t) \hat{a}(ω) $$

- Since this is an _inverse_ transform, this implies the 'modern physics' convention:
    - $(a, b) = (0,1)$
    - $b = σ q = ±1 × ±1 = 1$
    - $(σ, q, m) = (±1, ±1, 2π) = (±, ±1, τ)$

[Random Data: Analysis and Measurement Procedures, Author(s):Julius S. Bendat, Allan G. Piersol, First published:21 January 2010, Print ISBN:9780470248775 |Online ISBN:9781118032428 |DOI:10.1002/9781118032428](https://onlinelibrary.wiley.com/doi/book/10.1002/9781118032428)

Page 118

_"5.2.1 Spectra via Correlation Functions_

_... Then Fourier transforms of_ $R(τ)$ _will exist as defined by"_

$$ S_{xx}(f) = \int_{-∞}^{+∞} R_{xx}(τ) \ e^{-j 2π f τ} dτ $$

- This is the 'signal processing' convention $(a,b) = (0, -2π)$
    - $(a,b) = (0,-2π)$
    - $b = σ q = ±1 × \mp 2π = -2π$
    - $(σ, q, m) = (±1, \mp 2π, 2π) = (±, ±τ, τ)$
