# Information
Contains all code and data used for:
"Mapping relationships between glutathione and SLC25 transporters in cancers using hybrid machine learning models" - Luke Kennedy, Jagdeep K Sandhu, Mary-Ellen Harper, and Miroslava Cuperlovic-Culf.
**bioRxiv doi**: https://doi.org/10.1101/2023.09.20.558442

All code can be run using the packages specified below and data provided in **data** to reproduce the models and results of this work (unless specified otherwise in the main text). Placeholder strings for path directories in the code should be replaced with the path to where ever the data is located on the indivdual's system. Parameters for e.g., ML algorithm or model features can be specified in the code to replicate described models or produce novel models.

**Make your own predictions**: Example files and a brief tutorial are provided at the end under **TUTORIAL** to allow users to implement their own classifier and make predictions using this framework

## classifiers
Contains all python scripts used in data pre-processing, classifier model training, testing, and evaluation used for this work.

## data
Contains all data files used in python code in this repository. 'info.txt' contains specific information for each data file.

## deepGOWeb
Contains all python scripts used for collecting required data (FASTA sequences) for calling DeepGOWeb API, and evaluation of DeepGO annotations and RF classifier annotations.

## structural_analysis
Contains all python scripts used for structural analysis of SLC25 proteins, and for generating corresponding output figures. CAVER was implemented via plugin through PyMol GUI and results are summarized in SLC25_tunnelRes.pkl, generated by mGSH_CAVER_resis.py from CAVER plugin.


## Environment information
The following version of Python and Python packages are used in the code provided here. All code was implemented on Windows with an installation time of 15 minutes. 

Python   --3.8.16

### Scientific programming & machine learning packages
- numpy   --1.23.5
- pandas   --1.5.2
- scikit-learn   --1.2.1
- scipy   --1.10.0

### Plotting packages
- matplotlib   --3.6.3
- matplotlib-venn   --0.11.9
- seaborn   --0.12.2

### Other packages
- pymol   --2.4.1
- pymol-psico   --4.2.2
- requests   --2.28.1

Installation information:
```
pip install numpy
pip install pandas 
pip install scikit-learn   
pip install scipy  
pip install matplotlib  
pip install matplotlib-venn  
pip install seaborn  
conda install -c schrodinger pymol  
conda install -c speleo3 pymol-psico  
pip install requests  

conda install openpyxl 		<- Only necessary for using example generic code "run_model.py"

conda/pip install foo=1.2.3 		<- For installing specific versions
```

## TUTORIAL
For individuals interested in applying this classifier framework to their topic or function of interest, we have provided a generic ```run_model.py``` file which can be run in the command prompt in environments which contain a Python installation with the required packages, for example:
```
python run_model.py --help
```
To get information about the various requirements to run the code.

To run a simple classifier for glutathione metabolism based on a subset of CCLE transcriptomics principal components, unzip **ccleTranscriptomics_PCA.csv** in the **data** folder and, with that and the **exampleGSH_genes.csv** file, enter the following into the command prompt after changing to the directory where these files are located to generate predictions:
```
python run_model.py --data-path "data" --labeled-genes "example_GSHgenes.csv" --feature-data "ccleTranscriptomics_PCA.csv" --select-features 5 --iterations 10 --cpu-cores 2
```
The outputs contain test set results found in the "Results" csv file, and classification probabilites for unlabeld samples are found in the "unknownResults" csv file under "Average predicted label". 

In this example, these classifiers predict annotations for gene ontology terms of interest based on CCLE transcriptomics data, however, this framework and ```run_model.py``` can be used in many applications, such as classifying metabolites based on a metabolomics dataset and a dataset of metabolite biochemical properties. The only requirements are that rows and columns correspond to samples and features/observations, respectively, for use in classifiers and that sample identifiers are consistent across files (e.g., Ensembl gene/transcript IDs, UniProt IDs, Metabolite names).

Simply entering the above command and replacing ```labeled-genes```, ```feature-date```, and possible ```other-features``` with the feature and label data of interest, meeting the aforementioned requirements, is sufficient for generating a novel classifier and predctions.

We hope this code provides an easy implementation of our classification framework which can be used to generate hypotheses for biology! If you encounter and issues or would like to make a suggestion, please [open an issue](https://github.com/lkenn012/mGSH_cancerClassifiers/issues) so it can be addressed.
