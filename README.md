# Random Crop Class Selective

This is a simple custom Albumentations transform which acts as a random crop
while ensuring that specific classes will be preserved in the crop
post-transformation. 

This may be useful if it is desired to create augmentations of rare classes, to
ensure that these rare classes will actually be present in the augmentation.

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