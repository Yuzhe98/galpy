The following is a brief list of possible extensions that would be useful to implement. I am not directly working on any of these and am not planning on it, but if you want to add something along these lines to galpy, I would be happy to consult. To be accepted in the main repository through pull request all extensions should at the very least add documentation to the API and tests to the test suite.

Some of these are simple and could be done quickly as part of learning how to work with galpy. Other would require more significant changes to the structure of galpy. The larger extensions are marked by *

- [ ] Add new potentials: e.g.,
    - [ ] A Tri-axial logarithmic potential
    - [ ] An Einasto density profile
    - [ ] A radially exponential disk with a vertical sech profile, or with a general vertical profile
    - [ ] A power-law potential with flattening in the density
    - [ ] A power-law potential with an exponential cut-off and flattening in the density (bulge model in Binney & Tremaine 2008)
    - [ ] TwoPowerSphericalPotentials with flattening in the density (halo model in Binney & Tremaine 2008)
    - [ ] Double exponential disk with a central hole (ISM model in Binney & Tremaine 2008)
    - [ ] Models 1 and 2 of Binney & Tremaine (2008) [requires the three potentials above)
- [ ] Add adiabatically-contracted NFW potentials or add adiabatic contraction more generally
- [ ] *Add support for dynamical friction (note: there is an old branch where this was started that could serve as a starting point)
- [ ] *Better orbit integration: Add interpolation methods for integrators such that the step size can be larger than the requested output time step (right now, the step size is always smaller than the requested output step size, but for sufficiently smooth potentials, the step size can sometimes be increased with intermediate points found through interpolation; see NR).
- [ ] Implement simple spherical DFs (these will only be merged into the main repository if deemed useful; i.e., if you have used it in a paper).
- [ ] Add frequencies and angles for the adiabatic approximation:
     - [ ] in Python
     - [ ] in C
- [ ] Implement spherical actionAngle calculations in C in a similar way as actionAngleAdiabatic or actionAngleStaeckel.
- [ ] *Implement the integration of the phase-space volume (using Orbit.integrate_dxdv) for 3D orbits. This will require writing the integration routine that uses all of the relevant second derivatives of the potential, both in python and C, and implementing the necessary second deritvatives for a large number of potentials (in python and C).
- [ ] *Add support for interacting with N-body codes like NEMO or Gadget. This includes
     - [ ] Translate galpy potentials to external potentials that can be used with these codes;
     - [ ] Use galpy to sample initial conditions (e.g., for a disk using quasiisothermaldf) and write commands/files to run these through N-body codes (with or without an external potential).
