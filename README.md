# CIBMTR-EfficientNetV2 
This repo contains my solution for CIBMTR competition. The competition was hosted on Kaggle and the task was to improve the prediction of transplant survival rates for patients undergoing allogeneic Hematopoietic Cell Transplantation (HCT).

All training was done on GPU P100 on kaggle.

I adopted a new method, EfficientNetV2, to complete the competition. My solution received 3 votes and 4 copies in the kaggle community.

**Model Selection**

Inspired by the efficiency of EfficientNetV2 in image predication, I wanted to explore its potential for non-image predication. I chose Efficientnetv2_b2.

**Build Datasets**

While building the validation dataset, I encountered tensor shape mismatch errors that did not occur in image-based tasks. After analyzing the issue, I identified data type inconsistencies as the root cause. Adapted methods from [here](https://www.kaggle.com/code/kendontcare11/public-classifier-cat-xgb-lb-0-688) to handle data, ensuring compatibility with models.

**Modeling**

I optimized model architecture by tuning hidden layers, filter counts,and dropout rates. During the optimization phase, I initially introduced dropout layers to mitigate overfitting. However, after analyzing the training dynamics, I noticed that dropout was hindering the model's ability to learn comlpex pattens, resulting in suboptimal performance. Through a series of ablation experiments, I systematically removed dropout layers and observed a significant improvement in model performance, with AUC reaching 0.99. This experimence taught me the importance of tailoring regularization strategies to specific tasks and datasets.  

![image](https://github.com/user-attachments/assets/13732aa4-c7b9-4553-a1e0-b91995c8e153)


**Learning Rate**

Before modeling, I focus on optimizing the learning rate schedule to ensure stable and efficient convergence. I systematically tuned key parameters, including lr_start, lr_max, lr_min, lr_ramp_ep, lr_sus_ep, and lr_decay.

During the model optimization process, I realized that individual parameter tuning yielded limited improvements, and the key to maximizing performance lay in finding the right combination of hyperparameters. This experimence deepened my understanding of model optimization.

My solution on kaggle:[CIBMTR-EfficientNetV2](https://www.kaggle.com/code/wanyizhouzzz/cibmtr-efficientnetv2/notebook#Learning-Rate).

It's also in the cibmtr-efficientnetv2.ipynb.
