title: Mass Spectrometry

### Dataset

The dataset consists of 571 mass spectra values from 213 strains representing 20 Gram-Positive & 20 Gram-Negative bacterial species. An in vitro mock-up mixture dataset was created, with 10 selected pairs of species with varying taxonomic proximities consisting from the same species with same genus, different genera and Gram types. Each mixture was prepared at 9 concentration ratios with 2 replicates, resulting in a dataset of 360 spectral values. The dataset also includes 80 pure spectra samples. The dataset has 571 instances, 1301 features, 20 classes, and 1300 numeric values.

### Objective

The dataset exhibits an analyze and classify objective  based on a unique mass spectral fingerprint. It includes information about the number of bacterial strains and pure mass spectra values for each species making it a unique multilabel classification problem. (Ie, Species name: Bacillus Cereus, Species ID: BAC.CEU, No. of Strains: 10, No. of Spectra: 26). In published articles, an extended version of the SVM classification approach is in practice. SVM is usually implemented in cases of binary classification, where a rule is implied to classify instances from vector space X = R2  into 2 half spaces. The dataset can be represented as an open-ended decision tree, necessitating building a novel approach, driven by questions - Does CNNs perform better than naive approaches to pure spectra label classifications as the spectra exhibits spatial dependencies? and What performance measure benchmarks and approaches could be adopted as therefore standard, in classifying large dimensional spectral data with spatial dependencies? The presented approach in this abstract aims to ensure effective distribution of classes is conserved through splitting of data by nested cross validation approach since it is a relatively smaller dataset and to also prevent overfitting during hyperparameter tuning.
	
A subset of the presented dataset contains a certain number of species that are exigent to predict, thus the presented approach in this abstract also considers evaluating hamming loss function, Micro & Macro precisions through LRAP evaluation where this subset is evaluated by ranking of labels for each sample. Additionally, when working with decision trees, specific plots to see how the decision tree arrives at a solution is possible, thus helping us fine tune the model to the dataset further, this assists in better prediction, enhancing the model's predictive & classification accuracy, whilst  also allowing us to choose from efficient approaches (XGBoost, LightGBM classifiers) to specificate the model to the dataset in great detail. 


### Methods Applied

#### Smoothing

The Savitzky-Golay filter is applied to the spectra represented by a vector to obtain smooth intensity values while preserving key features within the spectral data. Normalization is performed before applying smoothing. This was primarily required as the feature scale varies widely within the entire spectra values and the presence of more than 30% of the spectra containing values 0 which would be considered as outliers. During normalization, to address the presence of values 0 which would result in inconsistent data, the spectra is divided by its sum and if the sum results in 0, it is replaced with NaN to avoid division by 0 and the NaN's are then replaced with 0 to ensure the spectra value remains consistent without loss of information.

After normalization, the Savitzky-Golay filter is applied to fit successive polynomial functions to the subsets of the spectral values therefore helping reduce the loss of key features like peak height whilst reduction of noise. The data consists of a set of points xi, yi; j = 1…n, where xi is an independent variable and yi is an observed value. They are treated with a set of m convolution coefficients given by Ci according to the expression.
$$
y_{j} = \sum_{i=(1-m)/2}^{(m-1)/2} C_{i}y_{i+j}
$$

#### Baseline Correction

Asymmetric Least Square method is applied to derive smoother baseline function. This is adopted because generally peaks and baseline points have positive and negative deviations respectively, ALS penalizes the positive deviations more when compared to the negative deviations, thus resulting in a smoother baseline. Pybaselines allows an iterative approach where the penalties are described and repeated for a number of iterations. The minimized function is given by $$ S = \sum_{i=1}^{N} w_{i}(y_{i} - z_{i})^{2} + \lambda \sum_{i=1}^{N-d} (\Delta^{d}z_{i})^{2} $$, where, __wi__  is the weight that is adjusted based on __yi__ , __zi__ is the baseline at index __i__, __yi__  is the observed intensity at index i, and whose linear system is given by $$ (W + \lambda D_{d}^{T}D_{d})z = Wy $$where, 
$$
w_{i} = 
\begin{cases} 
p & \text{if } y_{i} > z_{i} \\
1 - p & \text{if } y_{i} < z_{i}
\end{cases}
$$

#### Peak Picking

Peak picking is performed by identifying spectra values meeting a specified intensity threshold r, which can be formally defined as a vector of spectra values x  R, where a set of peaks represented by z for each x  R, where each peak must have an intensity value zr. A recent study Impact of Adjusting the Minimum Signal-Intensity Threshold in MALDI-TOF MS: a Metrics-Based Overview, states the impact of adjusting the minimum signal-intensity threshold on the performance of MALDI-TOF mass spectrometry. The approach addresses the impact of tweaking the threshold intensity or signal intensity to mitigate the resulting noise increase through increased laser shots and ensemble averaging whose impact is observed across three aspects of MALDI-TOF mass spectrometry. The default minimum signal intensity threshold value set to 600 arbitrary units led to the exclusion of low-intensity peaks. Lowering the threshold to 3 arbitrary units enabled detecting greater numbers of needed peaks resulting in 50-100% increase in the number of peaks detected for bacteria Ewingella Americana and also amongst bacteria's like Penicillium Olsonii and Pholcus Manueli. If the threshold value is decreased, it also means picking up more peaks which could increase the noise. This was addressed by combining the lower threshold value with an increased number of answer shots, typically between 2,00 to 10,000 resulting in ensemble averaging reducing the random noise and improving the signal-to-noise ratio of the detected peaks.

### Defining Taxonomic Proximites

Similarity between species, irrespective of their Genus, when using MALDI-TOF mass spectral data increases with their taxonomic proximities. Figure 2 includes the dendrogram built on top of the heatmap. But considering the additional complexities of this visualization, and the nature of understandability, in Tabular Phase 3, the dendrogram separating the species/genera was plotted separately.

The similarities between pairs of species increases with increase in their taxonomic proximity, making combined fingerprints of species from the same genus harder to discriminate. Bacillus cereus and Bacillus thuringiensis are species of the same order which belong to the same Genera - Bacillus, these bacteria have very similar taxonomic proximites which make them very hard to discriminate. A study named Bacillus anthracis, Bacillus cereus, and Bacillus thuringiensis—One Species on the Basis of Genetic Evidence mentioned the only established difference between B. cereus and B. thuringiensis strains is the presence of genes coding for the insecticidal toxins, usually present on plasmids. If these plasmids are lost, B. thuringiensis can no longer be distinguished from B. cerus. Furthermore, the results are in agreement with the view of B. cereus  as the more ancestral species with many of the strains belonging to the variants B. anthracis and B. thuringiensis encoding their most characteristic phenotypic properties from extrachromosomal DNA. Whereas, some of the relatively easier to find species belong to Genus Clostridium. Clostridium difficile and glycolicum. Though related, they have a much distinct metabolic and proteomic profile to each of them, making them distinct even when they belong to the same Genera.

### Binarization

Looking into the properties/characteristics of all the bacteria present the binarization of the most prominent, and the follow through of the approved questions made a few species stand out from each other in terms of taxonomical proximites. From observations from Figure 3, the Sheigella family consists of (S. boydii, S. flexneri and, S. sonnei) is closely related to the Escherichia family (E. coli). Some strains of the Shigella are usually considered to be another variant of the Esecherichia genre, and the mass spectra of both the species are extremely similar to each other due to the fact that these both share a large number of proteins which leads to overlapping during spectral profiling thus making them especially hard to discriminate. 

Shigellae are Gram-negative, nonmotile, facultatively anaerobic, non-spore-forming rods. Shigella are differentiated from the closely related Escherichia coli on the basis of pathogenicity, physiology (failure to ferment lactose or decarboxylate lysine) and serology. The genus is divided into four serogroups with multiple serotypes: A (S dysenteriae, 12 serotypes); B (S flexneri, 6 serotypes); C (S boydii, 18 serotypes); and D (S sonnei, 1 serotype). 

Biochemical characteristics and serotyping are usually used to identify the species. However, many isolates cannot be distinguished as either E. coli or Shigella spp. Molecular methods such as 16S rRNA gene sequencing and protein signature-based matrix-assisted laser desorption/ionization-time of flight mass spectrometry (MALDI-TOF MS) are unable to differentiate Shigella spp. from E. coli. Further, Shigella-like strains of E. coli(enteroinvasive E. coli, EIEC) causing invasive dysenteric diarrhoeal illness make clinical and laboratory diagnosis difficult. In addition, the change in antimicrobial resistance patterns with the change in the serogroup/serotype further highlights the need for accurate identification of Shigella spp. so that appropriate antimicrobial therapy may be administered.

Figure 5 is obtained by following a hierarchical clustering concept by applying linkages() through complete method following metric evaluation of euclidean to find the distance between each species, given by $$ d^2(r, s) = \frac{2n_r n_s}{n_r + n_s} \|\bar{x}_r - \bar{x}_s\|_2^2 $$, where || ||<sub>2</sub> is the euclidean distance, <i>x&#772;<sub>r</sub></i> and <i>x&#772;<sub>s</sub></i> are the centroids of the cluster <i>r</i> and <i>s</i>, and <i>n<sub>r</sub></i>, <i>n<sub>s</sub></i> are the number of elements in the cluster <i>r</i> and <i>s</i>.

### Results from df-analyze
