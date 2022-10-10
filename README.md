[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)


## Heart Murmur Detection using Bayesian Convolutional Neural Networks

### Our entry to the George B. Moody PhysioNet Challenge 2022: Heart Murmur Detection from Phonocardiogram Recordings

When using this code, please cite [our paper](https://cinc.org/2022/Program/accepted/355_Preprint.pdf): 

> Benjamin Walker, Felix Krones, Ivan Kiskin, Guy Parsons, Terry Lyons, and Adam Mahdi.
> "Dual Bayesian ResNet: A Deep Learning Approach to Heart Murmur Detection", 
> Computing in Cardiology, 2022.

This repository contains our solution to the first task from the PhysioNet 
Challenge 2022: Design an algorithm to classify the present, absent, or unknown cases 
of heart murmurs from heart sound recordings [1,2].

Two models are implemented:
* A Dual Bayesian ResNet (DBRes), where overlapping log mel spectrograms of the 
heart sound recordings undergo two binary classifications simultaneously: present 
versus unknown or absent, and unknown versus present or absent.
* The output from DBRes integrated with demographic data and signal features 
using XGBoost.

## Data

The challenge dataset can be downloaded via this 
[link](https://physionet.org/static/published-projects/circor-heart-sound/the-circor-digiscope-phonocardiogram-dataset-1.0.3.zip)
or using the following command.
```angular2html
wget -r -N -c -np https://physionet.org/files/circor-heart-sound/1.0.3/
```

## Running Experiments

A full experiment consists of four steps:
1. Splitting the data into stratified train, test, and validation sets (`stratified_data_split.py`).
2. Training the Bayesian ResNets on their respective binary classification tasks (`train_resnet.py`).
3. Calculating and evaluating the output from DBRes (`dbres.py`).
4. Calculating and evaluating the output from DBRes with XGBoost integration (`xgboost_integration.py`).

These steps can be run independently using the relevant script, or sequentially using `main.py`,
```angular2html
CUDA_VISIBLE_DEVICES=0 python main.py --full_data_directory physionet.org/files/circor-heart-sound/1.0.3/training_data --stratified_directory data/stratified_data --vali_size 0.2 --test_size 0.2 --random_state 14 --recalc_features --spectrogram_directory data/spectrograms --model_name resnet50dropout --recalc_output --dbres_output_directory outputs
```

## Affiliations

Ben Walker<sup>1</sup>, Felix Krones<sup>2</sup>, Ivan Kiskin<sup>3,4</sup>, 
Guy Parsons<sup>5</sup>, Terence Lyons<sup>1</sup>, Adam Mahdi<sup>2,3</sup>

1. The Mathematical Institute, University of Oxford, Oxford, UK, 
2. The Oxford Internet Institute, University of Oxford, Oxford, UK, 
3. The People-Centred AI Institute, University of Surrey, Surrey, UK, 
4. The Surrey Sleep Research Centre, University of Surrey, Surrey, UK, 
5. The Intensive Care Registrar, Thames Valley Deanery, NIHR Academic Clinical Fellow at University of Oxford, Oxford, UK.

## Acknowledgment

This work was supported by the Hong Kong Innovation and Technology Commission (InnoHK Project CIMDA).

## References

When using this code, please cite [1].

[1]: Walker B, Krones F, Kiskin I, Parsons G, Lyons T, and Mahdi A. 
"Dual Bayesian ResNet: A Deep Learning Approach to Heart Murmur Detection", 
Computing in Cardiology, 2022.

[2] Reyna MA, Kiarashi Y, Elola A, Oliveira J, Renna F, Gu
A, et al. "Heart murmur detection from phonocardiogram
recordings: The George B. Moody Physionet Challenge 2022".