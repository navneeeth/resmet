# Augmenting Backbone Approaches To Instance-level Recognition For Artworks
Studying the behaviours and patterns drawn by [ResNets](https://en.wikipedia.org/wiki/Residual_neural_network) on '[The Met](https://www.metmuseum.org/)' dataset.


Here, we use 'The Mini Met' & 'Met' [dataset](http://cmp.felk.cvut.cz/met/) which contains 33501 and 220k+ classes of 'art' respectively. In our experimentation so far, we have delved into the following (click to download the Descriptors):
1) [ResNet18 on ImageNet](https://drive.google.com/file/d/1amFEYsUmJkJlG1Kt0RQ_dAiYS-kojrgi/view?usp=sharing): The standard ResNet backbone. 
2) [ResNet18SRC on ImageNet](https://drive.google.com/file/d/1c6X9DxyGKHgKxj69UPZE2BhWvXL2z20X/view?usp=sharing): Trained on Met with contrastive loss (Syn+Real-Closest). Initialization: ImageNet pre-training.
3) [ResNet18-SWSL-SRC](https://drive.google.com/file/d/11aOyuZaUFze7ffDHJz-A7__rWArT2fsW/view?usp=sharing): Trained on Met with contrastive loss (Syn+Real-Closest). Initialization: SWSL.
### Usage



Navigate (```cd```) to ```[YOUR_MET_ROOT]/met/code```. ```[YOUR_MET_ROOT]``` is where you have cloned this repository. 
<details>
  <summary><b>Readily train a non-parametric model</b></summary><br/>
  
  Here, we collectively perform the training and extract the descriptors for the network variant that you wish to run from this list:<br/>
  r18INgem<br/>
  r50INgem<br/>
  r50_swav_gem<br/>
  r50_SIN_gem<br/>
  r50INgem_caffe<br/>
  r18_sw-sup_gem<br/>
  r50_sw-sup_gem<br/>
  resnext50_32x4d_swsl<br/>
  resnext101_32x4d_swsl<br/>
  resnext101_32x8d_swsl<br/>
  resnext101_32x16d_swsl<br/>
  
  Enter the variant name as one of the above when prompted.<br/>
  For the datasets, you can choose to train it on the Mini dataset or the full dataset. You can download the datasets [here](http://cmp.felk.cvut.cz/met/).
  <br/>You can download the train, test, and validation descriptors [here](http://cmp.felk.cvut.cz/met/).<br/>
  Once ready, run the following:
  ```
  python3 train_the_model.py
  ```
  </details>
  <details>
  <summary><b>Perform a KNN test</b></summary>
  Once ready, run the following and follow the prompts:
  ```
  python3 run_the_test.py
  ```
  </details>
  
<details>

  <summary><b>Descriptor extraction</b></summary><br/>
  
  Here, we extract the descriptors of the train, test, and validation sets.

  Run the following to begin extraction of the descriptors for ResNet-18 trained on ImageNet on The Met dataset.
  ```
  python3 extract_descriptors.py
  ```

</details>

<details>

  <summary><b>kNN classifier & evaluation</b></summary><br/>
  
  The next step is to evaluate the performance with GAP and derive accuracies.

  Run the below command and use -h for help options as shown below:
  ```
  python3 -m examples.knn_eval -h
  ```

  Example (using ground truth and descriptors downloaded from [here](http://cmp.felk.cvut.cz/met/), after unzipping both):  
  ```
  python -m examples.knn_eval [YOUR_DESCRIPTOR_DIR] --autotune --info_dir [YOUR_GROUND_TRUTH_DIR]
  ```

</details>

<details>
  
  <summary><b>Training with contrastive loss</b></summary><br/>

  Train using a parametric approach with contrastive learning.

  For detailed explanation of the options run:  
  ```
  python3 -m examples.train_contrastive -h
  ```

</details>


---
