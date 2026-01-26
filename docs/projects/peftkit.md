title: Peft-Kit 

!!! info "Information:"
    Updates to support **tabular datasets** are coming soon to `Peft-Kit`

Peft-Kit is a lightweight command line, python based toolkit for Parameter Efficient Fine Tuning (PEFT) with Low Rank Adaptation (LoRA) technique utilizing Vision Transformer models for finetuning medium or large sized datasets. 

### Features

* Improves training and predictive accuracy
* Adapts large Vision Transformer models (**google/vit-base-patch16-244**) streamlining and downsizing tasks with minimal computational overhead.
* The current update supports **Lion-Optimizer**

### Vision

- Implement methods to explore different combinations of hyperparameters for attaining efficient hyperparameters tuning.
- Include gradient accumulation methods to treat memory issuses during trainning.
- Improve training time to accelerate training in resource constrainned environments.
- Include additional evaluation metrics like accuracy, precision, recall and F1 score.

### Working

- This model processes images by splitting input images into fixed size patches. Then flattens and projects these patches into embeddings. 
- The model applies the transformer encoder to model the relationship between the patches. 
- Then flattens and projects these patches into embeddings. The model applies the transformer encoder to model the relationship between the patches.
- ViT's are computationally very expensive, therefore with Peft-Kit, the aim is to fine-tune only a small subset of a model's parameters, reducing memory and computational costs, whilst achiveing an equally good lvele of performance compared to that of heavier architectures.
- LoRA is a PEFT method that introduces a small subset of trainable low-rank matrices into the weight updates performed by the developed model. 

### Strenghts & Limitations

Vision Transformers are often considered as black boxes and lack interpretability. Understanding why the model makes certain predictions is a limitation as well as a potential for implementing a novel technique of measurement or monitoring the model's decision making processes. 

Additionally, the following aspects acts as the currently identified strenghts and limittions of the tool, but is not subjected to the following: 
- The script fine-tunes a Vision Transformer (ViT) model for image classification tasks using PEFT, the script accesses the system's GPU for faster data loading, training and evaluation. 
- The script relies on the user's GPU, thus the size of the dataset would be directly proportional to the training time, there is a potential for overfitting as the number of epochs is manually defined. 
- The use of 'torch' has has conflicts with python@3.12 version and above, future update include but is not subjected to adding additional calculation metrics like accuracy, precision, recall, and F1 score.

### Usage

!!! warning "Note:"
      Causes dependencies issues between **python3.11** & **pytorch**. Create a virtual environment with

<!-- termynal -->
```
$ python3.10 -m venv .venv
```

Run
<!-- termynal -->
```
chmod +x peft.sh
./peft.sh
```

Then,
<!-- termynal -->
```
cd src
python3 finetune.py --help
python3 feature_extraction.py --help
```

Finetune your data using: 
<!-- termynal -->
```
python3 finetune.py --data-path sample_data --num-epochs <num-epochs> --batch-size <batch-size>
```

Extract features with: 
<!-- termynal -->
```
python3 feature_extraction.py --model_path <.pth path> --dataset_path <dataset_path>
```

Before loading, the dataset is expected to in a specific format: 
<!-- termynal -->
```
sample_data
├── folder 
    ├── class1
    ├── class2
    └── ...
```

The output `.pth` file generates within the same directory.

!!! warning "Warning:"
      To enable GPU training within macOS environment, instal `tensorFlow-macos` & `tensorFlow-metal`

/// tab | `pip`

    :::bash
    pip install tensorflow
    pip install tensorflow-metal
///

/// tab | uv

    :::bash
    uv init tf_project
    uv add tensorflow tensorflow-metal

///

/// tab | pipenv

    :::bash
    pipenv install tensorflow tensorflow-metal

///

### Performance Validation

Results from both phases were compared to the top performing teams of the __ICIP 2022 grand challenge__. Team __NEGu__ achieved the best performance, based on `CBNetV2`, constructed as a composite layer of `FPNs`. The team obtained a __F1__ score of *0.995* and __mIoU__ score of *0.942*. The runner up team __ZUSFTA__ was similar to the performance of the __BAD__ crew which achieved a __mIoU__ score of *0.932* and *0.930* and __F1__ scores of *0.989* and *0.987* respectively. The __mAPs__ of these top three teams are *0.905* and *0.896*. The first and the runners up team had also employed pseudo labeling strategies for further achieving better performance. The BAD crew employed a combination of 5 models which was related to the `Cascade RCNNs`, generalized focal loss with `FPN`, `HTC (High-throughput Computing)`, `HRNetV2` (used on object detection with multi level representations generated from deep high resolution representation learning), `HTC x 101` (version x101 used on the Hybrid Task Cascade) of the `TODO` (Task-Aligned One Stage Object Detection).

During the initial setup, in phase 1, the ResNet50 model's predictive accuracy was shown to be *0.877*. The image datasets, this time with different configurations, showcased an improved accuracy score of *0.956*. The `SGD` and `Logistic Regression` models were the top performing models achieving accuracy scores of *0.911* and *0.908* with __F1__ scores if *0.911* and *0.988* respectively. The __F1__ scores had slight variations between different configurations in both the hold and the 5-Fold performance. The *AUROC* scores were *0.980* and *0.995* for the SGD and the LR model respectively, and remain the same in both the holdout and the 5 fold performance set. In phase 2, the LR was the top performing model. RF and the KNN demonstrated significant improvements and showcased consistent values across different configurations. LR showcased consistent accuracy and __F1__ scores of *0.987* and the __AUROC__ value were *0.997* across different configurations. RF demonstrated consistent accuracy of *0.976* across different configurations.

### Training Results

The developed peft-kit represents a step forward in combining computational efficiency with competitive accuracy, in training image datasets. By leveraging lightweight architectures, selective parameter tuning, and adaptability to raw images as well as degraded image qualities with varying characteristics, the developed method outperformed traditional models like `ResNet50`, `Faster R-CNN` in many aspects, and offer comparable results to ICIP 2022s top-performing models. 

By utilizing only a subset of parameters through the LoRA approach and integrating ViT, the model achieves F1 scores of *0.983* and accuracy of *0.983*. This methodology performed similarly compared to the top performing models of the ICIP 2022 grand challenge, such as `CBNetV2` and `YOLOv5` based ensembles, without the need for extensive architectures or computational resources. The adaptability of the developed method to degraded image datasets and its ability to generalize effectively, is validated by 5-fold cross validation and holdout set performance. 

This also poses a solid model and approach during image detection training, testing and validation activities, and help make informed decisions in low-resource environments. The tool also provides GPU training during dataset loading, testing and training.
