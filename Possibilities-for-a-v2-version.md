## Potential framework

* **Break down specific potentials to their purest implementation, use wrappers for *any* modification**. For example,
  * Log potential would just be phi(r) = vc^2 ln r, flattening in z (and/or y) can be done by wrapper that deforms potentials
  * Barred potentials only implement static, major-axis = x-axis form, pattern rotation and position angle from SolidBodyRotationWrapper
  * No potentials would have their own growth, all would be done by wrappers like DehnenSmoothWrapperPotential
* _Comments_:
  * Need to check performance: C wrappers at this point appear to be almost as fast as direct implementations, Python wrappers are more expensive (but for speed, use C)
  * This does not allow for analytic speed-ups from simplifications of expressions
  * What about things like the density? Can then only be computed using the Poisson equation
* **Allow potentials to be implemented in their own natural coordinate system, all other forces derived automatically**. For example,
  * Spherical potential: only implement phi(r), d phi / d r
  * Some potentials have simple d phi / d x etc. derivatives, implement as such.
* _Comments_:
  * Nothing really holding back from doing this in v1.x series, so can be started now.
* **Allow derivatives to be computed symbolically with some symbolic algebra package**. Currently, all derivatives (forces and second) have to be implemented by hand, would be nice to be able to just implement the potential and directly get access to all derivatives (and can then still implement derivatives by hand for potential speed-ups). 
* _Comments_:
  * Again nothing really holding back from starting this in v1.x series, because it does not _have_ to break things (but might)
  * Would ultimately be most useful if it could be combined with automatic compilation of C extension
* **Simplify names of general potential routines, e.g., ``evaluateRforces`` --> ``Rforce``.** 

## Orbit framework

* **Use a single orbit class**, rather than current ``FullOrbit``, ``RZOrbit``, etc. Can use similar approach to subclassing as for ``WrapperPotential``/``planarWrapperPotential``?
* **More clearly distinguish between an orbit that has not been integrated yet and one that has?**