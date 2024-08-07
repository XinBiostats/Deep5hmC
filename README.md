# Deep5hmC: Predicting genome-wide 5-Hydroxymethylcytosine landscape via multimodal deep learning model

We develop [__Deep5hmC__](https://www.biorxiv.org/content/10.1101/2024.03.04.583444v1), which is a multimodal deep learning framework that integrates both the DNA sequence and the epigenetic features, to predict genome-wide 5hmC modification. Moreover, __Deep5hmC__ demonstrates its practical usage by accurately predicting gene expression and differentially hydroxymethylated regions in a case-control Alzheimer’s disease study.

<br/>

![Deep5hmC.pdf](figure1.png)


## Installation

1. Download __Deep5hmC__:
```bash
git clone https://github.com/XinBiostats/Deep5hmC
```
2. Requirements: __Deep5hmC__ is implemented in Python. To install requirements
```bash
conda env create -f environment.yml
```
## Usage
We use “Forebrain Organoid” data at the EB stage as our example dataset. Follow the steps below to run the two main models: Deep5hmC-binary and Deep5hmC-cont, in both terminal and jupyter.

### Preparation
1. Download preprocessed data from [Dropbox](https://www.dropbox.com/scl/fo/zbht290yp67yfd1bcvofy/AGG8rFnKJxGTbmrv6uR_RSA?rlkey=3va94r26om8muivxho72wpzpp&dl=1) to './Deep5hmC/data'.
2. Download pretrained models from [Dropbox](https://www.dropbox.com/scl/fo/b8hyeamnojacp04o6hgs1/ACfiArxwvTk-guFqdpshKDA?rlkey=55mtuusluf7o4qpvfrm5p3q5d&dl=1) to "./Deeph5mC/pretrained".
3. Setup "./source/config.json" file.
```
{
  "data_path": "../data",           // Path to the directory where the data is stored
  "weights_path": "../weights",     // Path to the directory where model weights will be saved
  "prediction_path": "../prediction", // Path to the directory where prediction results will be saved
  
  "model_types": "binary", // Types of models to use: "binary","cont","gene","diff"
  "tissue": "EB",                   // Type of tissue being analyzed, in this case, 'EB' (Embryoid Body)
  "histones": ["H3K4me1", "H3K4me3"], // List of histone modifications to be considered in the analysis
  
  "batch_size": 512,                // Number of samples per batch during training
  "lr": 1e-3,                       // Learning rate for training the model
  "num_epochs": 5,                  // Number of training epochs
  "earlystop_thresh": 10            // Number of epochs to wait for improvement before early stopping is triggered
}
```
### In terminal
4. Activate your conda environment 'Deep5hmC' in the terminal.
```bash
conda activate Deep5hmC
```
5. Create .h5 data.
```bash
cd ./source

python create_h5.py config_binary.json

python create_h5.py config_cont.json

python create_h5.py config_gene.json

python create_h5.py config_diff.json
```
6. Run Deep5hmC models.
```bash
cd ./source

python Deep5hmC_binary.py config_binary.json

python Deep5hmC_cont.py config_cont.json

python Deep5hmC_gene.py config_gene.json

python Deep5hmC_diff.py config_diff.json
```

### In Jupyter
We created a demo ([demo.ipynb](https://github.com/XinBiostats/Deep5hmC/blob/main/source/demo.ipynb)) to demonstrate how to use __Deep5hmC__. The results will be displayed inline or saved by users.

# Citation
__Ma X__, Thela SR, Zhao F, Yao B, Wen Z, Jin P, Zhao J, Chen L. Deep5hmC: Predicting genome-wide 5-Hydroxymethylcytosine landscape via a multimodal deep learning model. bioRxiv [Preprint]. 2024 Mar 6:2024.03.04.583444. doi: 10.1101/2024.03.04.583444. PMID: 38496575; PMCID: PMC10942288.
