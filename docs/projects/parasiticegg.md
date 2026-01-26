title: Parasitic Egg Detection
description: ICIP 2022 Grand Challenge Problem

To create a novel approach to a multiclass classification problem to detect and classify parasitic eggs in varied, degraded, low-quality images in resource constrained environments. The project's goal was to develop a PEFT method to reduce the gap between performance of lighter architectures, in an resource constrained environments compared to heavier architectures.

### Motivation

Almost 24% of the world's population is affected by soil transmitted Helminth Infections. Known as helminths, are large macroparasites and the adults can usually be seen with the naked eyes. These are worms that can be soil transmitted and infect the gastrointestinal tract. There are other parasitic worms such as schistosomes which reside in blood vessels. More than thousands of eggs are produced each time the female worm deposits its eggs. The need for parasitic egg detection and classification remains the need of the hour as current diagnostic methods heavily rely on manual examination by skilled technicians which is both labour intensive and time consuming tasks. The existing convolution neural networks or also known as CNNs demonstrate tremendous potential for accurate parasite egg detection and classification. However due to the morphological characteristics of the parasitic eggs, fine-tuning these models become an essential aspect. This method shows low sensitivity, is time-consuming (approximately 30 minutes per sample) requires an experienced and skilled medical laboratory technologist and is impractical for use on-site. This means an automated routine fecal examination for parasitic disease is essential.

### Methedology

The [Chula-ParasitEgg 11](https://icip2022challenge.piclab.ai/dataset/) contains 11,000 images of different parasitic egg images which belong to different genus with varying morphological characteristics, obtained from fecal smear samples. The images acquired underwent an inconsistent degradation procedure to ensure the model built around is robust and capable of detecting parasitic eggs from low-quality images. Classification Modelling was done using an automated ML tool named df-analyze which runs the image datasets against different algorithms like Naive Bayes, Random Forest, etc. Evaluation of all developed models was achieved by testing the model on a subset of the dataset. They were initially passed through df-analyze without performing any preprocessing. Models demonstrated low recall, accuracy and F1 values. The images in phase 1 were trained on a ResNet50 model and were passed to [df-analyze](https://github.com/stfxecutables/df-analyze). The images in phase 2 were then trained using peft-kit which demonstrated improved scores, and exceeded the expectations.

### Degraded Images

The visual quality of the microscopic images that were captured followed a degradation phase so that detection became more challenging with an aim of increasing the robustness of the detection models. 

The stool samples were examined microscopically by direct simple smear and the degradation steps are as follows: 

* The specimens are fixed with 10% formalin before being stored at 4 degree celsius. 
* The images are cropped by each side by a random value from 0 to 30% and the gaussian blur with a standard deviation is applied between 0.0 and 3.0. 
* Motion blue is applied to 10% of the total images with a random kernel size deviation between 0.0 and 25.5 so that each color channel is colored separately. 
* Poisson noise with an adaptive lambda adding a value in a range of -25 to +25 to the S channel of the HSV color space. 
* Lastly, the contrast is adjusted using a gamma correction for a gamma value between 0.5 to 2.0.
