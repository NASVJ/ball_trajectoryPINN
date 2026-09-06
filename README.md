# ball_trajectoryPINN
practice  pinn codes
it's a learning project inspired by an existing idea
 Refered the original PINN paper by Raissi et al , This project was inspired by a PINN tutorial and code snippet from
[Vizuara Labs](https://vizuaranewsletter.com/p/teach-your-neural-network-to-...)
 but my curve is overfitting covering even noisy data points 
 would like to implement different parameters ,diferent planet and see and learn how Pinn works 

 
## Debugging Journey: Physics Loss on Sparse vs Dense Points

Initially, the physics (ODE) loss was computed only at the same
sparse, noisy data points used for the data loss. This meant the
network had no physics constraint between those points, so it
learned to follow the noise instead of the true underlying parabola.

**Before fix** — PINN prediction bends toward noisy points:
## Debugging Journey: Physics Loss on Sparse vs Dense Points

Initially, the physics (ODE) loss was computed only at the same
sparse, noisy data points used for the data loss. This meant the
network had no physics constraint *between* those points, so it
learned to follow the noise instead of the true underlying parabola.

**Before fix** — PINN prediction bends toward noisy points:
 Pinn curve before fix.png

**Fix:** Added a dense set of 200 "collocation" points spanning the
full time domain, and enforced the ODE residual loss there instead —
forcing the network to respect the physics equation  at all places, not
just at the 10 noisy measurements.

**After fix** — PINN prediction smoothly tracks the true parabola:
after fix ballTrajectPINNcurve.png

