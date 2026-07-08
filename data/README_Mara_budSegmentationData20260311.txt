This csv file contains all of the data required for Mara's bud analyses project. The dataset contains 7 different strains, being:
    "YET918": "ΔSUN4",
    "YET563": "ΔSHE2",
    "YET572": "ΔSHE3",
    "YET915": "WT",
    "YET916": "ΔSSD1",
    "YET919": "ΔMPT5",
    "YET921": "ΔSEC72"

Every strain contain several replicates. Below we summarized the number of cells and cells containing buds per individual strain + replicate  combination:

          Cells per strains:
          strain  cells  buds bud_pct
       0  YET563   1655   265  16
       1  YET572   1945   320  16
       2  YET915   1894   439  23
       3  YET916   2175   443  20
       4  YET918   2439   489  20
       5  YET919   1349   292  22
       6  YET921   1069   158  15

          total    12526  2406 19

           Cell per strain + replicate combination:
           strain replicate  cells  buds bud_pct
       0   YET563       BR1    357    54  15
       1   YET563       BR2    270    56  21
       2   YET563       BR3   1028   155  15

       3   YET572       BR1    123    34  28
       4   YET572       BR2    284    33  12
       5   YET572       BR3    604    98  16
       6   YET572       BR4    540   110  20
       7   YET572       BR5    394    45  11

       8   YET915       BR1    209    42  20
       9   YET915       BR2    729   132  18
       10  YET915       BR3    444   117  26
       11  YET915       BR4    183    61  33
       12  YET915       BR5    329    87  26

       13  YET916       BR1    383   147  38
       14  YET916       BR2    228    79  35
       15  YET916       BR3    275   111  40
       16  YET916       BR4   1289   106   8

       17  YET918       BR1    576   138  24
       18  YET918       BR2   1027   126  12
       19  YET918       BR3    836   225  27

       20  YET919       BR1    418    94  22
       21  YET919       BR2    294    95  32
       22  YET919       BR3    637   103  16

       23  YET921       BR1    556   101  18
       24  YET921       BR2    108    16  14
       25  YET921       BR3     36    12  33
       26  YET921       BR4    369    29   8

                    total    12526  2406 19

Description of how the data was acquired:
For smFISH imaging, we used an Olympus BX63 epifluorescence microscope equipped with Ultrasonic stage and UPlanApo 100X 1.35NA oil-immersion objective (Olympus). 
Lumencore SOLA FISH light source, a Hamamatsu ORCA-Fusion sCMOS camera (pixel-size 6.5 µm x 6.5 µm) mounted using U-CMT C-Mount Adapter, and zero-pixel shift filter sets: 

F36-500 DAPI HC Brightline Bandpass Filter, 
AHF-LED-FISH-R (for CalFluor610),
F36-523 Cy5 HC BrightLine Filter
and a F36-542 Cy3 HC BrightLine Filter Set.
Images are acquired across 41 sections with a Z-step size of 0.2 μm. 
The software CellSens (Olympus) was used for instrument control and image acquisition.

Exposure time of 750 ms for the FISH channels was used. 20-50 ms exposure was used for the DAPI, depending on brightness of the DAPI signal.

Column explanations:
#########################################################################################################
######### General Cell Identifiers

1) image_cell_id
Pixel value of the label corresponding to the cell in the mask image DIC_corrected_masks.tif.

2) fov
Field-of-view identifier. For example, fov 03 refers to the third image taken for a given \
strain and replicate combination.

3) uid
Unique identifier constructed for each cell in the dataset using the following fields:

strain + "" + replicate + "" + image_cell_id + "_" + fov

Example: YET563_BR3_8_01

4) source_folder
Folder from which the dataset was generated.

5) strain
Strain identifier. Example: YET563

6) replicate
Biological replicate number. Example: BR1

7) mRNA
The mRNA species measured in the experiment. ASH1CLB2, SUN4, SRL1

8) condition
Gene deletion background of the strain:

YET918 → ΔSUN4
YET563 → ΔSHE2
YET572 → ΔSHE3
YET915 → WT
YET916 → ΔSSD1
YET919 → ΔMPT5
YET921 → ΔSEC72

9) condition + strain
Combined column containing both strain and condition for easier plotting.
#########################################################################################################




#########################################################################################################
######### Whole Cell Morphology (regionprops)

Morphological properties calculated for the entire cell using scikit-image regionprops.
For more info see https://scikit-image.org/docs/0.23.x/api/skimage.measure.html#skimage.measure.regionprops.

10) bbox-0, bbox-1, bbox-2, bbox-3
Bounding box coordinates of the cell.

11) area
Cell area in pixels.

12) eccentricity
Measure of how elongated the cell is (0 = circular, 1 = highly elongated).

13) axis_minor_length
Length of the minor axis of the fitted ellipse.

14) axis_major_length
Length of the major axis of the fitted ellipse.

15) orientation
Angle of the major axis relative to the horizontal axis.

16) perimeter
Perimeter length of the cell boundary.

17) solidity
Ratio of the cell area to the area of its convex hull.
#########################################################################################################
######### Bud Morphology (regionprops)
Same morphological properties as above, but calculated for the bud compartment only. 
for example area_bud, or eccentricity_bud
#########################################################################################################



#########################################################################################################
######### RNA Spot Detection (Whole Cell)

18) spots
Number of RNA spots detected per whole cell using the Big-FISH function detect_spots().
For more info see: https://big-fish.readthedocs.io/en/stable/detection/spots.html)

19) dense_regions
Number of dense RNA regions detected in the cell using bigfish.detection.decompose_dense().
For more info see: https://big-fish.readthedocs.io/en/stable/detection/dense.html.

20) decomposed_RNAs
Estimated number of RNAs contained within dense regions.

21) tx
Number of dense regions overlapping with a nuclear mask.

22) nascent_RNAs
Estimated number of nascent RNAs obtained from decomposition of transcription sites (tx).

23) total_RNAs
Total number of RNAs per cell calculated as:

24) spots + decomposed_RNAs − dense_regions

Dense regions are subtracted to avoid counting single spots twice.
#########################################################################################################




#########################################################################################################
######### RNA Measurements (Bud Compartment)

Same measurements as above but restricted to the bud.

25) spots_bud
Number of RNA spots detected in the bud.

26) dense_regions_bud
Number of dense RNA regions detected in the bud.

27) decomposed_RNAs_bud
Estimated RNAs within dense regions in the bud.

28) tx_bud
Dense regions overlapping the bud nuclear mask.

29) nascent_RNAs_bud
Estimated nascent RNAs in the bud.

30) total_RNAs_bud
Total RNAs in the bud.
#########################################################################################################




#########################################################################################################
######### RNA Measurements (Mother Cell Compartment)

31) spots_mother
Number of RNA spots detected in the mother cell.

32) total_RNAs_mother
Total number of RNAs in the mother cell compartment.
#########################################################################################################




#########################################################################################################
######### Nuclear Measurements (Mother Cell)

33) mother_nuclei_count
Number of distinct nuclear cell masks detected within the mother cell.

34) mother_nuclei_area
Total nuclear area in pixels within the mother cell.

35) mother_nuclei_mean_intensity
Mean intensity of the Z-projected DAPI image within the mother nuclear mask.
#########################################################################################################




#########################################################################################################
######### Nuclear Measurements (Bud)

36) nuclei_bud_count
Number of nuclear regions detected within the bud.

37) nuclei_bud_area
Nuclear area in pixels within the bud.

38) nuclei_bud_mean_intensity
Mean intensity of the Z-projected DAPI image within the bud nuclear mask.
#########################################################################################################