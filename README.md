# Welcome to the code repository for the Tongji SIGS W20 A{AI} studio.
On this page you can find code that will allow you to explore 2D neural style transfer. This editing techniques must be run on graphics processing units (GPUs) in order to run or train efficiently and in a reasonable time frame. Thus, this repository is designed to run on Paperspace, which is a cloud computing platform that allows you to access GPUs.

# Tongji SIGS W20 A{AI} AI Model

## Content
1. [2D Neural Style Transfer](#neuralstyle)

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

Command Format for running:

`bash run_2Dneuralstyletransfer_nomask.sh CONTENT_FILE STYLE_FILE OUTPUT_DIR IMAGE_SIZE CONTENT_WEIGHT STYLE_WEIGHT NUM_ITERS`

Command Example for running: 

`bash run_2Dneuralstyletransfer_nomask.sh /storage/2Dmodels/robotics_building_satellite.png /storage/2Dmodels/new000343.png /artifacts 500 5.0 1.0 100`
