Wannier90_Si
============

Input files to calculate an electronic band structure for Si using the VASP Wannier90 interface and the HSE06 hybrid functional.

Running the example
-------------------

<em>**Note:** You will need to obtain a PBE PAW pseudopotential (`POTCAR` file) for Si from the VASP database to run these calculations. You can also use an LDA potential and set `GGA = PE` in the `INCAR` files.</em>

1. Calculate the wavefunctions at the PBE (GGA) level.

2. Copy the `WAVECAR` file from the first step, and recalculate the wavefunctions using the HSE06.

3. This part involves three separate steps:

  * Copy the `WAVECAR` file from the second step, and re-run VASP with `LWANNIER90 = .TRUE.`; VASP will generate several files needed by Wannier90, and will add missing information to the `wannier90.win` file.

  * Run Wannier90 with e.g. `wannier90.x wannier90` to calculate the maximally-localised Wannier functions (written to the checkpoint file `wannier90.chk`).
  
  * Uncomment the band-structure tags in `wannier90.win` and re-run Wannier90; the band structure data will be written to `wannier90_band.dat` and `wannier90_band.kpt`, along with scripts for Gnuplot and Grace (`wannier90_band.gnu`, `wannier90_band.agr`).

Links
-----

- [http://www.slideshare.net/jmskelton/vasp-and-wannier90-a-quick-tutorial](http://www.slideshare.net/jmskelton/vasp-and-wannier90-a-quick-tutorial) *A brief overview of using the Wannier90 interface with VASP.*

- [http://cms.mpi.univie.ac.at/wiki/index.php/Si_bandstructure](http://cms.mpi.univie.ac.at/wiki/index.php/Si_bandstructure) *VASP Wiki page on calculating the Si band structure using various approaches, including via the Wannier90 interface.*

- [http://wannier.org/user_guide.html](http://wannier.org/user_guide.html) *Wannier90 user-guide pages with links to a PDF manual and tutorial.*
