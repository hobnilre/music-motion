---
title: "Musical Motion from Shared Partials"
subtitle: "A directed chord relation from ordered harmonic and pseudo-partial coincidences"
author: "Hob Nilre & Bo C. Herlin"
date: "2026-09-28"
abstract: |
  Shared spectral components can describe an ordered relation between two chords. The construction developed here weights consonant partial pairs by their amplitudes and classifies each pair by the order of its two partial labels. The resulting backward, stationary and forward components define a signed direction. We derive the finite construction, its reversal and transposition properties, its dependence on timbre and aggregation, and its raw and normalized forms. An exact three-component model gives a complete twelve-tone transition table and a continuous worked comparison of C major with F major: the components are (63,274,360), giving normalized direction 297/697. The same construction permits directed cycles and balanced opposing contributions within an unchanged chord. These results specify what the descriptor measures and establish concrete questions about its musical interpretation and perceptual relevance.
keywords:
  - harmonic motion
  - partial coincidence
  - chord relations
  - timbre
  - consonance
---

\begingroup\scriptsize
\noindent PDF created: \pdfbuildtimestamp\par
\noindent Latest on GitHub: \url{https://github.com/hobnilre/music-motion}\par
\endgroup

# A direction carried by shared sound

A chord transition can share spectral material while changing the roles of the components that supply it. A pitch represented as a low-order component of one chord may coincide with a higher-order component of the next. Giving those roles an order makes the coincidence directional. Reversing the transition reverses the role comparison, even though the coincident pitches remain the same.

This article develops that idea into an explicit relation between chords. For every partial in the first chord and every partial in the second, a consonance weight measures their proximity under a declared pitch comparison. An amplitude product scales that weight. The order of the partial labels assigns it to a backward, stationary or forward component. Direction is the forward component minus the backward component.

The construction originates in the authors' Kotlin sonance models. Their shared mathematical idea admits several realizations: actual harmonic partials or a compact pitch-class template, continuous or coincidence-only weights, and different aggregation and normalization choices. We state these choices explicitly and derive the consequences. The article's worked construction can be reproduced from its definitions and tables without software.

The principal example uses three ordered components at offsets zero, seven and four semitones, weighted twelve, seven and nine. This gives an exact finite account of the C-major-to-F-major transition, including the opposing contributions that a single direction score conceals. It also supplies a complete transition table for individual pitch classes and hence every chord comparison in that model.

Spectral composition and tuning already have an established role in consonance modelling: [Sethares (1993)][sethares] relates a timbre's spectrum to local minima of dissonance as tuning varies. Here the additional object is the order of the component roles across an ordered pair of chords. Its musical interpretation requires its own evidence. Consonance itself has several perceptual contributors; [Harrison and Pearce (2020)][harrison] analyse interference, harmonicity and cultural familiarity. We therefore distinguish the mathematical relation, the choice of a musical interpretation and a perceptual claim about listeners.

# Notes, partials and ordered roles

Let $A$ and $B$ be finite lists of note occurrences. Repeated notes remain separate occurrences. A note with pitch $p$ is expanded into components
\begin{equation}
\mathcal P(p)=\{(p+\delta_i,a_i,\ell_i):i=0,\ldots,h-1\},
\label{eq:profile}
\end{equation}
where $\delta_i$ is a pitch offset, $a_i\geq0$ is an amplitude weight and $\ell_i$ is an ordered label. A profile can depend on the note when that dependence is declared. The worked examples use one fixed profile and unit note amplitudes throughout.

Pitch is measured in semitones. A frequency $f>0$ has coordinate $p=p_\ast+12\log_2(f/f_\ast)$ for declared reference values $p_\ast,f_\ast$. This coordinate makes a common frequency scaling a pitch translation. Phase, duration, onset separation, dynamics through time and voice identity are absent from the present descriptor. The amplitude weight is a factor in the comparison rule; it is not an acoustic-energy account.

For harmonic partials numbered $n=1,\ldots,h$, a natural choice is
\begin{equation}
\delta_{n-1}=12\log_2 n,\qquad \ell_{n-1}=n-1.
\label{eq:harmonic-profile}
\end{equation}
The zero-based label has the same ordering as the harmonic number. Amplitudes still require a separate timbral choice, such as $a_{n-1}=1/n$.

A pseudo-partial profile instead declares a finite collection of representative offsets and an ordering of their roles. In our central example,
\begin{equation}
(\delta_0,\delta_1,\delta_2)=(0,7,4),\qquad
(a_0,a_1,a_2)=(12,7,9),\qquad
(\ell_0,\ell_1,\ell_2)=(0,1,2).
\label{eq:three-profile}
\end{equation}
The labels order root, fifth and major-third roles. Their order is part of the model: the seven-semitone component precedes the four-semitone component. Sorting these offsets by pitch would change the relation if the labels were reassigned by position. These three components represent a chosen musical template; they are not the first three frequencies of a harmonic spectrum.

Flatten the expansions of all note occurrences into component lists $\widetilde A$ and $\widetilde B$. Write a component as $u=(x_u,a_u,\ell_u)$ or $v=(x_v,a_v,\ell_v)$. Every member of $\widetilde A$ is compared with every member of $\widetilde B$. No voice assignment or one-to-one matching is involved.

# What counts as a consonant coincidence

## Pitch comparison

Three pitch comparisons occur in the construction's implementations. The absolute distance retains register:
\begin{equation}
d_{\mathrm{abs}}(x,y)=|x-y|.
\label{eq:absolute-distance}
\end{equation}
The circular distance folds by the twelve-semitone octave:
\begin{equation}
d_{\mathrm{circ}}(x,y)=\min_{k\in\mathbb Z}|x-y-12k|,\qquad 0\leq d_{\mathrm{circ}}\leq6.
\label{eq:circular-distance}
\end{equation}
A third comparison first chooses representatives $\bar x,\bar y\in[0,12)$ and then uses $|\bar x-\bar y|$. This last distance has a seam at zero: representatives $11.9$ and $0.1$ are $11.8$ apart, although their circular distance is $0.2$. After a common translation by $0.2$, the representative distance becomes $0.2$. Consequently, representative distance does not generally preserve common-transposition invariance for a continuous kernel.

For integer pitches and exact coincidence, both folded comparisons test equality modulo twelve. The three-component example uses this equality. Register-sensitive and octave-folded models answer different questions and must be specified separately.

## Consonance kernel

Choose a positive width $\rho$, a positive exponent $q$ and a nonnegative curve $R$. The consonant component used for motion is
\begin{equation}
C(d)=
\begin{cases}
1-R(d/\rho)^q,&0\leq d<\rho,\\
0,&d\geq\rho.
\end{cases}
\label{eq:kernel}
\end{equation}
The underlying sonance construction also has dissonant and residual components. Motion uses only $C$. In particular, a distant pair assigned to the residual component contributes no directional weight.

For a nonnegative-weight interpretation, require $0\leq R(x)^q\leq1$ on $0\leq x<1$. This is an assumption to verify for the chosen curve. It is not guaranteed by naming a curve a dissonance model. Two useful cases make the role of the kernel explicit.

A binary curve with $R(x)=0$ for $x<1/2$, $R(x)=1$ for $1/2\leq x<3/2$, and $R(x)=0$ thereafter yields $C(d)=1$ exactly when $d<\rho/2$. With $\rho=1$ and integer component pitches, this is precisely a coincidence test. The half-width boundary is strict.

For $q=1$ and the polynomial family $R(x)=2x^\nu/(1+x^{2\nu})$, $\nu>0$, the local consonance weight is
\begin{equation}
C(d)=\frac{(1-x^\nu)^2}{1+x^{2\nu}},\qquad x=d/\rho<1,
\label{eq:polynomial-kernel}
\end{equation}
with zero beyond the cutoff. The numerator identity follows by subtracting $2x^\nu$ from $1+x^{2\nu}$. Thus $0\leq C\leq1$ and $C(0)=1$ follow directly.

These definitions describe the selected mathematics. The kernel's width and shape are modelling inputs; interpreting their values as an auditory law requires independent evidence.

# The directed comparison

For each cross-pair define
\begin{equation}
w_{uv}=a_u a_v C\bigl(d(x_u,x_v)\bigr).
\label{eq:pair-weight}
\end{equation}
The additive backward, stationary and forward components are
\begin{equation}
\begin{aligned}
B(A,B)&=\sum_{u\in\widetilde A}\sum_{v\in\widetilde B}w_{uv}\,\mathbf1_{\ell_u>\ell_v},\\
S(A,B)&=\sum_{u\in\widetilde A}\sum_{v\in\widetilde B}w_{uv}\,\mathbf1_{\ell_u=\ell_v},\\
F(A,B)&=\sum_{u\in\widetilde A}\sum_{v\in\widetilde B}w_{uv}\,\mathbf1_{\ell_u<\ell_v}.
\end{aligned}
\label{eq:triple}
\end{equation}
The symbols $B(A,B)$ and the chord name $B$ have different roles: the former is a scalar component of the ordered comparison. When the chord arguments are clear, write the triple simply as $(B,S,F)$.

The three comparisons partition every pair. Therefore total supported coincidence and signed direction satisfy
\begin{equation}
T=B+S+F=\sum_{u,v}w_{uv},\qquad D=F-B.
\label{eq:total-direction}
\end{equation}
A positive contribution occurs when a lower-labelled component of the first chord coincides with a higher-labelled component of the second. Equal labels contribute to $S$, even when they belong to different note occurrences.

For $T>0$, the normalized construction is
\begin{equation}
(\widehat B,\widehat S,\widehat F)=\frac{(B,S,F)}{T},\qquad
\widehat D=\frac{F-B}{T}.
\label{eq:normalization}
\end{equation}
For nonnegative weights, $-1\leq\widehat D\leq1$. More precisely, $|\widehat D|\leq1-\widehat S$. This follows from $|F-B|\leq F+B=T-S$.

At $T=0$, the nonnegative additive triple is $(0,0,0)$. Retaining that zero triple is the implementation's normalization convention. It carries no supported coincidence and is not a distribution summing to one. Keep $T$ alongside the normalized direction so that a zero-support comparison is distinguishable from a supported balance of opposing components.

When $T>0$, choosing a pair with probability $w_{uv}/T$ gives another exact interpretation: $\widehat D$ is the expected value of $\operatorname{sgn}(\ell_v-\ell_u)$. This interpretation belongs to the additive nonnegative construction; it follows from its definition and is not a probability of a listener reporting motion.

# Structural properties

\begin{theorem}[Reversal]
Suppose the component profiles remain attached to their respective chords and the pair kernel is symmetric in pitch. Reversing the chord order exchanges the backward and forward components, preserves the stationary component and total support, and negates the direction. The same conclusions hold after normalization wherever $T>0$.
\end{theorem}

To prove this, exchange $u$ and $v$ in every pair. The amplitude product and distance are unchanged, while $\ell_u<\ell_v$ becomes $\ell_v>\ell_u$. Each forward contribution becomes a backward contribution of the same size; equality is preserved. Summing proves the result, and the common denominator $T$ proves its normalized form. $\square$

In particular, comparing a chord with itself gives $D(A,A)=0$. It need not give $B=F=0$. Distinct notes of that chord can supply shared components with different labels, producing equal and opposite contributions. The diagonal contribution $S$ and the opposing contributions contain information that the single number $D$ discards.

\begin{theorem}[Common transposition]
With fixed translated profiles, unchanged amplitudes and labels, and either absolute or circular distance, a common pitch translation of both chords leaves the entire triple unchanged.
\end{theorem}

The two component pitches become $x_u+t$ and $x_v+t$. Their difference is unchanged, so every pair weight and every label comparison is unchanged. The conclusion follows term by term. $\square$

The conclusion requires profiles that actually translate. Register-dependent timbres or amplitudes can break it. The representative-distance comparison discussed above can break it even with otherwise fixed profiles. Its exact-coincidence specialization on integer pitches still has modular transposition invariance.

For the sum rule, multiplying all first-chord amplitudes by $\alpha\geq0$ and all second-chord amplitudes by $\beta\geq0$ multiplies the triple and $D$ by $\alpha\beta$. Normalized components remain unchanged when $\alpha\beta>0$ and $T>0$. Repeating the whole first chord $r$ times and the second $s$ times has the same effect with factor $rs$. Repeating selected notes changes the balance of contributions and may change normalized direction.

Permuting note occurrences or explicitly labelled components leaves the sums unchanged. Applying one strictly increasing relabelling to the common label scale also leaves all comparisons unchanged. Reassigning labels by a new list order, or independently relabelling the two sides on incompatible scales, need not preserve them.

# A complete three-component construction

## The elementary transition table

Use the profile in \eqref{eq:three-profile}, equality modulo twelve, and additive aggregation. Take the first note to have pitch class zero and the second to have pitch class $t$. A component pair contributes when
\begin{equation}
\delta_i\equiv t+\delta_j\pmod {12},
\qquad\text{equivalently}\qquad
 t\equiv\delta_i-\delta_j\pmod {12}.
\label{eq:coincidence-condition}
\end{equation}
There are nine component pairs. The three diagonal pairs yield $t=0$ with stationary weight $12^2+7^2+9^2=274$. The other six yield the complete table below. No fitting or rounding enters these values.

| $t$ (semitones) | $B$ | $S$ | $F$ | $D$ |
|---:|---:|---:|---:|---:|
| 0 | 0 | 274 | 0 | 0 |
| 1 | 0 | 0 | 0 | 0 |
| 2 | 0 | 0 | 0 | 0 |
| 3 | 0 | 0 | 63 | 63 |
| 4 | 108 | 0 | 0 | $-108$ |
| 5 | 0 | 0 | 84 | 84 |
| 6 | 0 | 0 | 0 | 0 |
| 7 | 84 | 0 | 0 | $-84$ |
| 8 | 0 | 0 | 108 | 108 |
| 9 | 63 | 0 | 0 | $-63$ |
| 10 | 0 | 0 | 0 | 0 |
| 11 | 0 | 0 | 0 | 0 |

: Complete single-note transition table for the specified three-component model.

For example, C to F has $t=5$. The first note's root component at zero coincides with the second note's fifth component at $5+7\equiv0$. Labels $0<1$ give a forward contribution $12\cdot7=84$. Reversal, F to C, gives the corresponding backward contribution. Figure \ref{fig:roles} illustrates the roles that make this coincidence directional.

![Ordered roles in a C-to-F comparison. Component positions are schematic; numbers denote pitch classes and model weights. The connecting line marks the shared pitch class zero.](figures/ordered-roles.pdf){#fig:roles width=95%}

\FloatBarrier

The normalized direction is $+1$ for elementary transitions $t=3,5,8$, and $-1$ for $t=4,7,9$. These normalized values conceal the different supported weights $63$, $84$ and $108$. The remaining cases include both a supported stationary comparison at $t=0$ and unsupported comparisons. Reporting the triple and $T$ retains those distinctions.

## From notes to chords

For arbitrary finite chords in this model, sum the appropriate elementary table entry for every ordered note pair. If $m(t)$ denotes the table's triple, then
\begin{equation}
(B,S,F)(A,B)=\sum_{a\in A}\sum_{b\in B}m\bigl((b-a)\bmod12\bigr).
\label{eq:chord-from-table}
\end{equation}
This equation follows by interchanging finite sums over note pairs and component pairs. It supplies every chord comparison in the specified model, including multiplicities.

A second representation exposes the component roles. Define
\begin{equation}
M_{ij}(A,B)=a_i a_j\sum_{a\in A}\sum_{b\in B}
\mathbf1_{a+\delta_i\equiv b+\delta_j\ (\mathrm{mod}\ 12)}.
\label{eq:role-matrix}
\end{equation}
The entries below, on and above the diagonal sum to $B,S,F$, respectively. This is a coincidence matrix, with no constraint that a component be used at most once.

For C major $A=\{0,4,7\}$ and F major $B=\{5,9,0\}$, the three role-specific pitch-class sets are
\begin{align}
A_0&=\{0,4,7\},& A_1&=\{7,11,2\},& A_2&=\{4,8,11\},\\
B_0&=\{5,9,0\},& B_1&=\{0,4,7\},& B_2&=\{9,1,4\}.
\label{eq:expanded-chords}
\end{align}
For instance, $A_0$ and $B_1$ share three pitch classes, so $M_{01}=3\cdot12\cdot7=252$. The full matrix is
\begin{equation}
M(C,F)=
\begin{pmatrix}
144&252&108\\
0&49&0\\
0&63&81
\end{pmatrix}.
\label{eq:cf-matrix}
\end{equation}
Its three sums give
\begin{equation}
(B,S,F)=(63,274,360),\quad T=697,\quad D=297,\quad
\widehat D=\frac{297}{697}.
\label{eq:cf-result}
\end{equation}
The backward contribution is $M_{21}=63$; it comes from the shared class four between $A_2$ and $B_1$. Thus a positive net direction can contain a substantial stationary component and an opposing component. Figure \ref{fig:matrix} keeps those contributions visible.

![The C-major-to-F-major role matrix. Orange, grey and blue cells contribute to backward, stationary and forward components. Values are exact sums in the declared template scale.](figures/role-matrix.pdf){#fig:matrix width=80%}

\FloatBarrier

\Needspace{14\baselineskip}

Some further exact chord comparisons demonstrate the range of this relation. Here G major is $\{7,11,2\}$ and C minor is $\{0,3,7\}$.

| Transition | $(B,S,F)$ | $T$ | $\widehat D$ |
|:---|:---|---:|:---|
| C major to F major | $(63,274,360)$ | 697 | $297/697$ |
| F major to C major | $(360,274,63)$ | 697 | $-297/697$ |
| C major to G major | $(360,274,63)$ | 697 | $-297/697$ |
| G major to C major | $(63,274,360)$ | 697 | $297/697$ |
| C major to C minor | $(84,548,426)$ | 1058 | $171/529$ |
| C major to itself | $(255,822,255)$ | 1332 | $0$ |

: Worked chord comparisons under one fixed profile, coincidence rule and additive aggregation.

These are descriptors of the specified chord relation. For example, the positive C-major-to-C-minor value follows from component-role coincidences. Interpreting it as an increase in tension, a preferred continuation or perceived forward motion is a separate hypothesis.

## Template scaling

The table uses amplitudes $(12,7,9)$ directly, as in the simpler discrete construction. The later sampled-timbre construction divides each template amplitude by the amplitude of its reference component. With reference amplitude twelve and unit note amplitude, its actual profile is $(1,7/12,3/4)$. Every additive pair weight, matrix entry and raw component is therefore divided by $144$.

For C major to F major this gives raw components $(7/16,137/72,5/2)$, total $697/144$ and direction $33/16$. Normalization still gives $297/697$. This scale change is independent of whether the final triple is normalized. A reproducible comparison must specify both profile scaling and output normalization.

# How harmonic roles produce direction

For actual harmonic partials, an exact register-sensitive coincidence satisfies $n f_A=m f_B$. Consequently,
\begin{equation}
\frac{f_B}{f_A}=\frac{n}{m}.
\label{eq:harmonic-ratio}
\end{equation}
Under the increasing labels in \eqref{eq:harmonic-profile}, a forward pair has $n<m$ and therefore a lower second fundamental in this exact-coincidence case. For example, the fundamental of a first tone can coincide with the second harmonic of a tone one octave below it. The forward label describes that ordered harmonic relationship.

Octave folding enlarges the coincidence condition to $n f_A=2^k m f_B$ for some integer $k$. The label comparison then leaves the octave displacement undetermined. For pseudo-partials, the declared role order directly replaces harmonic numbering. These cases explain why a directional label must be read together with the chosen profile and pitch comparison.

Explicit labels also permit undertone profiles. One implementation generates frequency $f/(i+1)$ with label $-i$, beginning at $i=0$. The same comparison rule applies to these signed labels, but its interpretation now depends on the declared undertone hierarchy. Relabelling that profile with increasing nonnegative list positions reverses its internal order and changes directional classifications.

# Aggregation, scale and information loss

The sum in \eqref{eq:triple} is the central construction. Two additional implementations operate on the same list of pair contributions.

The average divides every component by the number $N=|\widetilde A|\,|\widetilde B|$ of all component-pair opportunities, including pairs with zero weight. For $N>0$, this changes the raw scale while preserving signs and the normalized triple whenever $T>0$. An empty side gives $N=0$; the direct arithmetic average is undefined, and the unguarded implementation produces non-finite components. The sum rule instead returns a zero triple.

A power aggregation with exponent $r>0$ combines each directional bin as
\begin{equation}
F_r=\left(\sum_{\ell_u<\ell_v}w_{uv}^{r}\right)^{1/r},
\label{eq:power-merge}
\end{equation}
and analogously for $B_r,S_r$. It has no divisor by the number of contributions. Its exponent is distinct from the kernel exponent $q$. At $r=1$ it reduces to the sum. Other exponents change the relative influence of weak and strong coincidences.

Aggregation can even change the sign. For an illustrative contribution list with two forward weights of three and one backward weight of five, sum aggregation gives $D=6-5=1$. At $r=2$, direction is $\sqrt{18}-5<0$. This is an algebraic example of aggregation dependence, not a listening result or a claim about the default chord table. Uniform amplitude scaling still factors out of every component for positive $r$ and nonnegative weights, so normalization removes that common scale.

The older curve-based family normalizes its final triple. Its simpler discrete variant returns raw components. The later explicitly labelled family also returns raw components. One older supplied harmonic configuration uses thirteen partials with amplitudes $1/n$, kernel width $2/5$, kernel exponent one, polynomial exponent $27/10$ and aggregation exponent $11/10$. It is a different declared model from the later three-component sampled profile with binary coincidence and sum aggregation. Thresholds and raw scores do not transfer between them without accounting for these choices.

Direction itself is a lossy summary. Given $T>0$, write $m=\widehat F+\widehat B$. Then
\begin{equation}
\widehat F=\frac{m+\widehat D}{2},\quad
\widehat B=\frac{m-\widehat D}{2},\quad
\widehat S=1-m,\qquad |\widehat D|\leq m\leq1.
\label{eq:direction-freedom}
\end{equation}
Thus $\widehat D$ alone leaves a whole interval of triples. Even the full triple hides the detailed role matrix. Applications that need to distinguish opposed harmonic relationships should retain more than the net score.

# Chord progressions and directed cycles

Assign each allowed chord a vertex and each ordered comparison a directed edge labelled by its triple. A progression then selects a sequence of those edges. The construction permits a direction-based selection criterion once the profile, kernel, aggregation and scale are fixed; whether such a criterion produces useful music is an application question.

Even the elementary model admits a cycle with positive direction on every edge. Repeatedly transpose a single-note pitch class by five semitones:
\begin{equation}
0,5,10,3,8,1,6,11,4,9,2,7,0.
\label{eq:cycle}
\end{equation}
Each edge has the same triple $(0,0,84)$, so the sum of raw directions is $12\cdot84=1008$. If direction were the difference $V(B)-V(A)$ of a scalar value attached to each pitch class, its sum around a closed cycle would telescope to zero. Equation \eqref{eq:cycle} proves that no such scalar potential represents this relation on all pitch classes.

The relation can therefore describe consistently directed local transitions without supplying a global ranking of chords. A generative use also needs decisions about allowable transitions, repetition, phrase context, rhythm and ending conditions. Those decisions are additional musical structure, not determined by the triple.

# Relation to spectral distance and implied pitches

[Milne and Holland (2016)][milne-holland] model perceived triadic distance using weighted, smoothed harmonic pitch-class representations and their cosine distance, comparing it with Tonnetz and voice-leading distances. They explicitly discuss the relationship between this symmetric distance and musical asymmetry. Here, the pair weights are also symmetric, but comparing their component labels retains an ordered relation: reversal preserves $T$ and $S$, exchanges $B$ with $F$, and negates $D$. The role matrix in \eqref{eq:role-matrix} further records which components supplied the coincidence. This identifies the information carried by the present decomposition beyond its total overlap.

[Parncutt (2024)][parncutt] proposes a directional account in which subsidiary virtual pitches implied by one chord become sounded notes in the next. His C-major-to-F-major example involves F and A implied within the first chord and realized in the second. This is a direct conceptual comparison for \eqref{eq:cf-result}. The mechanisms assign direction differently: his account uses implied-pitch realization, while the present rule compares the labels of weighted component pairs. Computing the triple requires a declared profile and label order, without a separate inference of missing fundamentals. A common example supplies a point of comparison; it does not establish equivalence between the models or perceptual support for the label rule.

The contribution here is the explicit three-component decomposition, its exact constructions and its structural laws. Spectral distance and virtual-pitch implication provide comparison models for investigating its musical interpretation. Such comparisons must specify each model's inputs and distinguish judged similarity, expected continuation and heard direction; evidence for one response does not automatically establish the others.

# Questions made precise by the construction

**Which component roles carry a useful musical direction?** The model lets one vary the amplitudes while preserving offsets and labels, or vary labels while preserving coincident pitches. Those changes separate the influence of spectral weighting from that of role order. In the elementary model, changing the products $a_0a_1$, $a_0a_2$ and $a_1a_2$ changes the magnitudes attached to its six directed transitions. With multiple coincidences in chords it can also change their balance. A musical interpretation should specify which of these variations it expects to preserve.

**Does the direction contribute information about heard continuation?** For the worked profile, C major to F major and G major to C major have the same positive normalized direction, while their reversals have its negative. This gives exact comparison pairs for a proposed perceptual study. Timbre, voicing, loudness, duration, order, preceding context and listener familiarity must be declared, and any hypothesized association between the sign and a response must be stated before interpreting observations. The score alone supplies neither a response probability nor an effect size.

**What is lost by octave folding and by reduction to one number?** Circular comparison predicts invariance under octave displacement when the profiles translate and their weights remain fixed. Register-sensitive comparison need not do so. The self-comparison and \eqref{eq:direction-freedom} separately show that zero net direction can conceal supported opposing relationships. These are distinguishable mathematical constructions with concrete musical consequences to examine.

These questions follow from a fully specified descriptor. They do not depend on treating a software test as perceptual evidence. The elementary tables and structural statements here are algebraic results; perceptual associations remain questions for appropriate observations.

# Conclusion

Ordered component roles turn shared consonant material into a directed chord relation. The construction retains three components, admits a precise normalization and has an exact reversal law. Its central three-component realization gives every twelve-tone transition through a finite table, with chord results obtained by summing over ordered note pairs. C major to F major has components $(63,274,360)$ and normalized direction $297/697$ in the declared template scale.

The descriptor depends on its timbral profile, pitch comparison, kernel, aggregation and normalization. Explicit labels preserve role information across component reorderings, while different label assignments define different relations. Directed cycles show that local direction does not impose a global scalar ordering. Together these properties make the proposal reproducible and place its musical interpretation on a concrete foundation: a defined relation whose role in heard motion, continuation and composition can be investigated.

# Appendix: admissible inputs and correspondence

The mathematical nonnegative-weight model assumes finite nonnegative amplitudes, positive kernel width, positive kernel and aggregation exponents, finite pitches, symmetric distances and a kernel in the declared range. Implementation constructors do not uniformly enforce those conditions. One must check them when selecting a realization.

For example, a supplied additional curve is $R(x)=9136\sqrt{x}/[125(9x^4+64)]$. It exceeds one at $x=999/1000$: squaring the positive expression reduces this statement to an exact rational inequality. With kernel exponent one, \eqref{eq:kernel} then gives a negative local consonance weight below the cutoff. The probability and bounded-normalized-direction conclusions require the nonnegative domain and do not extend to this case. A curve choice must either satisfy that domain or be analysed as a different signed construction.

For a profile obtained by scaling a sampled template, its reference amplitude must be nonzero. For actual harmonic profiles, a finite partial count and an amplitude law must be supplied. A zero partial count yields empty component lists. For power aggregation, restricting the exponent to $r>0$ avoids powers of zero with nonpositive exponent. The average additionally requires a nonempty pair list.

The public note-list interfaces use integer pitches, and their pitch caches require nonnegative note indices. The mathematical formulas can be defined on a larger pitch domain; that extension is not an assertion that every legacy interface accepts it. Likewise, finite-precision implementations can change a comparison close to a cutoff, and large integer amplitude products in the simpler discrete implementation can overflow before conversion to real arithmetic. The worked integer weights are within its ordinary arithmetic range. Exact equalities and theorems in the article refer to the declared mathematical construction.

\Needspace{5\baselineskip}

In the positional-label family, a component's place in the generated partial list supplies its label. In the explicitly labelled family, labels travel with the components. The two agree only when these orders and the component data agree. Common transposition, sorting invariance and raw-scale comparisons must therefore be assessed with the actual profile and label convention specified.

Finally, all-pair coincidence counts allow the same component to contribute to several pairs. A capacity-limited matching of two spectra is a different construction. Voice-paired melodic displacement is another. The present descriptor is completely determined by the ordered, weighted component comparisons in \eqref{eq:triple}.

# References {-}

1. Sethares, W. A. (1993). Local consonance and the relationship between timbre and scale. *Journal of the Acoustical Society of America*, **94**(3), 1218–1228. [University of Wisconsin repository][sethares].
2. Harrison, P. M. C., and Pearce, M. T. (2020). Simultaneous consonance in music perception and composition. *Psychological Review*, **127**(2), 216–244. [doi:10.1037/rev0000169][harrison].
3. Milne, A. J., and Holland, S. (2016). Empirically testing Tonnetz, voice-leading, and spectral models of perceived triadic distance. *Journal of Mathematics and Music*, **10**(1), 59–85. [doi:10.1080/17459737.2016.1152517][milne-holland].
4. Parncutt, R. (2024). The origin of the dominant: Schoenberg's ‘strong progression’ and the realisation of implied virtual pitches. *Music Analysis*, **43**(2), 247–301. [doi:10.1111/musa.12233][parncutt].

[sethares]: https://minds.wisconsin.edu/handle/1793/9496
[harrison]: https://doi.org/10.1037/rev0000169
[milne-holland]: https://doi.org/10.1080/17459737.2016.1152517
[parncutt]: https://doi.org/10.1111/musa.12233
