# SaturnPoles
Repository for Cassini Saturn polar data from Fletcher et al., 2018

Fletcher et al. (2018) used data from Cassini's Composite Infrared Spectrometer (CIRS) to investigate the dynamics and composition of Saturn's polar atmosphere from 2004-2017.  This repository contains (i) the zonally-averaged CIRS spectra on a monthly grid and (ii) the interpolated temperature field in Saturn's polar regions over the entire time series.  All CIRS interferograms were curtailed so that they all had the same spectral resolution (15 cm-1), and both PRIME observations and RIDERs (where CIRS observed simultaneously with other Cassini instruments) were included in this analysis.

# Data
Cassini/CIRS spectra were extracted from v4.3.4 of the database via a series of vanilla queries, and then averaged onto a monthly time grid and a 2-degree resolution latitude grid (stepped every 1 degree).  These averages were used to generate individual spectral files for input to the NEMESIS optimal estimation retrieval algorithm.  These can be found in the spectra.tar.gz tarball with the following format:

#############################

FWHM LAT LON NGEOM

#############################

NPTS_FP3

NAV_FP3

LAT_FP3 LON_FP3 SOLAR_ANGLE_FP3 EMISSION_ANGLE_FP3 AZIMUTH_ANGLE_FP3 WEIGHT_FP3

SPECTRUM_FP3 = FLTARR(NPTS_FP3, 3) ; 3 columns are wavenumber (cm-1), spectral radiance (W/cm2/sr/cm-1); radiance error

#############################


NPTS_FP4

NAV_FP4

LAT_FP4 LON_FP4 SOLAR_ANGLE_FP4 EMISSION_ANGLE_FP4 AZIMUTH_ANGLE_FP4 WEIGHT_FP4

SPECTRUM_FP4 = FLTARR(NPTS_FP4, 3) ; 3 columns are wavenumber (cm-1), spectral radiance (W/cm2/sr/cm-1); radiance error

#############################

FWHM~15 cm-1 gives the spectral resolution of the data, NGEOM=2 because the two focal planes, FP3 (600-1100cm-1) and FP4 (1100-1400 cm-1), are treated seperately.  NAV and WEIGHT are both flags set equal to one.  Note that data are provided over wider spectral ranges, but are considered untrustworthy (due to low responsivity and aliasing effects) outside of the ranges quoted above.  The user should consult the CIRS user manual for the locations of known electrical interferences affecting these spectra.

Each file is a seperate spectrum, with the format YYMM_lat_???.spx, where YYMM provides the year and month for the particular average.  
