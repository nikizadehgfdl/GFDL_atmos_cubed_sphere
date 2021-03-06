# RELEASE NOTES for FV3 202101: Summary

FV3-202101-public --- 22 January 2021
Lucas Harris, GFDL <lucas.harris@noaa.gov>

This version has been tested against the current SHiELD (formerly fvGFS) physics
and with FMS release candidate 2020.04 from https://github.com/NOAA-GFDL/FMS

This release includes the following:

- Positive-definite advection scheme
- In-line GFDL Microphysics
- Fast-timescale Rayleigh damping
- Updated namelist documentation
- Implemented multiple same-level and telescoping nests for the global system (from J Mouallem)
- Updated coarse-graining capabilities (from S Clark)
- Re-organized fv_diagnostics, moving the revised fv_diag_column functionality and the declaration of diagnostic IDs to separate files
- and other updates and general cleanup

This version of FV3 is described as component of SHiELD in Harris et al. (2020, JAMES).

## Interface changes in 202101

drivers: renamed 'fvGFS' directory to SHiELD

atmosphere.F90: if using the in-line GFDL microphysics the precipitation rates (available in the structure Atm%inline_mp for rain, ice, snow, and graupel separately) must be passed into the physics and/or land model as appropriate. Here we demonstrate how to do this in SHiELD by copying them into IPD_Data(nb)%Statein%prep (and so on), which are newly defined in the IPD_Data structure within the SHiELD physics.

# RELEASE NOTES for FV3 201912: Summary

FV3-201912-public --- 10 January 2020
Lucas Harris, GFDL <lucas.harris@noaa.gov>

This version has been tested against the current SHiELD (formerly fvGFS) physics
and with FMS release candidate 2020.02 from https://github.com/NOAA-GFDL/FMS

Includes all of the features of the GFDL Release to EMC, as well as:

- Updated 2017 GFDL Microphysics (from S-J Lin and L Zhou included in GFSv15)
- Updates for GFSv15 ICs (from T Black/J Abeles, EMC)
- Updates to support new nesting capabilities in FMS (from Z Liang)
- Re-written grid nesting code for efficiency and parallelization
- Re-organized fv_eta for improved vertical level selection
- 2018 Stand-alone regional capabilities (from T Black/J Abeles, EMC)
- Refactored model front-end (fv_control, fv_restart)
- Support for point soundings
- And other updates

## Interface changes

drivers: renamed 'fvGFS' directory to SHiELD

atmosphere.F90: 'mytile' is renamed 'mygrid'

The non-functional gfdl_cloud_microphys.F90 has been removed and replaced with the 2017 public release given to EMC. Also added a proper initialization routine, that includes the use of INTERNAL_FILE_NML and thereby requires the input_nml_file argument. If you do not define the compiler flag INTERNAL_FILE_NML then you can delete this argument.

The namelist nggps_diag_nml has been eliminated. 'fdiag' is no longer handled by the dynamical core, and should be handled by the physics driver.

For a complete technical description see the NOAA Technical Memorandum OAR GFDL: https://repository.library.noaa.gov/view/noaa/23432
