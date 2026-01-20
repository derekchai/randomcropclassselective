# Random Crop Class Selective

This is a simple custom Albumentations transform which acts as a random crop
while trying to ensure that specific classes will be preserved in the crop
post-transformation. 

This may be useful if it is desired to create augmentations of rare classes, to
ensure that these rare classes will actually be present in the augmentation.

**NOTE!** This transform does *not* necessarily guarantee that there *will*
be at least one required class present in the augmented image. The transform
works by repeatedly generating crops until one is found where the required
class is present in the crop. As such, it is possible that all attempts will
be exhausted before any crop is found including a required class. The 
`max_attempts` parameter can be adjusted to increase the number of times the
transform will attempt to generate a crop, at the expense of running time.


## Installation

This package can be installed using Pip:

```
$ pip install randomcropclassselective==0.0.1
```


## Usage

```py
transform = A.Compose(
    [
        RandomCropClassSelective(crop_height=256,
                                 crop_width=256,
                                 required_classes=[1, 3],
                                 max_attempts=200,
                                 p=1.0)
    ],
    bbox_params=A.BboxParams(format='albumentations',
                             label_fields=['class_labels'])
)

augmented = TRANSFORM(image=my_image,
                      bboxes=bboxes,
                      class_labels=class_labels)
```