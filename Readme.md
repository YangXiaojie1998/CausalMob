# CausalMob (KDD2025): Official Implementation

This repository contains the Python source code for **CausalMob: Causal Human Mobility Prediction with LLMs-derived Human Intentions toward Public Events**.

## 🎉 Acceptance 🎉 (2024.11.17)
This research has been accepted by KDD 2025! Now pre-print can be accessed with this [link](https://arxiv.org/abs/2412.02155). Official version [link](https://dl.acm.org/doi/10.1145/3690624.3709231) 

## UPDATE (2024.10.09)
We updated sample data (noise processed, can not be used as real world data) in our research with a 25-day length (D = 25, as larger data can not be uploaded). For data description, please find the bottom of this page.

## Environments

To run CausalMob, ensure you have the following dependencies installed:

- **Python**: 3.8.0 
- **Pandas**: 1.5.3
- **NumPy**: 1.23.5
- **Torch**: 1.8.2
- **scikit-learn**: 1.3.0

You can install these dependencies using pip:

```sh
pip install pandas==1.5.3 numpy==1.23.5 torch==1.8.2 scikit-learn==1.3.0
```


## Usage

To use CausalMob, download the source code and run the following command in your terminal:

```
python run.py --causal True --input_window 24 --output_window 24 --device cuda:0 --batch_size 24
```

--causal: Set this to True to enable causal predictions.

--input_window: The number of input time steps.

--output_window: The number of output time steps.

--device: Specify the device for computation (e.g., cuda:0 for GPU or cpu for CPU).

--batch_size: Set the batch size for training.

For other settings, please see source codes in run.py and our paper.

## Data

In our research, we used [Blogwatcher data](https://www.blogwatcher.co.jp/) for human mobility and [Kyodo News data](https://english.kyodonews.net/) for news articles, both data time ranges are from 2023.04.01 to 2024.03.31.

However due to our data privacy policy, we are unable to share these data. Below is the shape of the data used in this repository (number refers to settings in our research):

**D**: Day (366)

**T**: Time interval of a day (24)

**N**: Node of regions (490)

**F**: Features of human mobility (in our research, it is 1, representing human volume)

Data Files:

1. **flows.npy**: Human mobility data with a shape of D × T × N × F. The time interval is 15 minutes here, so we use --interval = 4 in run.py.
2. **odmetrics_sparse_tensors.pk**: Normalized Origin-Destination (OD) data in a list with length D × T and for each item [ N × N sparse tensor].
3. **prev_treats_sum.npy**: Public event features in our research area, with a shape of [D × T] × N × scores (10 scores in our research). This file includes historical event features.
4. **post_treats_sum.npy**: Public event features in our research area, with a shape of [D × T] × N × scores (10 scores in our research). This file considers only predictable future public events.
5. **poi_distribution.pk**: A dict Points of Interest (POI) distribution in each region amd for each region code 17 types of POI are counted. We collected POI data from Open Streat Map ([OSM](https://www.openstreetmap.org/)). Specifically, considering pravicy issues (Region code aligns other data), we provided processed poi_data (D regions × C categories) in run.py.


## Citing
Arxiv Version:
```
@article{yang2024causalmob,
  title={CausalMob: Causal Human Mobility Prediction with LLMs-derived Human Intentions toward Public Events},
  author={Yang, Xiaojie and Ge, Hangli and Wang, Jiawei and Fan, Zipei and Jiang, Renhe and Shibasaki, Ryosuke and Koshizuka, Noboru},
  journal={arXiv preprint arXiv:2412.02155},
  year={2024}
}
```
ACM official version:
```
@inproceedings{yang2024causalmob,
title = {CausalMob: Causal Human Mobility Prediction with LLMs-derived Human Intentions toward Public Events},
author = {Yang, Xiaojie and Ge, Hangli and Wang, Jiawei and Fan, Zipei and Jiang, Renhe and Shibasaki, Ryosuke and Koshizuka, Noboru},
booktitle = {Proceedings of the 31st ACM SIGKDD Conference on Knowledge Discovery and Data Mining V.1},
pages = {1773–1784},
year = {2025}
}
```
