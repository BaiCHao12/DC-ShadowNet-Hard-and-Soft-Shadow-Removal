# DC-ShadowNet

## Introduction
This is an implementation of the following paper
**DC-ShadowNet: Single-Image Hard and Soft Shadow Removal Using
Unsupervised Domain-Classifier Guided Network. (ICCV'2021)** 
Yeying Jin, [Aashish Sharma](https://aasharma90.github.io/) and [Robby T. Tan](https://tanrobby.github.io/pub.html)

### Abstract
Shadow removal from a single image is generally still an open problem.
Most existing learning-based methods use supervised learning and require a large number of paired images (shadow and corresponding non-shadow images) for training.
A recent unsupervised method, Mask-ShadowGAN, addresses this limitation. 
However, it requires a binary mask to represent shadow regions, making it inapplicable to soft shadows. 
To address the problem, in this paper, we propose an unsupervised domain-classifier guided shadow removal network, DC-ShadowNet. 
Specifically, we propose to integrate a shadow/shadow-free domain classifier into a generator and its discriminator, enabling them to focus on shadow regions.
To train our network, we introduce novel losses based on physics-based shadow-free chromaticity, shadow-robust perceptual features, and boundary smoothness. 
Moreover, we show that our unsupervised network can be used for test-time training that further improves the results. 
Our experiments show that all these novel components allow our method to handle soft shadows, and also to perform better on hard shadows both quantitatively and qualitatively than the existing state-of-the-art shadow removal methods.



Overview of the proposed method:
<p align="center"><img src="teaser/network.png" width="98%"></p>

### Datasets
1. SRD (please download [train](https://drive.google.com/file/d/1W8vBRJYDG9imMgr9I2XaA13tlFIEHOjS/view) and test from the [authors](http://www.shengfenghe.com/publications/)).
[Extracted Shadow Masks in the SRD Dataset](https://github.com/vinthony/ghost-free-shadow-removal)

2. [AISTD](https://www3.cs.stonybrook.edu/~cvl/projects/SID/index.html) 

3. [LRSS: Soft Shadow Dataset](http://visual.cs.ucl.ac.uk/pubs/softshadows/)

4. [ISTD](https://github.com/DeepInsight-PCALab/ST-CGAN) 

5. [USR: Unpaired Shadow Removal Dataset](https://drive.google.com/file/d/1PPAX0W4eyfn1cUrb2aBefnbrmhB1htoJ/view)

### Shadow Removal Results:
1. SDR Dataset
[DC-ShadowNet Results](https://www.dropbox.com/sh/jhm4kxvq9apubq9/AAB5BickFfGhunK5ezJK0R0_a?dl=0),
[All Results](https://www.dropbox.com/sh/kg87bt5tcmi535n/AACrGNvLgpWd-UTs6NWep9MLa?dl=0)
<img src="teaser/result.png" > 

2. AISTD Dataset
[DC-ShadowNet Results](https://www.dropbox.com/sh/d2bqflmespymtzj/AADyX5NKAkrs5Kq8efkAmGLna?dl=0),
[All Results](https://www.dropbox.com/sh/foqmi8olum6n3qz/AADX3aQ4yzWvKHh4wtAF6YREa?dl=0)

3. LRSS Soft Shadow Dataset
[DC-ShadowNet Results](https://www.dropbox.com/sh/i9rto8h1shbc315/AADa6kvxwtUP8EKju2jSKxn2a?dl=0),
[All Results](https://www.dropbox.com/sh/ryku9yr1j4u4898/AABC2gPoM9scASHZ0N6SmwBDa?dl=0)

### Evaluation
The default root mean squared error (RMSE) evaluation code used by all methods (including ours) actually computes mean absolute error (MAE). 

1. The faster version [MAE evaluation code](https://www.dropbox.com/sh/nva9ddquvgogb5n/AABOHrWx9whMXeItcZfODe9ia?dl=0)
2. The original version [MAE evaluation code](https://drive.google.com/file/d/1-lG8nAJbWajAC4xopx7hGPKbuwYRw4x-/view)

1.1 SRD Dataset, set the paths of the shadow removal result and the dataset in demo_srd_release.m and then run it.

Get the following Table 1 in the main paper on the SRD dataset (size: 256x256).

| Method | Training | All | Shadow | Non-Shadow |
|------------------|----------|----------|------|------|
| **DC-ShadowNet** | Unpaired | **4.66** | 7.70 | 3.39 |
| Mask-ShadowGAN | Unpaired | 6.40 | 11.46 | 4.29 |
| DSC | Paired | 4.86 | 8.81 | **3.23** |
| DeShadowNet | Paired | 5.11 | **3.57** | 8.82 |
| Gong | Prior | 12.35 | 25.43 | 6.91 |
| Input Image | N/A | 13.77 | 37.40 | 3.96 |

1.2 AISTD Dataset, set the paths of the shadow removal result and the dataset in demo_aistd_release.m and then run it.

Get the following Table 2 in the main paper on the AISTD dataset (size: 256x256).
| Method | Training | All | Shadow | Non-Shadow |
|------------------|----------|---------|----------|-----|
| **DC-ShadowNet** | Unpaired | **4.6** | **10.3** | 3.5 |

1.3 LRSS Soft Shadow Dataset, set the paths of the shadow removal result and the dataset in demo_lrss_release.m and then run it.

Get the following Table 3 in the main paper on the LRSS dataset (size: 256x256).
| Method | Training | All | 
|------------------|----------|----------|
| **DC-ShadowNet** | Unpaired | **3.48** |
| Input Image | N/A | 12.26 |

## Pre-trained Model
Download the pre-trained model 
[here]

### Test
python main.py --dataset SRD --phase test

### Train
1. Implement the papers [On the removal of shadows from images (TPAMI,05)](https://www.cs.sfu.ca/~mark/ftp/Pami06/pami06.pdf) and [Recovery of Chromaticity Image Free from Shadows via Illumination Invariance (ICCV,03)](https://www.cs.sfu.ca/~mark/ftp/Iccv03ColorWkshp/iccv03wkshp.pdf)
<img src="teaser/chromaticity.png" > 

### Directory
Download Datasets and run 1, get the Shadow-Free Chromaticity Maps after Illumination Compensation, and put them in the trainC folder, you should see the following directory structure. 
```
${DC-ShadowNet-Hard-and-Soft-Shadow-Removal}
|-- dataset
    |-- SRD
      |-- trainA ## Shadow 
      |-- trainB ## Shadow-free 
      |-- trainC ## Shadow-Free Chromaticity Maps after Illumination Compensation
      |-- testA  ## Shadow 
      |-- testB  ## Shadow-free 
...
```

2. python main.py --dataset SRD --phase train

## Shadow-Robust Feature
<img src="teaser/feature_map.png" > 
VGG feature visualization code is in feature_release folder,
python test_VGGfeatures.py
results are in ./results_VGGfeatures/shadow_VGGfeatures/layernumber/imagenumber/visual_featurenumber_RMSE.jpg
ex:./results_VGGfeatures/shadow_VGGfeatures/22/214/visual_179_0.1125.jpg

## Boundary Smoothness Loss
<img src="teaser/smooth_map.png" > 

### Citation
Please kindly cite our paper if you are using our codes:
