# Using D-FINE obejct detection model to clean a contaminated, single class image datasettemp

## Introduction

A project to clean a contaminated dataset for a single class classification task, using the D-FINE object detection model.

You can find the cleaned dataset at: [Drive Link]()
 
### Project Directory Structure

```
using_dfine_for_cleaning_img_ds/
├── temp_cleaned/
│   ├── background/
│   └── football/
├── main.ipynb
├── requirements.txt
├── README.md
├── .gitignore
└── config.yaml
```

---

## Process Summary

While I've tried my best to document the code properly, which should allow easily recreating the code or using it again, here's a summary of how I worked on this assessment:

1. Manual observation:
    - I performed this just to get a good idea of what the dataset was like

2. Exploring the model input/output and working with small samples:

    - I loaded in the model with the provided pre-trained model weights on GPU and tried to explore the model input/output formats

    - I then tried working with a small sample (20 images) to get acquainted with working in batches with the model

    - Finally, I ran the actual cleaning over both the folders: ***background*** and ***football***
    
    - The primary idea behind processing the pre-labelled football images was just to ensure that we do end up having any ***False Positives*** in our dataset.

3. (Bonus Task):


---

## Inference

- The correctly labelled positive images (containing ball) are ```TP = 3861```

- The correctly labelled  negative images (not containing ball) are ```TN: 3263```

- The incorrectly labelled positive images (not containing ball, but labelled as positive) are ```FP: 189```

- The incorrectly labelled negative images (containing ball, but labelled as negative) are ```FN: 1286```

#### Hence, I had to remove ```1286``` images from the background folder (and move over to the football folder)
#### I also had to remove ```189``` images from the football folder (and move over to the background folder)

---

## Issues I ran into

- ### Requirement conflicts:

    1. Too many of these, the original requirements.txt file given in the [repository](https://github.com/ArgoHA/custom_d_fine) has many, mnay dependency conflicts, especially regarding the onnxruntime and numpy.

    2. As an advisable side-note, using Python 3.11 or 3.10 would be better.

    3. Also, install tensorrt as:
    
    ```export NVIDIA_TENSORRT_DISABLE_INTERNAL_PIP=0```

    ```pip install tensorrt```

    <!-- 4. And, ***oh my god***, the amount of repeated dependency specifications, specifically because a few dependencies install some packages themselves - *I am however, leaving them as they are for now* -->

- ### Output Quality
    - #### the pre-trained model produces quite a few false positives (detecting footballs where they do not exist)
        - it's worth noting that many of these images do not even contain any round figure that could be mistakenly classified as a ball
        - this is possibly caused by the low quality of images

    - #### there are a few false negatives, too
        - while relatively smaller, there are a few false negatives, as well, possibly in the range of 1/10 to 1/8 images

    - ### While I did not try solving this by retraining the model due to time constraints, it does pose some major problems.


