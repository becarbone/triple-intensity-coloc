This macro pulls elements of the Dendrite Analysis repository (which was initially developed by Lai Ding + modified for our use), but is primarily my construction. 

It is designed to take dendrites and assess them with respect to "pre" "post" and "protein of interest (POI)" channels. They don't inherently have to be actually pre and post synaptic markers, but for situations where you'd like to look at two markers with respect to a third, the two would be the pre/post and the third would be the POI. 

This macro requires: the dendrite ROI's in RGB compressed format within subfolders by treatment condition (ctrl, exp1, exp2, etc...), the chosen threshold for each of the three channels, the denotation of which color should be associated with which marker (pre/post/POI), and the percentage (in non-decimal format) for the amount of overlap required for two adjacent puncta to be considered overlapping. 

below is a simple illustration of approximately what is meant by 25% overlap. The o's indicate the punctum that is filled at least 25% by the other punctum (noted by x's), and so from the perspective of the o's punctum this is colocalized, but from the perspective of the x's punctum, it's not. 

ooooooo 
 o    o
 o xxxoxxxx
oooooooxxxxxx
   xxxxxxxxxx
      xxxxx
        xxx

This macro puts out: a bunch of spreadsheets (the method for exporting them w/ the imagej macro language is not 100% compatible with current spreadsheet programs, so if a box asks about having the right file, just hit yes and it'll open)
  -POITripleintensity.xls -> contains the intensity of the area within the ROI used in triple colocalization. The pattern is looking at the ROI of either the pre or post channel, determining if the ROI set used overlaps at least 25% with the other channel ROI (pre or post), and then determining which of the overlapping puncta are associated at least 25% with the POI ROI. The ROI that are successfully marked as positive for all gates are then assessed for intensity. 
  -PostPreIntensity.xls -> this is the intensity within the Post channel ROI that have been determined to have at least 25% overlap w/ the Pre ROI on the Pre channel image and then on the Post channel image. 
  -PrePostIntensity.xls -> this is the same thing as ^ this, but for the Pre channel ROI
  -Summary.xls -> contains (sorted by condition) the single puncta count, the double colocalized puncta count, and the triple colocalized puncta count as well as the calculated ratio colocalized of the total ROI screened. (if it's using Pre ROI, the PrePostPOI ratio will show how many of the Pre ROI passed the colocalization test with the Post and then the POI compared to the initial number of Pre ROI).
  -tripleColoc_areas.xls -> not working yet, supposed to show the areas of overlap for the space that is triple colocalized
  -tripleColoc_masks.xls -> has a side by side comparison of the total number of Pre/Post colocalized puncta that met the 25% criterion with the POI ROI (count) and all of the Pre/Post puncta that overlapped at all w/ the POI ROI regardless of meeting that criteron (total).
