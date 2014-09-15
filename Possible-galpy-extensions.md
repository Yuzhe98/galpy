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