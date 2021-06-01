# MUSIC Algorithm:
<div class="text-gray-dark mb-2">
  .text-gray-dark on white

Multiple SIgnal Classification

MUSIC method assumes that a signal vector, <img src="https://render.githubusercontent.com/render/math?math=x">, consists of {\displaystyle p}p complex exponentials, whose frequencies {\displaystyle \omega }\omega  are unknown, in the presence of Gaussian white noise, {\displaystyle \mathbf {n} }\mathbf {n} , as given by the linear model

{\displaystyle \mathbf {x} =\mathbf {A} \mathbf {s} +\mathbf {n} ,}{\displaystyle \mathbf {x} =\mathbf {A} \mathbf {s} +\mathbf {n} ,}
where {\displaystyle \mathbf {A} =[\mathbf {a} (\omega _{1}),\cdots ,\mathbf {a} (\omega _{p})]}{\displaystyle \mathbf {A} =[\mathbf {a} (\omega _{1}),\cdots ,\mathbf {a} (\omega _{p})]} is an {\displaystyle M\times p}{\displaystyle M\times p} Vandermonde matrix of steering vectors {\displaystyle \mathbf {a} (\omega )=[1,e^{j\omega },e^{j2\omega },\ldots ,e^{j(M-1)\omega }]^{T}}{\displaystyle \mathbf {a} (\omega )=[1,e^{j\omega },e^{j2\omega },\ldots ,e^{j(M-1)\omega }]^{T}} and {\displaystyle \mathbf {s} =[s_{1},\ldots ,s_{p}]^{T}}{\displaystyle \mathbf {s} =[s_{1},\ldots ,s_{p}]^{T}} is the amplitude vector. The {\displaystyle M\times M}M\times M autocorrelation matrix of {\displaystyle \mathbf {x} }\mathbf {x}  is then given by

{\displaystyle \mathbf {R} _{x}=\mathbf {A} \mathbf {R} _{s}\mathbf {A} ^{H}+\sigma ^{2}\mathbf {I} ,}{\displaystyle \mathbf {R} _{x}=\mathbf {A} \mathbf {R} _{s}\mathbf {A} ^{H}+\sigma ^{2}\mathbf {I} ,}
where {\displaystyle \sigma ^{2}}\sigma ^{2} is the noise variance and {\displaystyle \mathbf {R} _{s}}{\displaystyle \mathbf {R} _{s}} is the autocorrelation of {\displaystyle \mathbf {s} }\mathbf {s} .

The autocorrelation matrix {\displaystyle \mathbf {R} _{x}}\mathbf {R} _{x} is traditionally estimated using sample correlation matrix

{\displaystyle {\widehat {\mathbf {R} }}_{x}={\frac {1}{N}}\mathbf {X} \mathbf {X} ^{H}}{\displaystyle {\widehat {\mathbf {R} }}_{x}={\frac {1}{N}}\mathbf {X} \mathbf {X} ^{H}}
where {\displaystyle N}N is the number of vector observations and {\displaystyle \mathbf {X} =[\mathbf {x} _{1},\mathbf {x} _{2},\ldots ,\mathbf {x} _{N}]}{\displaystyle \mathbf {X} =[\mathbf {x} _{1},\mathbf {x} _{2},\ldots ,\mathbf {x} _{N}]}. Given the estimate of {\displaystyle \mathbf {R} _{x}}\mathbf {R} _{x}, MUSIC estimates the frequency content of the signal or autocorrelation matrix using an eigenspace method.

Since {\displaystyle \mathbf {R} _{x}}\mathbf {R} _{x} is a Hermitian matrix, all of its {\displaystyle M}M eigenvectors {\displaystyle \{\mathbf {v} _{1},\mathbf {v} _{2},\ldots ,\mathbf {v} _{M}\}}{\displaystyle \{\mathbf {v} _{1},\mathbf {v} _{2},\ldots ,\mathbf {v} _{M}\}} are orthogonal to each other. If the eigenvalues of {\displaystyle \mathbf {R} _{x}}\mathbf {R} _{x} are sorted in decreasing order, the eigenvectors {\displaystyle \{\mathbf {v} _{1},\ldots ,\mathbf {v} _{p}\}}{\displaystyle \{\mathbf {v} _{1},\ldots ,\mathbf {v} _{p}\}} corresponding to the {\displaystyle p}p largest eigenvalues (i.e. directions of largest variability) span the signal subspace {\displaystyle {\mathcal {U}}_{S}}{\displaystyle {\mathcal {U}}_{S}}. The remaining {\displaystyle M-p}M-p eigenvectors correspond to eigenvalue equal to {\displaystyle \sigma ^{2}}\sigma ^{2} and span the noise subspace {\displaystyle {\mathcal {U}}_{N}}{\displaystyle {\mathcal {U}}_{N}}, which is orthogonal to the signal subspace, {\displaystyle {\mathcal {U}}_{S}\perp {\mathcal {U}}_{N}}{\displaystyle {\mathcal {U}}_{S}\perp {\mathcal {U}}_{N}}.

Note that for {\displaystyle M=p+1}M=p+1, MUSIC is identical to Pisarenko harmonic decomposition. The general idea behind MUSIC method is to use all the eigenvectors that span the noise subspace to improve the performance of the Pisarenko estimator.

Since any signal vector {\displaystyle \mathbf {e} }\mathbf {e}  that resides in the signal subspace {\displaystyle \mathbf {e} \in {\mathcal {U}}_{S}}{\displaystyle \mathbf {e} \in {\mathcal {U}}_{S}} must be orthogonal to the noise subspace, {\displaystyle \mathbf {e} \perp {\mathcal {U}}_{N}}{\displaystyle \mathbf {e} \perp {\mathcal {U}}_{N}}, it must be that {\displaystyle \mathbf {e} \perp \mathbf {v} _{i}}{\displaystyle \mathbf {e} \perp \mathbf {v} _{i}} for all the eigenvectors {\displaystyle \{\mathbf {v} _{i}\}_{i=p+1}^{M}}{\displaystyle \{\mathbf {v} _{i}\}_{i=p+1}^{M}} that spans the noise subspace. In order to measure the degree of orthogonality of {\displaystyle \mathbf {e} }\mathbf {e}  with respect to all the {\displaystyle \mathbf {v} _{i}\in {\mathcal {U}}_{N}}{\displaystyle \mathbf {v} _{i}\in {\mathcal {U}}_{N}}, the MUSIC algorithm defines a squared norm

{\displaystyle d^{2}=\|\mathbf {U} _{N}^{H}\mathbf {e} \|^{2}=\mathbf {e} ^{H}\mathbf {U} _{N}\mathbf {U} _{N}^{H}\mathbf {e} =\sum _{i=p+1}^{M}|\mathbf {e} ^{H}\mathbf {v} _{i}|^{2}}{\displaystyle d^{2}=\|\mathbf {U} _{N}^{H}\mathbf {e} \|^{2}=\mathbf {e} ^{H}\mathbf {U} _{N}\mathbf {U} _{N}^{H}\mathbf {e} =\sum _{i=p+1}^{M}|\mathbf {e} ^{H}\mathbf {v} _{i}|^{2}}
where the matrix {\displaystyle \mathbf {U} _{N}=[\mathbf {v} _{p+1},\ldots ,\mathbf {v} _{M}]}{\displaystyle \mathbf {U} _{N}=[\mathbf {v} _{p+1},\ldots ,\mathbf {v} _{M}]} is the matrix of eigenvectors that span the noise subspace {\displaystyle {\mathcal {U}}_{N}}{\displaystyle {\mathcal {U}}_{N}}. If {\displaystyle \mathbf {e} \in {\mathcal {U}}_{S}}{\displaystyle \mathbf {e} \in {\mathcal {U}}_{S}}, then {\displaystyle d^{2}=0}d^2 = 0 as implied by the orthogonality condition. Taking a reciprocal of the squared norm expression creates sharp peaks at the signal frequencies. The frequency estimation function for MUSIC (or the pseudo-spectrum) is

{\displaystyle {\hat {P}}_{MU}(e^{j\omega })={\frac {1}{\mathbf {e} ^{H}\mathbf {U} _{N}\mathbf {U} _{N}^{H}\mathbf {e} }}={\frac {1}{\sum _{i=p+1}^{M}|\mathbf {e} ^{H}\mathbf {v} _{i}|^{2}}},}{\displaystyle {\hat {P}}_{MU}(e^{j\omega })={\frac {1}{\mathbf {e} ^{H}\mathbf {U} _{N}\mathbf {U} _{N}^{H}\mathbf {e} }}={\frac {1}{\sum _{i=p+1}^{M}|\mathbf {e} ^{H}\mathbf {v} _{i}|^{2}}},}
where {\displaystyle \mathbf {v} _{i}}\mathbf {v} _{i} are the noise eigenvectors and

{\displaystyle \mathbf {e} ={\begin{bmatrix}1&e^{j\omega }&e^{j2\omega }&\cdots &e^{j(M-1)\omega }\end{bmatrix}}^{T}}{\displaystyle \mathbf {e} ={\begin{bmatrix}1&e^{j\omega }&e^{j2\omega }&\cdots &e^{j(M-1)\omega }\end{bmatrix}}^{T}}
is the candidate steering vector. The locations of the {\displaystyle p}p largest peaks of the estimation function give the frequency estimates for the {\displaystyle p}p signal components

{\displaystyle {\hat {\omega }}=\arg \max _{\omega }\;{\hat {P}}_{MU}(e^{j\omega }).}{\displaystyle {\hat {\omega }}=\arg \max _{\omega }\;{\hat {P}}_{MU}(e^{j\omega }).}
MUSIC is a generalization of Pisarenko's method, and it reduces to Pisarenko's method when {\displaystyle M=p+1}{\displaystyle M=p+1}. In Pisarenko's method, only a single eigenvector is used to form the denominator; and the eigenvector is interpreted as a set of autoregressive coefficients, whose zeros can be found analytically or with polynomial root finding algorithms. In contrast, MUSIC assumes that several such functions have been added together, so zeros may not be present. Instead there are local minima, which can be located by computationally searching the estimation function for peaks.
</div>
in this code you have some data (test) and you can estimate direction of arrival of singals with MUSIC algorithm.
I believe there is enough comments in the code to understand it.

