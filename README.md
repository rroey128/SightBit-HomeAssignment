# Sky removal & re-annotate script
The following is a script that is used for sky removal and re-annotation of images that are of COCO dataset format. 
It consists of three main parts, each of those is editable and can be modified in order to adjust it's usage for different images or data-sets. 

<h2>The first part - extracting images (starting in the 6'th cell) :</h2>
in this particular script I filter out some images from COCO-dataset. The category keyword iv'e used ('airplane') can be changed and modified to the desired category. Alternatively, you can change the 6'th box in order to filter out images from any dataset you wish, but make sure to update the 'update_annotations' functions (16'th cell) to support the JSON format of your desired data-set. 
In addition, please make sure to update the paths all over the code to adjust these to the actual paths of your images.  

<h2>The second part - the actual script : </h2>
in the 24'th cell you can see the actual script. What it does basically is : 
Sky detection :
right after filtering out the relevant images from the data-sets, it detects the sky pixels in the image 
using detectron2's panoptic_fpn_R_101_3x Model for sky recognition. Then, it uses this model's inference results to mask the sky region with binary mask. After applying the mask, it locates the lowest pixel that is categorized as 'sky' and erases anything above that pixel. 
If you wish to use this script for something other than sky removal, you can do it by using a different model or detecting a different category other than sky using this specific model - all you need to do in order to achieve that is to edit the code in cell 24 and 19 to adjust it to the desired category (the relevant functions are 'get_stuff_class_id' and 'find_segment_id' if you only wish to replace the category).

Re-annotation : 
after the sky removal proccess, It uses detectron2's mask_rcnn_R_50_FPN_3x model for object recognition on the cropped image. It then edits the annotations in the provided JSON file according to model's inference results. By all means, the 'update_annotations' function in cell 16 can and maybe even SHOULD be edited in order to adjust it to work better with a specific JSON file such as the COCO format (using some specific libraries or frameworks) and enchances it's performance (as it is quite time consuming as it is right now). It can be as well updated to support other JSON formats, not only the COCO one. 

<h2>The third part - visualization : </h2>
I used pretty basic tools in order to draw and visualize the annotations on the images (mainly used the cv2 library). If you wish a different approach or a different style of visualization, you can edit or update anything below cell 26 (including this one). Please make sure to update the paths and folders in the relevant places in the code as well.


<h2> WARNING : </h2>
if you use this script on a different data-set that is not of COCO-format, make sure to update COCO specific functions such as 'extract_image_id_from_path' in cell 30 and 'update_annotations' in cell 16.






