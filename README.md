# Ion–Molecule Scattering: an Adaptive N-Body Solver from Scratch

Simulating the Coulomb scattering of an Ar⁺ ion off a flexible water molecule, and computing the
orientation-averaged deflection — built on a **hand-written adaptive Runge–Kutta integrator** and
**Gauss–Legendre quadrature**, with no black-box ODE or integration libraries.

Course project — NTU Computational Physics Final Project. All solver and integration code written from first principles.

![Sample scattering trajectory]
<Figure size 640x480 with 1 Axes><img width="428" height="396" alt="image" src="https://github.com/user-attachments/assets/dd2ca7c4-9c34-462f-9ac7-239994db79c5" />
  
## What this demonstrates

- **Adaptive RK4 from scratch** — a fourth-order Runge–Kutta stepper with an *embedded error estimate*
  (compare one full step against two half-steps) and automatic step-size control to a user tolerance.
- **Coupled N-body ODE system** — four interacting bodies (ion + O + 2×H). Coulomb forces between point
  charges plus harmonic bond and bond-angle springs for the molecule; rigid-body reorientation via
  Euler-angle rotation matrices.
- **High-dimensional numerical integration** — the observable (mean deflection angle) is averaged over a
  **5-D domain**: two impact-parameter coordinates × three Euler angles. Implemented with **composite
  Gauss–Legendre quadrature (orders 1–5)** and cross-checked against a rectangle rule.
- **Pure NumPy**, vectorised where practical; timed to show the cost of the 5-D sweep.

## Result

For the toy parameter set (reduced units), the rectangle-rule estimate of the orientation- and
impact-parameter-averaged deflection is **≈ 70.8°**. A single-trajectory run prints the exact deflection
for its initial condition and renders the 3-D trajectory.

## Scope & limitations

- Reduced/toy units; point-charge electrostatics and harmonic bonds — a physics **teaching model**, not a
  force field for real chemistry.
- The 5-D average is expensive; grids are deliberately coarse. The rectangle-rule value is the reference
  result reported above.
