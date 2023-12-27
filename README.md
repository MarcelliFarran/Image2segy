%IMAGE2SEGY:  Converts a Raster to SEG-Y format. 


                        HELP LINES:

 This program needs SegyMAT in your "Matlab path"
 SegyMAT(C) 2001-2012 Thomas Mejer Hansen 
 Is Recommended to use the latest Segymat version.
 Download here:   http://segymat.sourceforge.net/
 If you will transform many files probably you would like 
 to edit your defaults in line 125 (aprox)


 RASTER IMAGE can be a BMP, JPEG or TIFF                                    
 If seismic profile has only positive or negative values as old
 high resolution seismics on analogic recorders then save the
 image as 8 BITS Gray-scale file. If profile is a Blue-white-Red 
 record then input file should be a RGB file
 For old multichannel wiggle profiles better if save as Gray scale
 image  Scanner resolutions between 150 and 200 dpi are enough. 
  --------------------------------------------------------------

Program will ask you to input a parameters file, an image file and a
output segy file. A navigation file is also created (.bna file)

PARAMETERS FILE FORMAT:
Create an ASCII file with comma separated values with this 6 columns
structure:

======   TEXT FILE FIRST LINE FORMAT  ============(Atention: Change This from version 2.40)

TLP,L,ML,REV,DSF,ZUTM 
values ranges: 32000max, 32000max, 0/1, 0/1, 1/3/5, 0-60 
where.....

TLP: Trace length in pixels (constant along the whole profile) 

L: LineNumber (integer) that will be used only in the binary header, in the
   text header you can use line names as CAB-001L-N. In the binary header 
   you can only put there 1 for this line name. 
   You can use 0 for all lines without problem. 
   The program will alk you for the real name of the lines.

ML: Marine or lan profile
0 -> Marine profile 
1 -> Land profile with datum over sea level ( see ** downward) 

REV= SegY Revision format
0  ->  Segy Revision 0
1* ->  Segy Revision 1  ( *recommeded)

DSF= 1,3 or 5  SegY numeric format 
1  ->  32 bits IBM floating point 
3* ->  16 bits IBM floating point ( *recomended)
5  ->  IEEE format

ZUTM zone UTM = integer (1-60 or 0)  this value will be writte in the ascci header 
if you prefer you can leb be cero, because is not use for any calculation.    

Exemple: 2880,22,0,1,3,31  
  a trace length of 2880 pixels for line 22, marine survey, stored in segy
  revision 1 and IBM format 16bits and coordinates from UTM zone # 31 
===========================================================================
and as lines as you like with this structure

px, py, X1, Y1, TD, TL
where...

px, py  are top first pixels position for any known (or not) position on the
   image profile.

X1, and Y1 are UTM position in meters for known positions. 
    Put zeros if unknown but you want use this position to correct distortion 
    in the image due to paper drift in the scanner device.  

** TD  For Marine profiles is the delay (positive) of the interval in ms  
  (positive values in byte 105 and 109 in the output SEGY).
   For Land profiles is the time over the datum (negative value in the 
   byte 105 and 0 in the byte 109).  

TL is the time interval or trace length in ms. For Land profiles the full
time including time over datum (see example included in the downloaded zip).
For any changes (speed, course, delay) in the profile or just to get better
   position control you can add a new line in the control file.
Lines with 0 in utm X and Y can be used to correct the paper drift in the
   scanner ( real world positions are interpolated).

Example files included in the downloaded ZIP file 

Example without zeros in positions:
2880,1,0,1,3,31
1,   22,555000,4500000,2400,1000
1143,22,557000,4502000,2200,1000
2000,22,558000,4503000,2200,1000
2701,22,559000,4504000,2200,1000

Example with zeros in positions to correct distortion in the image:
2880,22,0,1,3,31
1,   22,555000,4500000,2400,1000
1143,22,557000,4502000,2200,1000
2000,22,      0,     0,2200,1000
2701,22,559000,4504000,2200,1000

Land_example:
1141,000,1,1,3,30
61,42,500000,4500000,600,5600
1392,42,505000,4505000,600,5600


If you just wants to create a segy without navigation and scale of 1 second
press cancel when program ask you for the parameter file.
In this case these values will be used
 raws,1,0,1,3,31
 1,1,1,1,0,1000
 columns,1,1000,1000,0,1000
raws & Columns are the image dimensions. 


Program will displays a map to check possible errors in the input parameters.

 MAXIMUM SIZE tested for images in Gray scale is 140*10E6 pixels in a
 computer with 2G RAM and Windows vista
 Remember MATLAB is not the fast programming language. Be patient,
 profiles has been waiting for years to be digitized.


 Author: Marcel·lí Farran, ICM (CSIC) Barcelona,
 Program page: http://gma.icm.csic.es/ca/image2segy

