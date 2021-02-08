# Tensorflow-2.0-FCN-
## Installation
Install packages from requirements.txt
```pip3
$ pip3 install -r ./packages/requirements.txt
```

## How to use
### Folder structure
```bash
.
├── dataset
│   ├── FCN_500_imageset                # raw images of dataset, it's ok to rename the folder name as you wish, remember to modify data path in config.py
│   └── FCN_500_refine_txx              # 2-D txt labels, it's ok to rename the folder name as you wish, remember to modify data path in config.py
├── validation_data                     # input images for evaluation
├── validation_result                   # evaluation result
├── log
│   └── fits                            # tensorbaord logs directory
├── packages
│   └── requirements.txt
├── config.py
├── data_generator_multi_path_crop.py
├── model.py
├── train.py
└── validation.py
```

### setup configuration
Specify your own data set and training paramenter in ```config.py```

```python3
_CFG.TRAIN.IMG_SIZE           = (224,224)
_CFG.TRAIN.BATCH_SIZE         = 5
_CFG.TRAIN.EPOCHS             = 60  
_CFG.TRAIN.FCN_TYPE           = 2    
_CFG.TRAIN.N_CLASSES          = 2 
_CFG.TRAIN.OPTIMIZER          = 0 # 0: Adelta, 1: Adam 
_CFG.TRAIN.DATASET            = ['./dataset/FCN_500_imageset', './dataset/FCN_imageset'] 
_CFG.TRAIN.LABELSET           = ['./dataset/FCN_500_refine_txt', './dataset/FCN_refine_txt'] 
```
Notice: 
  * ```DATASET``` and ```LABELSET``` support list of input images, keep labeset be the same order as dataset
  * labels are 2D array recorded in text files, each class is denoted as corresponding value

### Train your own dataset
simply input below comment in the directory
```bash
$ python3 train.py

6725/6725 [==============================] - ETA: 0s - loss: 0.0131 - accuracy: 0.9964     
Epoch 00001: saving model to FCN2s.h5
6725/6725 [==============================] - 16032s 2s/step - loss: 0.0131 - accuracy: 0.9964
Epoch 2/60
6725/6725 [==============================] - ETA: 0s - loss: 0.0062 - accuracy: 0.9980     
Epoch 00002: saving model to FCN2s.h5
...
Epoch 60/60
6725/6725 [==============================] - ETA: 0s - loss: 0.0023 - accuracy: 0.9992     
Epoch 00060: saving model to FCN2s.h5

```

## Evaluate your own model
## Setup configuration
Specify your own data set and training paramenter in ```config.py```
```python3
_CFG.EVAL.USE_CPU             = True          # if you want to evaluate result in the middle of training process, set this parameter as True.
                                            # otherwise, set this value as False to use GPU instead
_CFG.EVAL.INPUT_SIZE          = 320
_CFG.EVAL.FIRST_LAYER_SIZE    = 320
_CFG.EVAL.FCN_TYPE            = 2             # FCN_TYPE has to be set as 2, 4, or 8 and should be the same as configuration for training
_CFG.EVAL.N_CLASSES           = 2 
_CFG.EVAL.THRESHOLD           = 0.5
_CFG.EVAL.MAX_BATCH_SIZE      = 2
```
### Evaluate the model
input the comment as follows
```bash
$ python3 validation.py
```
evaluation result will be saved in ```./validation_result```
