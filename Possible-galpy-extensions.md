Introduction
-------------

The following is a brief list of possible extensions that would be useful to implement. I am not directly working on any of these and am not planning on it, but if you want to add something along these lines to galpy, I would be happy to consult. To be accepted in the main repository through pull request all extensions should at the very least add documentation to the API and tests to the test suite. Please let the maintainer of the code know if you start working on one of these.

Some of these are simple and could be done quickly as part of learning how to work with galpy. Other would require more significant changes to the structure of galpy. The larger extensions are marked by !

Potentials
-----------

- [ ] Add new potentials (see [#232](https://github.com/jobovy/galpy/pull/232) or [#242](https://github.com/jobovy/galpy/pull/242) for example pull requests for new potentials): e.g.,
    - [x] A Tri-axial logarithmic potential
    - [ ] An Einasto density profile
    - [x] The perfect ellipsoid ([de Zeeuw 1985](http://adsabs.harvard.edu/abs/1985MNRAS.216..273D))
    - [ ] A triaxial Staeckel potential in a sensible way
    - [x] A radially exponential disk with a vertical sech profile, or with a general vertical profile (**done!** through DiskSCFPotential)
    - [ ] A power-law potential with flattening in the density (straightforward based on TwoPowerTriaxialPotential)
    - [ ] A power-law potential with an exponential cut-off and flattening in the density (bulge model in Binney & Tremaine 2008; straightforward based on TwoPowerTriaxialPotential)
    - [x] TwoPowerSphericalPotentials with flattening in the density (halo model in Binney & Tremaine 2008)
    - [x] Double exponential disk with a central hole (ISM model in Binney & Tremaine 2008) (**done!** in [jobovy/diskscf](https://github.com/jobovy/galpy/tree/diskscf))
    - [ ] The potential of a thin shell (for educational purposes)
    - [ ] The potential of a razor-thin ring (for educational purposes)
    - [ ] !The potential of a donut ring
    - [ ] Models 1 and 2 of Binney & Tremaine (2008) [requires the three potentials above)
    - [x] A three-dimensional spiral potential (**done** in [#305](https://github.com/jobovy/galpy/pull/305))
    - [ ] A three-dimensional bar potential: a Ferrers bar (done! in [smoh/ferrers](https://github.com/smoh/galpy/tree/ferrers), but only in Python so far)
    - [x] Basis function expansions, w/ a way to compute them for a given potential. For example, [Hernquist & Ostriker](http://adsabs.harvard.edu/abs/1992ApJ...386..375H) (**done!** in [SeaifanAladdin/SCF](https://github.com/SeaifanAladdin/galpy/tree/SCF))
    - [x] !Basis function expansions for the disk (see Binney & Tremaine); for axisymmetric potentials this could potentially be done using a modification of the method of Dehnen & Binney (1998): use approximate rho(R,z) = f(R) h(z) and solve Poisson equation for their Phi_ME using SCF. (**done!** in [jobovy/diskscf](https://github.com/jobovy/galpy/tree/diskscf))
    - [x] A three-Miyamoto-Nagai disk approximation to an exponential disk from [Smith et al. (2015)](http://arxiv.org/abs/1502.00627)
- [ ] Add adiabatically-contracted NFW potentials or add adiabatic contraction more generally
- [x] Wrapper that allows mass growth over time (**done!**, see cases of the new WrapperPotential classes)
- [ ] General mass/amplitude growth wrapper that uses a basis expansion of the 1D growth to support arbitrary growth histories
- [ ] !Add rotation, tumbling, and movement of center of potential more generally as a wrapper around other potentials
- [ ] !Add rotation, tumbling, and movement of center of potential more generally as a wrapper around other potentials in a sensible way in C
- [ ] Add general methods to return forces in rectangular coordinates (building them from the standard Rforce,zforce,phiforce).
- [ ] Add general methods to return forces in spherical coordinates (building them from the standard Rforce,zforce,phiforce).
- [ ] The zero-velocity curve for axisymmetric potentials.

Orbit integration and orbits
------------------------------

- [x] !Add support for dynamical friction (**done!** in [#346](https://github.com/jobovy/galpy/pull/346))
- [ ] !Add support for dynamical friction in C
- [ ] Integrate R(Z)Orbits in C without integrating phi [see [this issue](https://github.com/jobovy/galpy/issues/28)]
- [ ] !Better orbit integration: Add interpolation methods for integrators such that the step size can be larger than the requested output time step (right now, the step size is always smaller than the requested output step size, but for sufficiently smooth potentials, the step size can sometimes be increased with intermediate points found through interpolation; see NR).
- [ ] !Implement the integration of the phase-space volume (using Orbit.integrate_dxdv) for 3D orbits. This will require writing the integration routine that uses all of the relevant second derivatives of the potential, both in python and C, and implementing the necessary second derivatives for a large number of potentials (in python and C).
- [ ] Add the IAS15 symplectic integrator ([Rein & Spiegel 2015](http://adsabs.harvard.edu/abs/2015MNRAS.446.1424R)); cannot use the rebound version, as that is incompatible GPL'ed code.
- [ ] Add the Dormand-Prince 853 integrator.
- [ ] Allow orbits to be plotted in a rotating frame (i.e., write a wrapper that makes use of the general orbit plotting)
- [ ] Allow uncertainties to be provided at Orbit initialization and uncertainties on orbital parameters to be computed with Monte Carlo simulations
- [x] Allow an Orbit instance to be initialize using an astropy v3 SkyCoord (see [323](https://github.com/jobovy/galpy/issues/323))
- [ ] !Orbit factories: initialize many orbits at the same time from a list of initial conditions
- [ ] Orbit method that returns the guiding-star radius (simply using the ``Potential.rl`` function)
- [ ] Plot the epicycle approximation to an orbit
- [ ] !Animate the epicycle approximation to an orbit

Action-angle
-------------
- [ ] Add frequencies and angles for the adiabatic approximation:
     - [ ] in Python
     - [ ] in C
- [ ] Implement spherical actionAngle calculations in C in a similar way as actionAngleAdiabatic or actionAngleStaeckel.
- [x] Implement the transformation from actions and angles to configuration space for the isochrone potential (**done** in [aaisoinv](https://github.com/jobovy/galpy/tree/aaisoinv), but not merged)
- [ ] Implement the transformation from actions and angles to configuration space for spherical potentials (**underway**)
- [ ] Implement the triaxial Staeckel fudge ([Sanders & Binney 2015](http://adsabs.harvard.edu/abs/2014arXiv1412.2093S))
- [ ] Implement frequencies from Fourier analysis of integrated orbits (see [Binney & Spergel](http://adsabs.harvard.edu/abs/1982ApJ...252..308B), [Laskar](http://adsabs.harvard.edu/abs/1990Icar...88..266L), or [Valluri & Merritt](http://adsabs.harvard.edu/abs/1998ApJ...506..686V))
- [x] Implement actionAngleIsochroneApprox for triaxial potentials; requires to do the phi fit in actionsFreqsAngles as well.
- [x] !Basic interaction with Paul McMillan's TorusMapper code ([this github repository](https://github.com/PaulMcMillan-Astro/Torus))
- [ ] !Implement the torus machinery directly in a robust manner

Distribution functions
------------------------
- [ ] Implement simple spherical DFs:
  - [ ] The Hernquist DF
  - [ ] The isochrone DF
  - [ ] General Eddington inversion
- [ ] Implement action-based DFs for NFW halos
- [ ] Generalize diskdf to be able to use any potential [see [this issue](https://github.com/jobovy/galpy/issues/7)]
- [ ] Implement a particle-spray model for tidal streams (see, e.g., [Fardal et al.](http://adsabs.harvard.edu/abs/2015MNRAS.452..301F))
- [ ] Improvements in the DF for a tidal stream:
  - [ ] Perform actionAngle approximations as (x,v) -> (J,O,a) rather than (R,vR,...) -> (J,O,a) [see [this issue](https://github.com/jobovy/galpy/issues/113)]
  - [ ] Add error convolutions to callMarg [see [this issue](https://github.com/jobovy/galpy/issues/114)]
  - [ ] Look into including the Jacobian (l,b,...) -> (X,V) properly in lb callMarg [see [this issue](https://github.com/jobovy/galpy/issues/115)]
  - [ ] Use detdOdJp from nearest trackpoint when evaluating the DF, or interpolate between two nearest, as done in streamgapdf to compute the kicks due to a subhalo interaction [see [this issue](https://github.com/jobovy/galpy/issues/197)]

Miscellaneous
---------------
- [ ] !Add support for interacting with N-body codes like NEMO or Gadget. This includes
     - [x] Translate galpy potentials to external potentials that can be used with NEMO; **done!** (at least partially)
     - [ ] Use galpy to sample initial conditions (e.g., for a disk using quasiisothermaldf) and write commands/files to run these through N-body codes (with or without an external potential).
     - [x] Translate galpy potentials to external potentials that can be used with Gadget/Gizmo. Make a shared library that these codes can link to.
