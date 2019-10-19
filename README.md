# DeepImpute: an accurate and efficient deep learning method for single-cell RNA-seq data imputation

[![Build Status](https://travis-ci.org/lanagarmire/deepimpute.svg?branch=master)](https://travis-ci.org/lanagarmire/deepimpute)

Arisdakessian, Cedric, Olivier Poirion, Breck Yunits, Xun Zhu, and Lana Garmire.  
"DeepImpute: an accurate, fast and scalable deep neural network method to impute single-cell RNA-Seq data.", *Genome biology* 20.1 (2019): 211"
https://genomebiology.biomedcentral.com/articles/10.1186/s13059-019-1837-6?fbclid=IwAR2wkwBbp_rQBv0muKEYlt-MDZGlJF6sej1sbKJOP58jvXX1XdD98aGuauo

DeepImpute has been implemented in Python2 and Python3. The recommended version is Python3.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine.

### Installing

To install DeepImpute, you only need to download the git repository at https://github.com/lanagarmire/deepimpute and install it using pip:

```bash
git clone https://github.com/lanagarmire/deepimpute
cd deepimpute
pip install --user .
```

### Usage

DeepImpute can be used either on the command line or as a Python package.

Command line:

```
usage: deepImpute.py [-h] [-o O] [--cores CORES] [--cell-axis {rows,columns}]
                     [--limit LIMIT] [--minVMR MINVMR] [--subset SUBSET]
                     [--learning-rate LEARNING_RATE] [--batch-size BATCH_SIZE]
                     [--max-epochs MAX_EPOCHS]
                     [--hidden-neurons HIDDEN_NEURONS]
                     [--dropout-rate DROPOUT_RATE]
                     [--output-neurons OUTPUT_NEURONS]
                     inputFile

scRNA-seq data imputation using DeepImpute.

positional arguments:
  inputFile             Path to input data.

optional arguments:
  -h, --help            show this help message and exit
  -o O                  Path to output data counts. Default: ./
  --cores CORES         Number of cores. Default: all available cores
  --cell-axis {rows,columns}
                        Cell dimension in the matrix. Default: rows
  --limit LIMIT         Genes to impute (e.g. first 2000 genes). Default: auto
  --minVMR MINVMR       Min Variance over mean ratio for gene exclusion. Gene
                        with a VMR below ${minVMR} are discarded. Used if
                        --limit is set to 'auto'. Default: 0.5
  --subset SUBSET       Cell subset to speed up training. Either a ratio
                        (0<x<1) or a cell number (int). Default: 1 (all)
  --learning-rate LEARNING_RATE
                        Learning rate. Default: 0.0001
  --batch-size BATCH_SIZE
                        Batch size. Default: 64
  --max-epochs MAX_EPOCHS
                        Maximum number of epochs. Default: 500
  --hidden-neurons HIDDEN_NEURONS
                        Number of neurons in the hidden dense layer. Default:
                        256
  --dropout-rate DROPOUT_RATE
                        Dropout rate for the hidden dropout layer (0<rate<1).
                        Default: 0.2
  --output-neurons OUTPUT_NEURONS
                        Number of output neurons per sub-network. Default: 512```
```

Python package:

```python
from deepimpute.deepImpute import deepImpute

data = pd.read_csv('examples/test.csv', index_col=0) # dimension = (cells x genes)
imputed = deepImpute(data, NN_lim='auto', n_cores=16, cell_subset=1)
```

A more detailed usage of deepImpute's functionality is available in the iPython Notebook notebook_example.ipynb

### Running the tests

Each file has been validated using a unittest script. They are all available in the test folder.
To run all the tests at once, you can also use the makefile by running `make test`.
