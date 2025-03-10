# Description

The tool elaborates the percentage of land covered by tree canopy within a custom radial buffer around each city address. The address is considered to be passing the criterion if the percentage of tree canopy cover equals or exceeds 30%.


# Input data requirements

* City addresses, vector dataset with point geometry
* Tree canopy cover, raster map
* Model parameters:
   * spatial reference system of the tree canopy cover map
   * optional threshold to apply to the values of the tree canopy cover map
   * pixel resolution (X and Y) of the tree canopy cover map
   * radius in meters of the buffer to apply around city addresses locations (default 500 meters) 


# Output data requirements

* Input dataset "City addresses" dataset with the addition of the following fields:
   * "percentuale_copertura": the percentage of land covered by tree canopy within the radial buffer
   * "is_30": the boolean flag, true if the percentage of tree canopy cover equals or exceeds 30%


# Objective

The purpose is to support decision makers by identifying the addresses where the criterion is met and the ones where it is not met, and by what amount.


# Use of resource

* Applies the optional threshold to the values of the tree canopy cover map, generating a binary map
* Projects the addresses dataset into the projected reference system of the binary canopy cover map
* Bufferizes the point location of addresses with the custom radius
* Determines the area of the buffer (in the common projected reference system)
* Counts the number N of canopy pixels within each buffer and derives the cumulative area A:
  A = N * pixel_X_resolution * pixel_Y_resolution
* Computes the percentage of tree canopy cover and determines if the criterion is passed of not
* Joins the newly determined fields with the original dataset of addresses


# Constraints
None: input data are commonly available. 
Tree canopy map is commonly available as high-vegetation map with low accuracy from satellite images. If a more accurate dataset is available, for example from an aerial survey, the results improve.
