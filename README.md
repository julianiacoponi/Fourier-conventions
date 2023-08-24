# FOURIER CONVENTIONS
This is all heavily based on the links given, but I've added some extra expressions + intuitions to help connect the ideas better!

---
## (1) https://mathworld.wolfram.com/FourierTransform.html

_"In general, the Fourier transform pair may be defined using two arbitrary constants $(a, b)$:_

$$
\text{FT} \lbrace f(t) \rbrace
=
f(\omega)
=
\sqrt{ \frac{|b|}{(2\pi)^{1 - a}} }
\int_{-\inf}^{\inf}
f(t) e^{i b \omega t}
dt
$$

$$
\text{FT}^{-1} \lbrace f(\omega) \rbrace
=
f(t)
=
\sqrt{ \frac{|b|}{(2\pi)^{1 + a}} }
\int_{-\inf}^{\inf}
f(\omega) e^{-i b \omega t}
d \omega
$$

_The Fourier transform $f(\omega)$ of a function $f(t)$ is implemented by the Wolfram Language as `FourierTransform[f, t, \omega]`, and different choices of $a$ and $b$ can be used by passing the optional `FourierParameters → {a, b}` option._

_By default, the Wolfram Language takes `FourierParameters` as `{a, b} = {0,1}`*."_

*This convention is described later as 'modern physics'


---
## (2) https://www.johndcook.com/blog/fourier-theorems/

This link shows a lot of handy theorems and how they convert between the different definitions!

_"There are several slightly different ways to define a Fourier transform. This means that when you look up a theorem about the Fourier transform you have to ask yourself which convention the source is using. All the common conventions can be summarized in the following definition:_

$$
\text{FT} \lbrace f(t) \rbrace
=
f(\omega)
=
\frac{1}{\sqrt{m}}
\int_{-\inf}^{\inf}
f(t) \exp(i \sigma q \omega t)
dt
$$

Implying
$$
\text{FT}^{-1} \lbrace f(\omega) \rbrace
=
f(t)
=
\frac{\sqrt{m} |\sigma q|}{2\pi}
\int_{-\inf}^{\inf}
f(\omega) \exp(-i \sigma q \omega t)
d\omega
$$

where
- _Sign convention_ $\sigma = +1$ or $-1$,
- _Frequency convention_ $q = 2\pi$ or $1$,
- _Scaling convention_ $m = 1$ or $2\pi$,

"_This means there are eight potential definitions, one for each choice of $\sigma$, $q$, and $m$, though only six* of these are widely used._"

*As will become clear, there are in fact more than 6 commonly used definitions...


---
## (3) Understanding the parameters defining different conventions
An intuituion on the presence of these arbitrary parameters is that they represent two independent free choices to be made when defining the Fourier transform pair:


#### Normalisation parameter, $a \in \mathbb{R}$
- Choosing parameter $a$ can be seen as an arbitrary choice of how to satisfy the only actual meaningful constraint:
$$
C_- \ C_+ = |b|/2\pi
$$

(defining $C_± = \sqrt{ |b| / (2\pi)^{1 ± a} }$ as the normalisation constants outside the forward ($C_-$) and inverse ($C_+$) transforms).


#### Frequency/Rotation parameter, $b \in \ ?$*
- Choosing parameter $b$ can be seen as another arbitrary decision of how much one would like to define the transforms in:
    - angular frequency terms ($b = ±1$, with angles measured in radians), or
    - ordinary frequency terms ($b = ±2\pi$, with angles measured in degrees).

- The arbitrary sign of $b$ represents the ambiguity in defining a positive rotational direction of an angular frequency.

- Even in defining the transforms in fully ordinary frequency terms ($b = ±2\pi$), the sign choice reflects the fact that $t$ is as much the _angular frequency_ of $\omega$ (and hence requires a directional definition) as $\omega$ is to $t$; even if, linguistically, the latter relationship is heavily favoured.

- This sign decision does not have any bearing on the normalisation constraint since it affects each definition oppositely and cancels. Hence, $b$ appears as $|b|$ in that constraint.

\* While it seems clear any $a \in \mathbb{R}$ satisfies the normalisation constraint, it is unclear to me what the full range of valid values for $b$ are.

For example, in a computed (and therefore discrete) Fourier transform, https://reference.wolfram.com/language/ref/FourierParameters.html describes how _"the second parameter needs to be relatively prime to the data length to guarantee invertibility"_.

It gives the warning _"the discrete Fourier transform may not be invertible unless [$b$] is an integer having no factors in common with the length of the input"_.


#### Sign convention, $\sigma = ±1 → b = ±1$
- Choosing $\sigma = +1$ (and hence $b = 1$) means the _forward_ transform uses $e^{i \omega t}$ (and hence rotates anti-clockwise when defining angles in the common, Cartesian plane / Argand diagram, convention), and the _inverse_ transform uses $e^{-i \omega t}$.
- Using the reverse $\sigma = b = -1$ is arguably a lot less intuitive from this perspective.


#### Frequency convention, $q = 1$ or $2\pi → b = 1$ or $2\pi$
- $q = 1 → b = 1$ results in an "angular frequency transform" using $e^{i \omega t}$.
- $q = 2\pi → b = 2\pi$ results in an "ordinary frequency transform" $e^{i 2\pi \omega t}$.

- If choosing $q = b = 2\pi$, it seems sensible to use a different symbol for frequency, to thoroughly avoid adding any more confusion to this whole matter! ($f$ being the natural choice in physics; although $\xi$ is used in the [wiki](https://en.wikipedia.org/wiki/Fourier_transform#Other_conventions) to, presumably, avoid clashing with the even more commonly used, in maths at least, function symbol.)


#### Scaling convention, $m = 1$ or $2\pi → a = 1$ or $0$
- $m = 1 → a = 1$
- $m = 2\pi → a = 0$

- This determines how to share, amongst the normalisation constants outside the forward and inverse transform definitions, the necessary $1 / 2\pi$ that must be their product (assuming $|b| = 1$).


#### Converting between $(a, b)$ and $(\sigma q, m)$
- Despite being perhaps a bit more intuitive, Cook's definitions clearly have a redundant parameter, since it is really only the product $b = \sigma q$ that is independent.
- A small bit of algebra shows:

$$
(a,b) = (1 - \log_{2\pi}(m|\sigma q|), \sigma q)
$$

$$
(\sigma q, m) = (b, {2\pi}^{1 - a} / |b|)
$$


---
## (4) Common conventions

Adapted from https://mathworld.wolfram.com/FourierTransform.html:

__Unfortunately__, a number of conventions are in widespread use.

For example:

#### Modern physics
- $(a, b) = (0,1)$
- $b = \sigma q = ±1 × ±1 = 1$
- $(\sigma, q, m) = (±1, ±1, 2\pi) = (±, ±1, \tau)$

$$
f(\omega)
=
\frac{1}{ \sqrt{2\pi} }
\int_{-\inf}^{\inf}
f(t) e^{i \omega t}
dt
$$

$$
f(t)
=
\frac{1}{ \sqrt{2\pi} }
\int_{-\inf}^{\inf}
f(\omega) e^{-i \omega t}
d \omega
$$

#### Pure mathematics / Systems engineering
- $(a, b) = (1,-1)$
- $b = \sigma q = ±1 × \mp 1 = -1$
- $(\sigma, q, m) = (±1, \mp 1, 1) = (±, \mp 1, 1)$

$$
f(\omega)
=
\int_{-\inf}^{\inf}
f(t) e^{-i \omega t}
dt
$$

$$
f(t)
=
\frac{1}{2\pi}
\int_{-\inf}^{\inf}
f(\omega) e^{i \omega t}
d \omega
$$

- also for 'signal processing', according to https://reference.wolfram.com/language/ref/FourierParameters.html



#### Probability theory
- For computing the "characteristic function"
- $(a, b) = (1,1)$
- $b = \sigma q = ±1 × ±1 = 1$
- $(\sigma, q, m) = (±1, ±1, 1) = (±, ±1, 1)$

$$
f(\omega)
=
\int_{-\inf}^{\inf}
f(t) e^{i \omega t}
dt
$$

$$
f(t)
=
\frac{1}{2\pi}
\int_{-\inf}^{\inf}
f(\omega) e^{-i \omega t}
d \omega
$$


#### Classical physics
- $(a,b) = (-1,1)$
- $b = \sigma q = ±1 × ±1 = 1$
- $(\sigma, q, m) = (±1, ±1, 4\pi^2) = (±, ±1, \tau^2)$


$$
f(\omega)
=
\frac{1}{2\pi}
\int_{-\inf}^{\inf}
f(t) e^{i \omega t}
dt
$$

$$
f(t)
=
\int_{-\inf}^{\inf}
f(\omega) e^{-i \omega t}
d \omega
$$
- also for 'data analysis', according to https://reference.wolfram.com/language/ref/FourierParameters.html

#### Signal processing
- $(a,b) = (0,-2\pi)$
- $b = \sigma q = ±1 × \mp 2\pi = -2\pi$
- $(\sigma, q, m) = (±1, \mp 2\pi, 2\pi) = (±, ±\tau, \tau)$

$$
f(\omega)
=
\int_{-\inf}^{\inf}
f(t) e^{-2\pi i \omega t}
dt
$$

$$
f(t)
=
\int_{-\inf}^{\inf}
f(\omega) e^{2\pi i \omega t}
d \omega
$$


---
## (5) Handy theorems

Adapted from https://www.johndcook.com/blog/fourier-theorems/


### Integration (depends only on $m$):
- _"The integral of a function is proportional to its Fourier transform evaluated at 0"_

- In general
$$
\int_{-\inf}^{\inf} f(t) dt
=
\sqrt{m} \
f(\omega = 0)
$$

- In particular for the 'modern physics' convention, $m = 2\pi$:
$$
f(\omega = 0)
=
\frac{1}{ \sqrt{2\pi} }
\int_{-\inf}^{\inf} f(t) dt
$$


### Shift (depends only on $b = \sigma q$):
- _"Shifting the argument of a function rotates its Fourier transform"_

- In general:
$$
\text{FT}_{a b}\lbrace f(t - h) \rbrace  = e^{i b h \omega} f(\omega)
$$
$$
\text{FT}_{\sigma q m}\lbrace f(t - h) \rbrace = \exp(i \sigma q h \omega) f(\omega)
$$

- In particular for the 'modern physics' convention, $b = 1$:
$$
\text{FT}_{0,1}\lbrace f(t - h) \rbrace = e^{i h \omega} f(\omega)
$$


### Parseval's theorem
- Defined using the inner product $\lang •,• \rang$ of functions $f, g \in \mathbb{C}$:
$$
\lang f, g \rang
=
\int_{-\inf}^{\inf}
f(t) \ g^{*}(t)
dt
$$

- It can then be stated, using the 'modern physics' convention $(a,b) = (0, 1)$, very nicely as:
$$
\lang f(t), g(t) \rang
=
\lang f(\omega), g(\omega) \rang
$$

- Other conventions often include factors of $2\pi$ or $1 / 2\pi$.


### Plancherel's theorem
- A special case of Parseval's where $g = f$, hence is also stated nicely under the 'modern physics' convention as:
$$
\int_{-\inf}^{\inf}
|f(t)|^2
dt
=
\int_{-\inf}^{\inf}
|f(\omega)|^2
d\omega
$$

- In this case, other conventions often include factors of $\sqrt{2\pi}$ or $1 / \sqrt{2\pi}$.


### Convolution (depends only on $m$)
- _"The Fourier Transform of a convolution of two functions is proportional to the product of the Fourier transforms of each function"_

- Defined for two functions $f, g$ as:
$$
(f * g)(t)
=
\int_{-\inf}^{\inf}
f(t - t')g(t')
dt'
$$

- In general:
$$
\text{FT} \lbrace (f * g) \rbrace
=
\sqrt{m}
f(\omega)g(\omega)
$$

- In particular for the 'modern physics' convention, $m = 2\pi$:
$$
\text{FT} \lbrace (f * g) \rbrace
=
\sqrt{2\pi}
f(\omega)g(\omega)
$$


### Derivative (depends only on $b = \sigma q$):
- Commonly used for time derivative to derive equations of motion
- Derived below (adapted from [this StackExchange](https://math.stackexchange.com/questions/430858/fourier-transform-of-derivative) that uses [integration by parts](https://en.wikipedia.org/wiki/Integration_by_parts)):

$$
\int u \ dv = uv - \int v \ du
$$

$$
u = C \ e^{i b \omega t}; \ C = \sqrt{ \frac{|b|}{(2\pi)^{1 - a}} }
$$
$$
du = i b \omega \ u \ dt
$$

$$
v = f(t)
$$
$$
dv = \dot{f}(t) \ dt
$$


$$
\therefore
$$
$$
\dot{f}(\omega)
=
C
\int_{-\inf}^{\inf}
\dot{f}(t)
e^{i b \omega t}
dt

\\ =
\int_{-\inf}^{\inf}
u \ dv

\\=
\left[ u \ f(t) \right]_{-\inf}^{+\inf}
-
\int_{-\inf}^{+\inf} f(t) \ i b \omega \ u \ dt

\\ =
0
- i b \omega C \int_{-\inf}^{+\inf} e^{i b \omega t} f(t) \ dt

\\ =
- i b \omega f(\omega)
$$

- Noting the _key_ assumption: $f(t → ±\inf) = 0$.

- Thus, the result of this handy theorem only relies on the choice of convention parameter $b$!
$$
\dot{f}(\omega) = -i b \omega f(\omega)
$$

- In particular for the 'modern physics' convention, $b = 1$:
$$
\dot{f}(\omega) = -i \omega f(\omega)
$$

- This generalises iteratively for multiple derivatives:
$$
\frac{d^n}{dt^n} f(\omega) = (-i b \omega)^n f(\omega)
$$

- Notably, this result means the choice of convention affects the susceptibility for a damped harmonic oscillator!
    - i.e. from the equation of motion:
        $$
        \ddot{x}(t) + \Gamma\dot{x}(t) + \omega_0^2 x(t)
        =
        \frac{1}{m} F(t)
        $$
    - The Fourier transform becomes:
        $$
        (-i b \omega)^2 x(\omega) + (-i b \omega) \Gamma x(\omega) + \omega_0^2 x(\omega)
        =
        \frac{1}{m} F(\omega)
        $$
    - Hence, the susceptiblity/response function $\chi$, defined by $x(\omega) = \chi(\omega)F(\omega)$, becomes:
        $$
        \chi(\omega) = \frac{1/m}{\omega_0^2 - b^2 \omega^2 - i b \Gamma \omega}
        $$

## (6) Examples in the wild

[Optomechanical sideband asymmetry explained by stochastic electrodynamics, L. Novotny, M. Frimmer, A. Militaru, A. Norrman, O. Romero-Isart, and P. Maurer; Phys. Rev. A 106, 043511 – Published 17 October 2022](https://journals.aps.org/pra/pdf/10.1103/PhysRevA.106.043511)

- Defined before Eq. (24):

$$
\textbf{E}( \textbf{r}, \omega)
=
(2\pi)^{-1}
\int_\mathbb{R}
dt \
\textbf{E}( \textbf{r}, t)
\exp(i \omega t)
$$

- which implies the 'classical physics' convention:
    - $(a, b) = (-1, 1)$ or
    - $b = \sigma q = ±1 × ±1 = 1$
    - $(\sigma, q, m) = (±1, ±1, 4\pi^2) = (±, ±1, \tau^2)$.

- Interestingly, this one isn't listed in John Cook's blog!

- This also means that the suscpetibility function they reportin Eq. (6) is
$$
\chi(\omega) = [m(\Omega_0^2 - \omega^2 - i \gamma \omega)]^{-1}
$$

[Error Correction for Continuous Quantum Variables, Samuel L. Braunstein, Phys. Rev. Lett. 80, 4084 – Published 4 May 1998](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.80.4084)

 _"We shall find it convenient to use a units-free notation where_
$$
\text{position} = x \times (\text{scale length})
$$

$$
\text{momentum} = p / (\text{scale length})
$$

_where $x$ is a scaled length, $p$ is a scaled momentum, and we have taken $\hbar =­ \frac{1}{2}$. (We henceforth drop the modifier “scaled.”)_

_The position basis eigenstates $\ket{x}$ are normalized according to $\bra{x'} \ket{x} = δ(x' - x)$ ­with the momentum basis given by_
$$
\ket{x} = \frac{1}{\sqrt{\pi}} \int dp \  e^{-2i x p} \ket{p}
$$
 _To avoid confusion we shall work in the position basis throughout and so define the Fourier transform as an active operation on a state by_
$$
\hat{\mathbb{F}} \ket{x} = \frac{1}{\sqrt{\pi}} \int dy \  e^{2i x y} \ket{y}
$$
_where both $x$ and $y$ are variables in the position basis. Note that Eqs. (3) and (4) correspond to a change of representation and a physical change of the state, respectively."_

- This implies $m = \pi$ and $b = 2$, overall implying:
    - $(a, b) = (0, 2)$ or
    - $(\sigma q, m) = (2, \pi) = (2, \tau/2)$.

- This one isn't listed in Wolfram MathWorld __or__ John Cook's blog!

[Quantum Theory of Optical Homodyne and Heterodyne Detection, M.J. Collett , R. Loudon  & C.W. Gardiner, Pages 881-902 | Received 03 Dec 1986, Published online: 01 Mar 2007](https://www.tandfonline.com/doi/abs/10.1080/09500348714550811)

_"The time-dependent input operators are defined by"_

$$
\hat{a}(t) = (2\pi)^{-1/2} \int d\omega \exp(-i \omega t) \hat{a}(\omega)
$$

- Since this is an _inverse_ transform, this implies the 'modern physics' convention:
    - $(a, b) = (0,1)$
    - $b = \sigma q = ±1 × ±1 = 1$
    - $(\sigma, q, m) = (±1, ±1, 2\pi) = (±, ±1, \tau)$

[Random Data: Analysis and Measurement Procedures, Author(s):Julius S. Bendat, Allan G. Piersol, First published:21 January 2010, Print ISBN:9780470248775 |Online ISBN:9781118032428 |DOI:10.1002/9781118032428](https://onlinelibrary.wiley.com/doi/book/10.1002/9781118032428)

Page 118

_"5.2.1 Spectra via Correlation Functions_

_... Then Fourier transforms of $R(\tau)$ will exist as defined by"_

$$
S_{xx}(f) = \int_{-\inf}^{+\inf} R_{xx}(\tau) \ e^{-j 2\pi f \tau} d\tau
$$

- This is the 'signal processing' convention $(a,b) = (0, -2\pi)$
    - $(a,b) = (0,-2\pi)$
    - $b = \sigma q = ±1 × \mp 2\pi = -2\pi$
    - $(\sigma, q, m) = (±1, \mp 2\pi, 2\pi) = (±, ±\tau, \tau)$
