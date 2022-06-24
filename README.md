# INVESTIGATING THE GENERALIZATION ABILITIES OF A DEEP LEARNING METHOD
FOR SOUND SOURCE LOCALIZATION USING SMALL-SIZED MICROPHONE ARRAYS

## Description

In this work, we test the ability of a Convolutional Neural Net- 
work (CNN) trained on a specific environmental condition to localize the Direction Of Ar- 
rival (DOA) of a sound source in different settings from the training ones. To this end, we 
generated 3 datasets via simulation techniques that address differ- 
ent acoustic parameters: room volume, microphone array position 
in the room and distance of the source. 

## Prerequisities

**RIRgenerator**: [ehabets/RIR-Generator: Generating room impulse responses (github.com)](https://github.com/ehabets/RIR-Generator)

### Trained models

**Model for resolution 30°**: https://drive.google.com/drive/folders/1vfMAvJECAkNPA6yMZTZlBgEz5T0uRLjF?usp=sharing

**Model for resolution 10°**: https://drive.google.com/drive/folders/1hWLM7Omebq4AG1-U4RkYXROunNbwzj7Y?usp=sharing

## How to use

* Upload in your Drive all the [DATASETS](https://github.com/RobertoAlessandri/CNN_DOA/tree/main/DATASETS) and both the models;

* Save a copy of both notebooks in your Drive

* In each of your notebook change the paths accordingly, in order to find the files in your Drive

* Run "[Various_Room_Tests.ipynb](https://github.com/RobertoAlessandri/CNN_DOA/blob/main/Various_Room_Tests.ipynb)" to check the performance of the CNN

* Use "[Neural_Net_Training.ipynb](https://github.com/RobertoAlessandri/CNN_DOA/blob/main/Neural_Net_Training.ipynb)", to modify the CNN and save new models to test out with "[Various_Room_Tests.ipynb](https://github.com/RobertoAlessandri/CNN_DOA/blob/main/Various_Room_Tests.ipynb)"

* Download "[dataset_gen_livescript.mlx](https://github.com/RobertoAlessandri/CNN_DOA/blob/main/dataset_gen_livescript.mlx)" if you are interested in creating new datasets

## Source Codes

The Matlab script and the two notebooks are based on the paper [_Deep learning assisted sound source localiztion using two orthogonal first-order differential microphone arrays_ [Nian Liu, Huawei Chen, Kunkun Songgong, et al]](https://asa.scitation.org/doi/10.1121/10.0003445).

### Dataset Generator:

[dataset_gen_livescript.mlx](https://github.com/RobertoAlessandri/CNN_DOA/blob/main/dataset_gen_livescript.mlx) generates the dataset for training a Neural Net able to performe source localization. We used rir-generator to simulate the room acoustics.

The script has the following structure:

* Room simulation Parameters  -> Initialization of all the parameters used to simulate the room acoustics;

* Train dataset generation -> To generate the dataset for the training, first we randomly select 300 sentences from the TIMIT/TRAIN dataset. And since we want to reach a dataset size of 6000 datapoints, we locate 1 sentence in 30 different DOAs;

* Validation dataset generation -> Procedure as above, but since we consider 100 sentences, associated to 10 DOAs, we reach a dataset of size 1000

* Test dataset generation  -> We randomly select 10 sentences

* - Test dataset for resolution 10° -> reaches a size of 360,
  
  - Test dataset for resolution  30° -> reaches a size of 120;

* Custom tests -> we generate the datasets for testing the generalization abilities of the NN

* * Receiver position -> we move the experimental strumentation from the center of the room at mid height to top-right corner at floor height,
  
  * Source distance -> we move radially the sources starting from near positions from the microphones' center to far positions,
  
  * Room volume -> we mantain the shape of the room while increasing linearly the three dimensions.

#### Functions

* sourceClass(candidates, target) ->

* extractAudio(fileList, randIndexes, numSelectedSentences, maxDuration, fs) ->

* generateDataset(filepath, audioSamples, numSelectedSentences, DOASxSentence, targetDatasetSize, randomDOAS, res30, res10, sourceCoordinates, c, fs, r, room_dom, T60, n, mytpe, order, dim, orientation, hp_filter) ->

* convAndSave(currentAudio, h, filepath, id, sampleNum, labelDOA30, labelDOA10, fs, maxSamples) ->

### Training Convolutional Neural Network

[Neural_Net_Training.ipynb](https://github.com/RobertoAlessandri/CNN_DOA/blob/main/Neural_Net_Training.ipynb) is subdivided into 4 sections:

1. **Imports and auxiliary functions** where we import libraries and define the core functions for feature extraction
2. **Feature extraction and data exploration** where we plot and play some simulated examples together with the SI features
3. **Training** where we show the learning curves
4. **Testing** where we evaluated the models' performances

**PLEASE NOTE**: The actual training of the neural networks has been performed on a local machine with a GPU. In this Colab we uploaded the training output for easy consultation of the loss and accuracy curves

### Testing CNN's soundness

In [Various_Room_Tests.ipynb](https://github.com/RobertoAlessandri/CNN_DOA/blob/main/Various_Room_Tests.ipynb) we explore the generalization properties of the NNs by testing their ability to adapt to the following conditions:

* **Room volume:** changing room volume while mantaining the same shape
* **Source distance:** changing the distance (radially) of the sources from the microphones
* **Receiver position:** changing the receivers' position by moving it from the center of the room to the top-right corner, near the floor

## Report

A detailed description of our work can be find here: **TODO** put hypertext to the report

## Contacts

* Affatato Giovanni: giovanni.affatato@mail.polimi.it

* Alessandri Roberto: roberto.alessandri@mail.polimi.it
