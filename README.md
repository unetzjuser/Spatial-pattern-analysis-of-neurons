# Spatial pattern analysis of neurons
Use R spatstat package to analyze the spatial distribution pattern of neurons

----
# Software:
1. Install R (or RStudio). See https://cran.r-project.org

2. Install the spatstat package and dependencies. For further information, see https://spatstat.org

3. Install ImageJ/Fiji (optional). See https://imagej.net/Fiji

# Data:

The X and Y coordinates of neuronal points as well as the vertices of the region of interest (ROI). This information can be obtained, for example, using ImageJ/Fiji.

-----
# R codes:
***Run R and load the spatstat package***

library(spatstat)

***Input the X and Y coordinates of points***

x <- scan()

*#Paste the X coordinates of neurons here, separated by space.*

y <- scan()

*#Paste the Y coordinates of neurons here, separated by space.*

***Input the X and Y coordinates of the polygon ROI (e.g., the dentate gyrus)***

*#Note: In R, the coordinates of ROI vertices are in principle traversed anticlockwise. However, we determine ROI vertex coordinates in a clockwise manner in ImageJ/Fiji, and the ROI will be plotted upside down in R. In case that one direction does not work, just try the other way. This can be facilitated, for example, by sorting data in Excel.*

p<- ppp(x, y, poly = list(x = c(#paste the X coordinates of ROI vertices, separated by comma), y = c(#paste the Y coordinates of ROI vertices, separated by comma)))

***Define unit length (optional)***

unitname(p)<-list("unit","unit", #length_of_unit)

***Summarize results (optional)***

*#Note: cell density (referred to as “average intensity”) is presented as the number of points per square unit (not unit length) here, which needs calibration (e.g., to number of points per square millimeter). Alternatively, analyze cell density using ImageJ/Fiji or commercial software.*

summary(p)
 
***Plot ROI and neuronal points***

*#Note: for more plotting options, see the book "Spatial Point Patterns: Methodology and Applications with R" by Baddeley et al.*

plot(p)

***Set working directory***

setwd("type_pathname")
 
***Run nearest neighbor distance analysis and save the data as a .csv file***

*#Note: the distances calculated here are shown and saved in non-calibrated units and thus need to be calculated to unit length (e.g., millimeter).*

nndist(p)

write.table(nndist(p),"Name_of_the_file.csv",sep=",")

-----
# References:

1. Baddeley, A. & Turner, R. Spatstat: an R package for analyzing spatial point patterns. J. Statist. Software 12, 1-42 (2005).

2. Baddeley, A., Rubak, E. & Turner, R. Spatial point patterns: methodology and applications with R (CRC Press, Boca Raton, 2015).
