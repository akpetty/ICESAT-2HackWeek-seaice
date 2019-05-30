# ICESAT-2HackWeek-seaice
ICESat-2 hack week repository for those in the sea ice team


* Look at https://nsidc.org/data/atl07 AND ADD INFO ON THE VARIABLES ETC!!
* Get the ATL10 files for Nov 15th (coincident with ATL03/07)

* Add some stuff on the filename convention (e.g. Fernando's notebook)
* provide some more info on the variables of interest.
* Explore the ssh_flag and quality flags. Highlight issues of cloud filtering etc. 
* Analyze the various beams! Show the consistency between strong and weak etc.
* Do a freeboard derivation! Show how we go from ATL07 to ATL10. 
* Maybe work backwards from the included data to derive elevation using ATL03 and the various ancillary products (geoid, tides, atmospheric corrections etc).
* Do some large scale processing reading in a load of ATL07 files.


## Background

ICESat-2 carries onboard a single instrument – the Advanced Topographic Laser Altimeter System, or ATLAS. Like the altimeter on the first ICESat mission, ATLAS measures the travel times of laser pulses to calculate the distance between the spacecraft and Earth’s surface. 

![icesat2_profiling](icesat2_profiling.png?raw=true "ICESat-2 profiling the sea ice surface, figure taken from the ATL07/10 ATBD document")

ICESat-2 employs a photon counting (PC) system to obtain better measurement sensitivity with lower resource (power) demands on the satellite platform compared to the original ICESat mission. A high repetition rate, low pulse energy laser at 532 nm and sensitive detectors are used to provide the round-trip time of individual photons scattered from the surface. The ATLAS instrument transmits laser pulses at 10 kHz and at the ICESat-2 nominal orbit altitude of ~500 km, the laser footprints (~17 m) are separated by ~0.7 m along ground tracks. Six across track beams (three pairs of strong and weak beams) provide profiles of the ice surface, and for ice sheets the multiple beams address the need for unambiguous separation of ice sheet slope from height changes. For sea ice, this provides multiple profiles of sea ice and sea surface heights for improved freeboard and thickness retrievals. The beam configuration and their separation are shown below: the beams within each pair have different transmit energies (‘weak’ and‘strong’, with an energy ratio between them of approximately 1:4) and are separated by 90 m in the across-track direction. The beam pairs are separated by ~3.3 km in the across-track direction, and the strong and weak beams are separated by ~2.5 km in the along-track direction. The ICESat-2 products of most interest to the sea ice community are:

* ATL03: Along-track photon cloud elevations  
* ATL07: Along-track segment heights (this notebook!!)   
* ATL09: Cloud productrs (used here mainly for cloud filtering)
* ATL10: Along-track freeboards (see other Notebook!)
* ATL20: Gridded freeboard
* Unofficial sea ice thickness products through NASA GSFC (along-track and gridded)

  

## ATL03 (photon heights)


The primary input data from ATL03 are photons heights, background rates, and corrections applied to the height estimates. The standard height estimates include a number of corrections applied to the height estimates (see below). ATL03 applies multiple geophysical corrections to provide corrected heights for all the downlinked photons. By design, each of these corrections can easily be removed by the end user from the ATL03 data products if desired. By default, they are applied to generate a best estimate of the photon height. 

Additional corrections that some users may decide to apply are provided with the product. Also, a number of meteorological parameters (e.g., wind, surface air temperature, sea level pressure, etc.) from reanalysis products are available in ATL03.

Photon cloud parameters:
• Background rate at 400 Hz (which includes solar background and dark count rates)
• The height of the column used in the background calculation
(bckgrd_int_height_reduced)

### ATL09 (clouds)



## ATL07 (sea surface/sea ice heights)

Arguably ATL07 is the most important IS2 product for sea ice users. ATL07 provides along-track surface height and type (e.g. snow-covered ice, open water) for the ice-covered seas of the northern and southern hemispheres. Sea surface and sea ice height are estimated for segments along each of the six beams. Surface height estimates are referenced to the mean sea surface (MSS). Segment length varies with surface type as it is determined by the distance over which ~150 signal photons are accumulated (expect segments length around 50 m, as each shot gives us back a few photons and the shots have an along-track reoslution of 70 cm). 

Two files are provided per day, one each for the north and south, which contain the sixteen intra-day orbits broken out by hemisphere. 


Summarize the following flow-charts??


![Coarse_surface_finding](Coarse_surface_finding.png?raw=true "Coarse_surface_finding, figure taken from the ATL07/10 ATBD document")

Provide a brief overview of this two-step filtering

![Fine_surface_finding](Fine_surface_finding.png?raw=true "Fine_surface_finding, figure taken from the ATL07/10 ATBD document")

Provide a brief overview of this classification scheme

![Surface classification](Surface_classification.png?raw=true "Surface classification, figure taken from the ATL07/10 ATBD document")


![swath_segment](swath_segment.png?raw=true "ICESat-2 swath_segment, figure taken from the ATL07/10 ATBD document")


### Things to consider when using ATL07
* First photon bias (Is this a variable in the ATL07 file???)
* Subsurface-scattering corrections (not included)


A first-photon bias estimate is provided from system engineering with each height estimate. The expected biases are defined in the Cal-19 (an ICESat-2 document). 

The subsurface-scattering, or volume scattering, bias comes from photons that experience multiple scattering within the snow or ice before returning to the satellite. 



<!-- As mentioned earlier, at low photon rates an insignificant fraction of input events occur
during the dead time from a previous event, so the output event rate from the receiver is
linear with the input photon rate (the counting efficiency). As the input rate increases, a
larger fraction occurs during the dead time, and the behavior becomes less linear. There
are 16/4 detectors for the returns from the strong/weak beams to reduce the dead time
effect on the observed photon distribution. Figure 9 illustrates the FPB for different
return pulse width and events/shot. It can be seen that at the nominal return rates of 6/1.5 
photon/pulse (strong/weak beams) for snow covered sea ice, the corrections are ~1-3 cm.
It should also be noted that these corrections will use the average dead time for the active
channels for each ground track. -->



<!-- Ice absorbs
green light only weakly, with attenuation lengths of tens of meters or more, but ice grains
in snow and bubbles in ice both scatter green light strongly [Warren et al., 2006]. While
most photons exit the surface of a snow pack within a fraction of a nanosecond, some are
delayed significantly, potentially producing a long tail on the histogram of return times.
Averaging returns times of photons from this tail with photons from the surface return
leads to a mean delay in the photon return time, and a downward bias in the apparent
surface height. This error and its temporal variability is expected to be small for finegrained snow surfaces, but it may be more significant in coastal areas where there are
large seasonal variations in the surface grain size.
The magnitude of the subsurface-scattering bias delay depends in part on the scattering
density of the snow and its bulk absorbance, both of which are determined by the density
and grain and/or bubble size close to the surface. Since neither of these properties are
known at the time of ATLAS processing, each must be determined independently using
external information about the snow, such as meteorological model output or infrared
reflectance data. -->


## ATL10 (sea ice freeboards)

## Gridded freebaords (ATL20) and sea ice thickness (NASA GSFC research product)



# Repo setup


Run the following from the terminal to get the data you need in your repo..
cp Data
aws s3 cp s3://pangeo-data-upload-oregon/icesat2/ATL07-01_20181115003141_07240101_001_01.h5 .

aws s3 cp s3://pangeo-data-upload-oregon/icesat2/ATL03_20181115022655_07250104_001_01.h5 .

To upload the data 

aws s3 cp ATL03_20181115022655_07250104_001_01.h5 s3://pangeo-data-upload-oregon/icesat2/
aws s3 cp ATL07-01_20181115003141_07240101_001_01.h5 s3://pangeo-data-upload-oregon/icesat2/