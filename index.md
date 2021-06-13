## Welcome to the Official Site of SpeCollate

SpeCollate is the first Deep Learning-based peptide database search tool. It allows you to search a peptide database by generating embeddings for both mass spectra and peptides and then performs the search process on GPU.

SpeCollate is available as a standalone executable that can be downloaded and run on a Linux server with a Cuda-enabled GPU.

Two different executables are included in the downloadable specollate.tar.gz file; 1) specollate_train for retraining a model and 2) specollate_search for performing database search using a trained model. A pre-trained model is provided within the download file.

The below sections separately explain the setup for training and search operation. You can skip the training section if you only intend to use SpeCollate for database search.

## Prerequisites

- Linux server with Ubuntu 16.04 (or later) or CentOS 8.1 (or later).
- At least 120GBs of system memory and 10 CPU cores.
- Cuda enabled GPU with at least 12 GBs of memory. Cuda Toolkit 10.0 (or later).
- OpenMS tool for creating custom peptide database. (Optional)
- Crux for FDR analysis using its percolator option.

## Training

1. Download the [specollate.tar.gz](https://drive.google.com/uc?export=download&id=1iAR4a6qQQyS2pDFMRqCd7Jaofsmxwdsp) file and extract the contents using the following command:  
`tar -xzf specollate.tar.gz`  
The extracted directory contains multiple files, including:
    - `specollate-train`: This is the executable for training SpeCollate.
    - `specollate-search`: This is the executable for database search.
    - `config.ini`: Parameter file for training and searching.
    - `models (dir)`: Contains the pre-trained model. New models will also be stored here.
    - `percolator (dir)`: Percolator input (.pin) files be placed here after the search is complete.

2. Download the preprocessed data for training ([here](https://drive.google.com/uc?export=download&id=10bZbMdc2eN_l4ToJd6ruzNX7t6wIUfHw)) and extract the contents using:  
`tar -xzf specollate-training-data.tar.gz`

3. Open the config.ini file from step 1 in your favorite text editor and set the following parameters:
    - `in_tensor_dir` in [preprocess] section: Absolute path of the decompressed file from step 2.
    - `model_name` in [ml] section: The name by which to wish to save the trained model file.
    - other parameters in the [ml] section: You can adjust different hyperparameters in the [ml] section, e.g., learning_rate, dropout, etc.

4. Execute the specollate_train file.  
`./specollate_search`

5. Once the training is complete; the trained models can be found in the `/models` directory. Note that models are saved as `model-name-epoch_id.pt` after every epoch. Make sure to delete any unwanted model files after the training is done.

## Search

1. Same as step 1 in the **Training** section.
2. Download the [mgf file](https://drive.google.com/uc?export=download&id=1vMGda5UpIziyIW3dDmNSWpjeE3w6SmM8). Or you can use your own spectra files in mgf format.
3. Download the [human peptide database](https://drive.google.com/uc?export=download&id=1pOBYkCFl66Yk1DjSIw6l9RRi7f6iSXSf). You can provide your own peptide database file created using the Digestor tool provided by [OpenMS](https://www.openms.de/download/openms-binaries/).
4. Set the following parameters in the [search] section of the `config.ini` file:
    - `model_name`: Name of the model to be used. The model should be in the `/models` directory.
    - `mgf_dir`: Absolute path to the directory containing mgf files to be searched.
    - `prep_dir`: Absolute path to the directory where preprocessed mgf files will be saved.
    - `pep_dir`: Absolute path to the directory containing peptide database.
    - `out_pin_dir`: Absolute path to a directory where percolator pin files will be saved. The directory must exist; otherwise, the process will exit with an error.
    - Set database search parameters e.g. `precursor_mass_tolerance` etc.

5. Once the search is complete; you can analyze the percolator files using the crux percolator tool:
```shell
cd <out_pin_dir>
crux percolator target.pin decoy.pin --list-of-files T --overwrite T
```


If you use our tool, please cite our work:  
`Place holder for citation`

For questions, suggestions, or technical problems, contact:  
<mtari008@fiu.edu>

