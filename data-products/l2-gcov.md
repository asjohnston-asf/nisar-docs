# Geocoded Polarimetric Covariance

## Product Overview

The GCOV product is an L2 product derived from the L1 Range Doppler Single Look Complex (RSLC) product, providing terrain-corrected polarimetric covariance projected onto a predefined UTM or polar stereographic projection system grid. RSLC radar samples, organized as a polarimetric scattering vector, are cross-correlated with the scattering vector’s conjugate transpose, originating the polarimetric covariance matrix expressed in the same grid as the RSLC range-Doppler grid. 

The magnitude of the resulting polarimetric covariance terms is strongly affected by the topography, with areas facing the sensor becoming brighter and areas away from the sensor turning darker in the images, biasing covariance measurements. To reduce the effect of the topography, an area-based radiometric terrain correction (RTC) is applied over the covariance terms, normalizing the backscatter coefficient beta0 to gamma0. The normalized covariance terms are then geocoded onto the output grid using area-based adaptive multi-looking. 

```{figure} /assets/nisar-gcov.png
:label: covariance
:alt: Covariance polarimetric matrix elements
:width: 400px
:align: left

Covariance polarimetric matrix elements
```

Since the polarimetric covariance matrix is Hermitian, only the upper triangular covariance terms are provided. The diagonal terms of the polarimetric covariance matrix (highlighted in darker gray) are real-valued (HHHH, HVHV, VHVH, and VVVV, or RHRH and RVRV), representing the radar backscatter associated with each polarimetric channel. The off-diagonal terms of the polarimetric covariance matrix (highlighted in lighter gray) are complex-valued (HHHV, HHVH, HHVV, HVVH, and VHVV, or RHRV) and may or may not be present depending on the GCOV processing mode.

## Finding Data

{button}`Find in Vertex<https://search.asf.alaska.edu/#/?dataset=NISAR&sciProducts=GCOV>`

{button}`Find in Earthdata Search<https://search.earthdata.nasa.gov/search?q=nisar_l2_gcov_&ac=true>`

## Product Specification

{button}`Product Specification<https://nisar.asf.earthdatacloud.nasa.gov/NISAR-SAMPLE-DATA/DOCS/NISAR_D-102274_RevE_NASA_SDS_Product_Specification_L2_GCOV_Nov8_2024_w-sigs.pdf>`

## Data Layers

A GCOV data product includes the following raster data sets. For more information, see section 4.3 of the [product specification](#product-specification).

### Geocoded Polarimetric Covariance Terms
```
/science/LSAR/GCOV/grids/frequency[A|B]/HHHH
/science/LSAR/GCOV/grids/frequency[A|B]/HVHV
/science/LSAR/GCOV/grids/frequency[A|B]/HHHV
/science/LSAR/GCOV/grids/frequency[A|B]/HHVH
/science/LSAR/GCOV/grids/frequency[A|B]/HHVV
/science/LSAR/GCOV/grids/frequency[A|B]/HVVH
/science/LSAR/GCOV/grids/frequency[A|B]/HVVV
/science/LSAR/GCOV/grids/frequency[A|B]/VVVV
/science/LSAR/GCOV/grids/frequency[A|B]/VHVH
/science/LSAR/GCOV/grids/frequency[A|B]/VHVV
/science/LSAR/GCOV/grids/frequency[A|B]/RHRH
/science/LSAR/GCOV/grids/frequency[A|B]/RVRV
/science/LSAR/GCOV/grids/frequency[A|B]/RHRV
```

The primary data elements of the GCOV product are the images of the geocoded polarimetric covariance terms.

The diagonal terms (HHHH, HVHV, VVVV, VHVH, RHRH, RVRV) are real-valued and represent the radar backscatter.

The remaining terms (HHHV, HHVH, HHVV, HVVH, HVVV, VHVV, RHRV) are complex valued and relate to the electrical and geometric properties of the observed surface.

Which frequencies and polarizations are available in a particular GCOV data product will vary based on the acquisition mode of the satellite used to collect the data.

For more information on NISAR polarimetry, see [TODO](https://science.nasa.gov/mission/nisar/polarimetry/)

### Number of Looks

`/science/LSAR/GCOV/grids/frequency[A|B]/numberOfLooks`

The GCOV terms are obtained from the geocoding of the RSLC product polarimetric covariance terms using an adaptive area-based multi-looking algorithm. The multi-looking window and number of averaged looks vary with the topography and radar geometry. The number of looks layer provides the number of looks used for computing each GCOV term sample. 

### Mask

`/science/LSAR/GCOV/grids/frequency[A|B]/mask`

The mask layer provides information about the averaging ensemble of radar samples that originated the GCOV terms through adaptive multi-looking.

### Radiometric Terrain Correction Gamma-to-Sigma Factor

`/science/LSAR/GCOV/grids/frequency[A|B]/rtcGammaToSigmaFactor`

The RTC Gamma-to-Sigma factor provides factors to normalize the backscatter normalization convention of the GCOV matrix from gamma0 to sigma0.

## Naming Convention

NISAR GCOV product names will conform to the following naming convention:

{term}`NISAR`\_{term}`I`{term}`L`\_{term}`PT`\_{term}`PROD`\_{term}`CYL`\_{term}`REL`\_{term}`P`\_{term}`FRM`\_{term}`MODE`\_{term}`POLE`\_{term}`S`\_{term}`StartDateTime`\_{term}`EndDateTime`\_{term}`CRID`\_{term}`A`\_{term}`C`\_{term}`LOC`\_{term}`CTR`.{term}`EXT`

:::{glossary}
NISAR
: 5 char for mission: NISAR

I
: 1 char for Instrument: L for L-SAR, S for S-SAR

L
: 1 char for Level: 1 or 2 or 3

PT
: 2 char for Processing Type:
    - PR: Production
    - UR: Urgent Response
    - OD: Science On-Demand

PROD
: 4 chars for Product Identifier: GCOV

CYL
: 3 chars for CycLe number in the mission, each cycle represents 12 days, zero padded, starting at 001.

REL
: 3 chars for RELative orbit track number within a cycle, resets to 1 with a cycle number increment, zero padded.Valid values: 001-173.

P
: 1 char for direction of movement of the satellite at the time of imaging
    - A for Ascending
    - D for Descending

FRM
: 3 chars for track frame number, a segment of an orbital track corresponding to theproduct, zero padded Valid Values: 001-176 on each track.

MODE
: 4 chars for Bandwidth Mode Code of Primary and Secondary Bands:
    - 40, 20, 77, 05, or 00 (only if the secondary band is missing)

POLE
: 4 chars for Polarization of the data for the primary and secondary bands. Each band uses a two character code among the following:
    - SH = HH – Single Polarity (H transmit and receive)
    - SV = VV – Single Polarity (V transmit and receive)
    - DH = HH/HV – Dual Polarity (H transmit)
    - DV = VV/VH – Dual Polarity (V transmit)
    - CL= LH/LV – Compact Polarity (Left transmit)
    - CR = RH/RV – Compact Polarity (Right transmit)
    - QP = HH/HV/VV/VH – Quad Polarity
    - NA if band does not exist
    For example, a “quasi-quad” polarization mode would be noted DHDV while a “quasidual” polarization mode would be noted SHSV.

S
: 1 char for source of data for the product
    - A = Acquired source of the observation, single mode
    - M = Mixed source of observations, mixed mode

StartDateTime
: 15 chars for Radar Start Time of the data processed as zero Doppler contained in the file as YYYYMMDDTHHMMSS, UTC

EndDateTime
: 15 chars for Radar End Time of the data processed as zero Doppler contained in the file as YYYYMMDDTHHMMSS, UTC

CRID
: 6 chars for Composite Release Identifier
    - Format of EPMMmm.

A
: 1 char for Product Accuracy or Fidelity of the Orbit Ephermis and Radar Pointing:
    - P, M, N, or F.

C
: 1 char as Coverage Indicator: F for Full or P for Partial.

LOC
: 1 char to represent the location of the Science Data System. J for JPL,vrecommends N for NRSC.

CTR
: 3 chars for Product Counter (zero padded).

EXT
: 1 to n chars for Extension: h5, met, log
:::
