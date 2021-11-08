---
title: 'ASGarD: Adaptive Sparse Grid Discretization'
tags:
  - C++
  - Cuda
  - fusion
  - plasma
  - sparse grid
  - high dimensional
  - discontinuous Galerkin
authors:
  - name: David L. Green
    orcid: 0000-0003-3107-1170
    affiliation: 1
  - name: Mark Cianciosa
    orcid: 0000-0001-6211-5311
    affiliation: 1
  - name: Ed D'Azevedo
    orcid: 0000-0002-6945-3206
    affiliation: 1
  - name: Wael Elwasif
    orcid: 0000-0003-0554-1036
    affiliation: 1
  - name: Steven E. Hahn
    orcid: 0000-0002-2018-7904
    affiliation: 1
  - name: Coleman J. Kendrick
    orcid: 0000-0001-8808-9844
    affiliation: 1
  - name: Hao Lau
    orcid: 0000-0000-0000-0000
    affiliation: 1
  - name: Graham Lopez
    orcid: 0000-0002-5375-2105
    affiliation: 1
  - name: Adam McDaniel
    orcid: 0000-0000-0000-0000
    affiliation: "1, 4"
  - name: Benjamin T. McDaniel
    orcid: 0000-0000-0000-0000
    affiliation: "1, 2"
  - name: Lin Mu
    orcid: 0000-0002-2669-2696
    affiliation: "1, 3"
  - name: Timothy Younkin
    orcid: 0000-0002-7471-6840
    affiliation: 1
affiliations:
 - name: Oak Ridge National Laboratory
   index: 1
 - name: University of Tennessee Knoxville
   index: 2
 - name: University of Georgia
   index: 3
 - name: South Doyle High School, Knoxville, TN
   index: 4
date: 28 October 2021
bibliography: paper.bib
---
# Summary

Many areas of science exhibit physical processes which are well described by high dimensional partial differential equations (PDEs), e.g., the 4D, 5D and 6D models describing magnetized fusion plasmas [@juno2018], or the ... models describing quantum mechanical interactions of several bodies (ref). In such problems, the so called "curse of dimensionality" whereby the number of degrees of freedom (or unknowns) required to be solved for scales as $N^D$ where $N$ is the number of grid points in any given dimension. A simple, albeit naive, 6D example is demonstrated in Fig.~\ref{fig:scaling} below where with $N=1000$ grid points in each dimension, the memory required just to store the solution vector, not to mention forming the matrix required to advance such a system in time, would exceed an exabyte. While there are methods to simulate such high-dimensional systems, they are mostly based on Monte-Carlo methods which rely on a statistical sampling such that the resulting solutions include noise. Since the noise in such methods can only be reduced at a rate proportional to $\sqrt{N_p}$ where $N_p$ is the number of Monte-Carlo samples, there is a need for continuum, or grid / mesh based methods for high-dimensional problems which both do not suffer from noise, but which additionally bypass the curse of dimenstionality. Here we present a simulation framework which provides such a method.

![(left) Illustration of the curse of dimensionality in the context of solving a 6 dimensional PDE (e.g., those at the heart of magnetically confined fusion plasma physics) on modern supercomputers, and how the memory required to store the solution vector (solid black curves) and the matrix (magenta curves) in both naive and Sparse Grid based discretizations as the resolution of the simulation domain is varied. Memory limits of the Titan and Summit supercomputers at Oak Ridge National Laboratories, in addition to an approximate value for an ExaScale supercomputer, are overlaid for context; (right) Potential memory savings of a Sparse Grid based solver represented as the ratio of the naive tensor product full-grid (FG) degrees of freedom (DoF) to the sparse-grid (SG) DoF. \label{fig:scaling}](figures/scaling-and-savings.png){width=100%}

The Adaptive Sparse Grid Discretization (ASGarD) code is a framework specifically targeted at solving high-dimensional PDEs using a combination of a Discontinuous-Galerkin Finite Element solver implemented atop an adaptive sparse grid basis. The adaptivity aspect allows for the sparsity of the basis to be adapted to the properties of the problem of interest, which facilitates retaining the advantages of sparse grids in cases where the standard sparse grid selection rule is not the best match.  

The implementation incorporates CPU and GPU, as well as single and multi-node parallelism in a performance portable manner by casting the computational kernels as linear algebra operations and relying on vendor provided BLAS libraries to give portability. Several test problems are provided, including advection up to 6D.   

# Acknowledgements

This research used resources of the Oak Ridge Leadership Computing Facility (OLCF) at the Oak Ridge National Laboratory, and the National Energy Research Scientific Computing Center (NERSC), which are supported by the Office of Science of the U.S. Department of Energy under Contract Numbers DE-AC05-00OR22725 and DE-AC02-05CH11231 respectively.

# References
