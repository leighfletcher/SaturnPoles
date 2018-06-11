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

FWHM~15 cm-1 gives the spectral resolution of the data, NGEOM=2 because the two focal planes, FP3 (600-1100cm-1) and FP4 (1100-1400 cm-1), are treated seperately.  NAV and WEIGHT are both flags set equal to one.  All latitudes are planetographic, all longitudes are System III West. Note that data are provided over wider spectral ranges, but are considered untrustworthy (due to low responsivity and aliasing effects) outside of the ranges quoted above.  The user should consult the CIRS user manual for the locations of known electrical interferences affecting these spectra.

Each file is a seperate spectrum, with the format YYMM_lat_???.spx, where YYMM provides the year and month for the particular average.  

# Reconstructed Temperatures
As described by Fletcher et al., 2018, the individual retrievals were used to generate a "reconstructed" temperature field, using tensioned splines to interpolate the temperatures with time.  These outputs are stored as two IDL 'save' files, one for the North Pole and one for the South Pole.  These contain the interpolated temperatures (FINALTEMP) as an NPROxNLATxNDAYS array, where NPRO=120 is the number of pressure levels (in atm) in the PRESS array; NLAT=31 is the number of latitudes in the NEWLAT array (planetographic); NDAYS=493 is the number of days (Julian date) in the NEWDAYS array.  Note that these are only provides for 0.08 mbar to 1.2 bar, and dates before and after the Cassini/CIRS time series have been set to zero to avoid the temptation to extrapolate to other dates.

# Reconstructed Ethane and Acetylene
Finally, vertical distributions of ethane and acetylene were scaled during the retrievals of temperature, and can be used to estimate the latitudinal and temporal changes in these hydrocarbons at a single pressure level.  In the "polarcomp.sav" file, we provide estimates of the 1-mbar abundance of each species in ppmv as a function of latitude and time:
C2H2_NORTH      FLOAT     = Array[493, 31]
C2H2_SOUTH      FLOAT     = Array[493, 31]
C2H6_NORTH      FLOAT     = Array[493, 31]
C2H6_SOUTH      FLOAT     = Array[493, 31]
NEWDAYS         FLOAT     = Array[493]
NEWLAT          FLOAT     = Array[31]




