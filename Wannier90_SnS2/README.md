Wannier90_SnS<sub>2</sub>
=========================

Input files to calculate the electronic band structure and DoS of SnS<sub>2</sub> using the VASP Wannier90 interface and the PBE and HSE06 functionals and the *G*<sub>0</sub>*W*<sub>0</sub>, sc*GW*<sub>0</sub> and sc*GW* methods.

Running the example
-------------------

<em>**Note:** You will need to obtain the Sn_d and S PBE PAW pseudopotentials (`POTCAR` files) from the VASP database to run these calculations.</em>

1. Perform an ionic relaxation with the experimental lattice parameters using PBEsol with the DFT-D3 dispersion correction and fairly tight convergence criteria.

2. Perform an electronic-structure calculation with PBE:

  * Run VASP with the skeleton `wannier90.win` in the working directory; VASP will add the missing information and will generate several other input files needed by Wannier90.

  * Add the additional band-structure tags from `wannier90_band.win` and run Wannier90 with e.g. `wannier90.x wannier90` to calculate the maximally-localised Wannier functions (written to`wannier90.chk`) and the band structure. The result is saved into `wannier90_band.dat`, `wannier90_band.kpt`, `wannier90_band.gnu` for plotting.

  * Replace the band-structure tags with the `postw90.x` tags in `wannier90-dos.win` and run `postw90.x` with e.g. `mpirun -np 32 postw90.x wannier90` to calculate the DoS. The result is saved into `wannier90-dos.dat`.

3. Perform an electronic-structure calculation with HSE06. The complete calculation consists of three three parts:

  * First, perform an electronic-structure calculation with PBE to obtain converged GGA wavefunctions (this step can be skipped, but should save time).

  * Copy the `WAVECAR` file and use the GGA wavefunctions as an initial guess for an electronic-structure calculation with HSE06.

  * Copy the `WAVECAR` file and re-run VASP with `ALGO = None`, `NELMIN = 0`, `NPAR = <Default>` and `LWANNIER90 = .TRUE.` to generate Wannier90 input from the converged HSE06 wavefunctions (post-process as in #2).

4. Perform electronic-structure calculations with the *GW* routines. This calculation is again done in several separate steps:

  * First, again perform an electronic-structure calculation with PBE to obtain converged wavefunctions (this is identical to the first step in #3, and can again be skipped if desired).

  * Copy the `WAVECAR` and re-run VASP with `ALGO = Exact` and `LOPTICS = .TRUE.` to obtain accurate conduction states and a `WAVEDER` file.

  * For each of the *GW* calculations (a. *G*<sub>0</sub>*W*<sub>0</sub>, b. sc*GW*<sub>0</sub>, c. sc*GW*), copy the `WAVECAR` and `WAVEDER` files from the previous step, and run VASP to generate the Wannier90 input from the calculations (again, post-process as in #2).

Links
-----

- [http://www.slideshare.net/jmskelton/vasp-and-wannier90-a-quick-tutorial](http://www.slideshare.net/jmskelton/vasp-and-wannier90-a-quick-tutorial): A brief overview of using the Wannier90 interface with VASP.

- [http://wannier.org/user_guide.html](http://wannier.org/user_guide.html): Wannier90 user-guide pages with links to a PDF manual and tutorial.
