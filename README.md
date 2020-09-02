## Introduction

Trex is a tool to match semantically similar functions based on transfer learning. It extends Roberta encoder with masked language modeling objective [1] by supporting multi-field inputs and outputs. It outperforms state-of-the-art tools (e.g., SAFE [2], Asm2Vec [3], Gemini [4], etc.).

## Installation
We recommend `conda` to setup the environment and install the required packages.

First, create the conda environment,

`conda create -n trex python=3.7 numpy scipy scikit-learn`

and activate the conda environment:

`conda activate trex`

Then, install the latest Pytorch (assume you have GPU):

`conda install pytorch torchvision cudatoolkit=10.2 -c pytorch`

Finally, enter the trex root directory: e.g., `path/to/trex`, and install trex:

`pip install --editable .`

## Preparation

### Pretrained models:

Create the `checkpoints` and `checkpoints/pretrain` subdirectory in `path/to/trex`

`mkdir checkpoints`, `mkdir checkpoints/pretrain_all`

Download our [pretrained weight parameters](https://drive.google.com/file/d/18LMUt6xJGTrSJ4HoaXBUYt2le3YNGcOu/view?usp=sharing) and put in `checkpoints/pretrain`

### Sample data for finetuning similarity

We provide the sample training/testing files of finetuning in `data-src/clr_multifield_any`
If you want to prepare the finetuning data yourself, make sure you follow the format shown in `data-src/clr_multifield_any` (coming soon: tokenization script).

We have to binarize the data to make it ready to be trained. To binarize the training data for finetuning, run:

`./command/clr_multifield/preprocess_any.sh`

The binarized training data ready for finetuning (for function boundary) will be stored at `data-bin/clr_multifield_any`

## Training

To finetune the model, run:

`./command/clr_multifield/finetune.sh`

The scripts loads the pretrained weight parameters from `checkpoints/pretrain/` and finetunes the model.

## Comming soon

- Finetuned parameters.
- Tokenization scripts.
- Micro-execution implementation

## References

[1] Liu, Yinhan, et al. "Roberta: A robustly optimized bert pretraining approach." arXiv preprint arXiv:1907.11692 (2019).

[2] Massarelli, Luca, et al. "Safe: Self-attentive function embeddings for binary similarity." International Conference on Detection of Intrusions and Malware, and Vulnerability Assessment. Springer, Cham, 2019.

[3] Ding, Steven HH, Benjamin CM Fung, and Philippe Charland. "Asm2vec: Boosting static representation robustness for binary clone search against code obfuscation and compiler optimization." 2019 IEEE Symposium on Security and Privacy (SP). IEEE, 2019.

[4] Xu, Xiaojun, et al. "Neural network-based graph embedding for cross-platform binary code similarity detection." Proceedings of the 2017 ACM SIGSAC Conference on Computer and Communications Security. 2017.