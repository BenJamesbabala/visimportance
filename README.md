# [Learning Visual Importance for Graphic Designs and Data Visualizations](http://visimportance.csail.mit.edu/)

Code to train and test models to predict importance (saliency) on graphic designs and data visualizations.
We also provide links to our [models](https://github.com/cvzoya/visimportance/tree/master/models) and our train/test [data](https://github.com/cvzoya/visimportance/tree/master/data).

If you use this code, please consider citing:
Zoya Bylinskii, Nam Wook Kim, Peter O'Donovan, Sami Alsheikh, Spandan Madan, Hanspeter Pfister, Fredo Durand, Bryan Russell, and Aaron Hertzmann. "Learning Visual Importance for Graphic Designs and Data Visualizations" (UIST'17)

``` 
@inproceedings{predimportance,
    author    = {Zoya Bylinskii and Nam Wook Kim and Peter O'Donovan and Sami Alsheikh and Spandan Madan
                 and Hanspeter Pfister and Fredo Durand and Bryan Russell and Aaron Hertzmann},
    title     = {Learning Visual Importance for Graphic Designs and Data Visualizations},
    booktitle = {Proceedings of the 30th Annual ACM Symposium on User Interface Software \& Technology},
    year      = {2017}
}
```

This code is written in Python 2.7 using the [Caffe library](http://caffe.berkeleyvision.org/), and is based on [code for semantic segmentation](https://github.com/shelhamer/fcn.berkeleyvision.org). 

About our models:
------
  * We provide [pre-trained models](https://github.com/cvzoya/visimportance/tree/master/models) for both graphic design and data visualization importance prediction. These models were separately trained on the GDI and Massvis datasets, respectively. 
  * We initialized our models using the pre-trained [VOC-FCN32s](https://github.com/shelhamer/fcn.berkeleyvision.org/blob/master/voc-fcn32s/caffemodel-url) and only fine-tuned the final importance prediction layers and additional skip connections (if applicable).

Setting up training:
------

1. Choose whether to train an importance model for graphic designs or data visualizations. The models have slightly different architectures, and the training data is different.

2. Download the corresponding [data](https://github.com/cvzoya/visimportance/tree/master/data). We provide links to all the image files and ground truth importance maps. Once you clone this repo, if you download directly into the data directory, then the file paths indicated in the prototxt files should point to the right places.

3. Download `surgery.py` from [https://github.com/shelhamer/fcn.berkeleyvision.org]. Download the pre-trained [VOC-FCN32s](https://github.com/shelhamer/fcn.berkeleyvision.org/blob/master/voc-fcn32s/caffemodel-url).

4. Check for paths. Look for the `#CHANGETHIS` comment throughout the files.

5. Start training: `python solve.py N` (where N is replaced by the desired GPU ID)

### About our data loaders:
  * We wrote custom data loaders for both models in [imp_layers.py](https://github.com/cvzoya/visimportance/blob/master/gdi/imp_layers.py) and [imp_layers_massvis.py](https://github.com/cvzoya/visimportance/blob/master/massvis/imp_layers_massvis.py) which get invoked by the data layers (see top of train.prototxt and val.prototxt files)
  * We also provide an example of how to load data using a pre-constructed LMDB database, without relying on these custom data loaders (see [gdi/fcn16_lmdb](https://github.com/cvzoya/visimportance/tree/master/gdi/fcn16_lmdb)). In this case, all the data processing occurs during database construction (see [create_lmdb_data.py](https://github.com/cvzoya/visimportance/blob/master/gdi/fcn16_lmdb/create_lmdb_data.py))


