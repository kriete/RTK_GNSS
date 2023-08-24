# Excerpt from RTKLIB manual for rnx2rtkp

## SYNOPSIS

```rnx2rtkp [option ...] file file [...]```
 
## DESCRIPTION
Read  RINEX  OBS/NAV/GNAV/HNAV/CLK,  SP3,  SBAS  message  log  files  and  compute  receiver  (rover) positions and output position solutions.

The  first  RINEX  OBS  file  shall  contain  receiver  (rover)  observations.  For  the  relative  mode,  the  second RINEX  OBS  file  shall  contain  reference  (base  station)  receiver  observations.  At  least  one  RINEX NAV/GNAV/HNAV file shall be included in input files. To use SP3 precise ephemeris, specify the path in the  files.  The  extension  of  the  SP3  file  shall  be .sp3   or  .eph .  All  of  the  input  file  paths  can  include wild‐cards ( * ). To avoid command line deployment of wild‐cards, use ʺ...ʺ for paths with wild‐cards.

Command line options are as follows ([]:default). With ‐k option, the processing options are input from the configuration  file.  In  this  case,  command  line  options  precede  options  in  the  configuration  file.  For  the configuration file, refer B.4. 
 
OPTIONS
```
-? print help
-k file input options from configuration file [off]
-o file set output file [stdout]
-ts ds ts start day/time (ds=y/m/d ts=h:m:s) [obs start time]
-te de te end day/time
(de=y/m/d te=h:m:s) [obs end time]
-ti tint time interval (sec) [all]
-p mode mode (0:single,1:dgps,2:kinematic,3:static,4:moving-base,
5:fixed,6:ppp-kinematic,7:ppp-static) [2]
-m mask elevation mask angle (deg) [15]
-f freq number of frequencies for relative mode (1:L1,2:L1+L2,3:L1+L2+L5) [2]
-v thres validation threshold for integer ambiguity (0.0:no AR) [3.0]
-b backward solutions [off]
-c forward/backward combined solutions [off]
-i instantaneous integer ambiguity resolution [off]
-h fix and hold for integer ambiguity resolution [off]
-e output x/y/z-ecef position [latitude/longitude/height]
-a output e/n/u-baseline [latitude/longitude/height]
-n output NMEA-0183 GGA sentence [off]
-g output latitude/longitude in the form of ddd mm ss.ss [ddd.ddd]
-t output time in the form of yyyy/mm/dd hh:mm:ss.ss [sssss.ss]
-u output time in utc [gpst]
-d col number of decimals in time [3]
-s sep field separator [' ']
-r x y z reference (base) receiver ecef pos (m) [average of single pos]
-l lat lon hgt reference (base) receiver latitude/longitude/height (deg/m)
-y level output solution status (0:off,1:states,2:residuals) [0]
-x level debug trace level (0:off) [0]
```

## EXAMPLES
Example 1. Kinematic Positioning, L1+L2, output Latitude/Longitude/Height to STDOUT. 
```
rnx2rtkp 07590920.05o 30400920.05o 30400920.05n
```

Example 2. Single Point Positioning, El Mask=15deg, output NMEA GGA to file out.pos 
```
rnx2rtkp -p 0 -m 15 -n -o out.pos 07590920.05o 30400920.05n
```

Example 3. Static Positioning, L1, time form yyyy/mm/dd hh:mm:ss, output X/Y/Z‐ECEF positions 
```
rnx2rtkp -p 3 -f 1 -t -e 07590920.05o 30400920.05o 30400920.05n
```

Example 4. Kinematic Positioning, Instantaneous AR, validation threshold=2, comma separator 
```
rnx2rtkp -i -v 2 -s , 07590920.05o 30400920.05o 30400920.05n
```