# Welcome to the code repository for the ACADIA2020_DeepDesign workshop.
On this page you can find code that will allow you to explore 2D neural style transfer and 2D-3D neural style transfer. These editing techniques must be run on graphics processing units (GPUs) in order to run or train efficiently and in a reasonable time frame. Thus, this repository is designed to run on Paperspace, which is a cloud computing platform that allows you to access GPUs.

# ACADIA 2020 Deep Design Models

## Content
[2D Neural Style Transfer](#neuralstyle)
[2D to 3D Style Transfer](#3dstyle)


<a name="neuralstyle"></a>
## Neural Style Transfer
Neural style transfer is an optimization technique used to take two images—a content image and a style reference image (such as an artwork by a famous painter)—and blend them together so the output image looks like the content image, but “painted” in the style of the style reference image.
This is implemented by optimizing the output image to match the content statistics of the content image and the style statistics of the style reference image. These statistics are extracted from the images using a convolutional network.
You can run this code with no mask, which means that the style will be transferred to the entire content image, or with a mask, which will apply the style to only the locations in the content image specified by the mask. Currently, the mask is a binary mask the same size as the content image, where a pixel value of 1 indicates a region to transfer style to and 0 indicates where the content image will be unaffected by the style transfer. 

### Running 2D style transfer
First, you will need to create notebook via web GUI, upload vgg weights, called `imagenet-vgg-verydeep-19.mat`, to `/storage`
You will also need to upload a content image and style guide image, and if desired the mask image, to `/storage`. You can download the vgg weights from <http://www.vlfeat.org/matconvnet/models/imagenet-vgg-verydeep-19.mat>.

2D style transfer Docker container image:

`acarlson32/neuralstyle-tf:firstimage`

Workspace:

`https://github.com/alexacarlson/DeepDesign2019.git`

Command Format for running with no mask:

`bash run_2Dneuralstyletransfer_nomask.sh CONTENT_FILE STYLE_FILE OUTPUT_DIR IMAGE_SIZE CONTENT_WEIGHT STYLE_WEIGHT NUM_ITERS`

Command Example for running with no mask: 

`bash run_2Dneuralstyletransfer_nomask.sh /storage/2Dmodels/robotics_building_satellite.png /storage/2Dmodels/new000343.png /artifacts 500 5.0 1.0 100`


Command Format for running with mask:

`bash run_2Dneuralstyletransfer_withmask.sh CONTENT_FILE STYLE_FILE MASK_FILE OUTPUT_DIR IMAGE_SIZE CONTENT_WEIGHT STYLE_WEIGHT NUM_ITERS`

Command Example  for running with mask: 

`bash run_2Dneuralstyletransfer_withmask.sh /storage/2Dmodels/robotics_building_satellite.png /storage/2Dmodels/new000343.png /storage/2Dmodels/new000343_mask.png /artifacts/styleoutputdir 500 5.0 1.0 100`


<a name="3dstyle"></a>
### Running 2D to 3D neural renderer for 2D to 3D style transfer
This project uses the neural 3D mesh renderer (CVPR 2018) by H. Kato, Y. Ushiku, and T. Harada to achieve dreaming and style transfer in 3D. It builds upon the code in (https://github.com/hiroharu-kato/neural_renderer.git)

Note that before running any jobs in this project, you will need to upload the desired 3D models (in `.obj` format) to the paperspace `/storage` space. Add each 3D model to `/storage/3Dmodels` and any 2D models (i.e., images) to `/storage/2Dmodels`. You do not need to worry about uploading pretrained weights, the code handles this under the hood. 

Neural Renderer Docker container image:

`acarlson32/2d3d_neuralrenderer:secondimage`

Workspace:

`https://github.com/alexacarlson/DeepDesign2019.git`

Command Format:

`bash run_2Dto3Dstyletransfer.sh INPUT_OBJ_PATH INPUT_2D_PATH OUTPUT_FILENAME OUTPUT_DIR STYLE_WEIGHT CONTENT_WEIGHT NUM_ITERS`

Command Example: 

`bash run_2Dto3Dstyletransfer.sh /storage/3Dmodels/TreeCartoon1_OBJ.obj /storage/2Dmodels/new000524.png 2Dgeo_3Dtree.gif /artifacts/results_2D_to_3D_styletransfer 1.0 2e9 1000`

