##### Table of Content

1. [Introduction](#cpm-color-pattern-makeup-transfer)
1. [Datasets](#datasets)
1. [Getting Started](#getting-started)
	- [Requirements](#requirements)
	- [Usage Example](#usage)
1. [Training & Evaluation](#training-and-evaluation)

# CPM: Color-Pattern Makeup Transfer

- CPM is a holistic makeup transfer framework that outperforms previous state-of-the-art models on both light and extreme makeup styles.
- CPM consists of an improved color transfer branch (based on [BeautyGAN](http://www.colalab.org/projects/BeautyGAN)) and a novel pattern transfer branch.
- We also introduce 4 new datasets (both real and synthesis) to train and evaluate CPM.
---

### Datasets

We introduce ✨ 4 new datasets: **CPM-Real**, **CPM-Synt-1**, **CPM-Synt-2**, and **Stickers** datasets. Besides, we also use published [LADN's Dataset](https://georgegu1997.github.io/LADN-project-page/) & [Makeup Transfer Dataset](http://liusi-group.com/projects/BeautyGAN).

CPM-Real and Stickers are crawled from Google Image Search, while CPM-Synt-1 & 2 are built on [Makeup Transfer](http://liusi-group.com/projects/BeautyGAN) and Stickers. *(Click on dataset name to download)*

|    Name  						  | #imgs | Description						   | - 									|
|:-------------------------------:|:-----:|:-----------------------------------|:----------------------------------:|
|[CPM-Real](https://public.vinai.io/CPM-datasets/CPM-Real.zip)| 3895  | real - makeup styles 			   |![CPM-Real.png](./imgs/CPM-Real.png)|
|[CPM-Synt-1](https://public.vinai.io/CPM-datasets/CPM-Synt-1.zip)| 5555| synthesis - makeup images with pattern segmentation mask|![./imgs/CPM-Synt-1.png](./imgs/CPM-Synt-1.png)|
|[CPM-Synt-2](https://public.vinai.io/CPM-datasets/CPM-Synt-2.zip)| 1625| synthesis - triplets: makeup, non-makeup, ground-truth|![./imgs/CPM-Synt-2.png](./imgs/CPM-Synt-2.png)|
|[Stickers](https://public.vinai.io/CPM-datasets/Stickers.zip)|577| high-quality images with alpha channel |![Stickers.png](./imgs/Stickers.png)|


### Getting Started

##### Requirements

- python=3.7
- torch==1.6.0
- tensorflow-gpu==1.14
- [segmentation_models_pytorch](https://github.com/qubvel/segmentation_models.pytorch)

##### Installation

``` sh
# clone the repo
git clone https://github.com/VinAIResearch/CPM.git
cd CPM

# install dependencies
conda env create -f environment.yml
```

##### Download pre-trained models

- Download CPM’s pre-trained models: [color.pth](https://public.vinai.io/CPM_checkpoints/color.pth) and [pattern.pth](https://public.vinai.io/CPM_checkpoints/pattern.pth). Put them in `checkpoints` folder.

```sh
mkdir checkpoints
cd checkpoints
wget https://public.vinai.io/CPM_checkpoints/color.pth
wget https://public.vinai.io/CPM_checkpoints/pattern.pth
```

- Download [PRNet pre-trained model] from [Drive](https://drive.google.com/file/d/1UoE-XuW1SDLUjZmJPkIZ1MLxvQFgmTFH/view). Put it in `PRNet/net-data`

##### Usage

```sh
# Color+Pattern: 
CUDA_VISIBLE_DEVICES=0 python main.py --style ./imgs/style-1.png --input ./imgs/non-makeup.png

# Color Only: 
CUDA_VISIBLE_DEVICES=0 python main.py --style ./imgs/style-1.png --input ./imgs/non-makeup.png --color_only

# Pattern Only: 
CUDA_VISIBLE_DEVICES=0 python main.py --style ./imgs/style-1.png --input ./imgs/non-makeup.png --pattern_only
```

Result image will be saved in `result.png`

<div style="align: left; text-align:center;">
  <img src="./result.png" alt="result" width="250"/>
  <div class="caption">From left to right: Style, Input & Output</div>
</div>

---

### Training and Evaluation


As stated in the paper, the Color Branch and Pattern Branch are totally independent. Yet, they shared the same workflow:

1. Data preparation: Generating texture_map of faces.

1. Training

Please redirect to [***Color Branch***](./Color) or [***Pattern Branch***](./Pattern) for further details.

---

