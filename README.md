 In this notebook, I implement object detection using the very
 powerful YOLO model. Many of the ideas in this notebook are described in
 the two YOLO papers: Redmon et al., 2016 and Redmon and Farhadi, 2016.

##This model can:

- Detect objects in a car detection dataset
- Implement non-max suppression to increase accuracy
- Implement intersection over union
- Handle bounding boxes, a type of image annotation popular in deep learning

###YOLO

"You Only Look Once" (YOLO) is a popular algorithm because it achieves
high accuracy while also being able to run in real time.
This algorithm "only looks once" at the image in the sense that it
requires only one forward propagation pass through the network to make
predictions. After non-max suppression, it then outputs recognized objects
together with the bounding boxes.

###Model Details

##Inputs and outputs

The input is a batch of images, and each image has the shape (m, 608, 608, 3)

The output is a list of bounding boxes along with the recognized classes.
Each bounding box is represented by 6 numbers  (𝑝𝑐,𝑏𝑥,𝑏𝑦,𝑏ℎ,𝑏𝑤,𝑐).


##Anchor Boxes

Anchor boxes are chosen by exploring the training data to choose reasonable
height/width ratios that represent the different classes. For this exercise,
5 anchor boxes were chosen (to cover the 80 classes), and stored in the
file 'yolo_anchors.txt'

The dimension of the encoding tensor of the second to last dimension based
on the anchor boxes is  (𝑚,𝑛𝐻,𝑛𝑊,𝑎𝑛𝑐ℎ𝑜𝑟𝑠,𝑐𝑙𝑎𝑠𝑠𝑒𝑠).

The YOLO architecture is:
IMAGE (m, 608, 608, 3) -> DEEP CNN -> ENCODING (m, 19, 19, 5, 85).

##Non-Max suppression

Get rid of boxes with a low score. Meaning, the box is not very confident
about detecting a class, either due to the low probability of any object,
or low probability of this particular class.
Select only one box when several boxes overlap with each other and detect
the same object.

##Defining Classes, Anchors and Image Shape

The information on the 80 classes and 5 boxes is gathered in two
files: "coco_classes.txt" and "yolo_anchors.txt".

The car detection dataset has 720x1280 images, which are pre-processed
into 608x608 images.

## images
The repo does not include images, but if you'd like to try the model just need to upload your pictures into 'images' directory and the program will push the pictures into the 'out' directory.
The model able to predict the following classes:
person
bicycle
car
motorbike
bus
train
truck
boat
traffic light
fire hydrant
stop sign
parking meter
