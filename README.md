# In-The-Wild Dataset Process

This repository contains a Jupyter notebook documenting the steps taken to create the "In The Wild" dataset, now available on Kaggle. The dataset contains real and fake videos for deepfake detection.

## Overview

The dataset was originally sourced from [Deepfake Total](https://deepfake-total.com/in_the_wild). Due to format issues with the downloaded file, additional steps were required to prepare the dataset for upload to Kaggle.

The Jupyter notebook includes:
1. Downloading the dataset
2. Extracting the files
3. Organizing the files into `real` and `fake` folders
4. Uploading the dataset to Kaggle

## Usage

Clone this repository and open the Jupyter notebook to follow the steps taken.

```bash
git clone https://github.com/yourusername/In-The-Wild-Dataset-Process.git
cd In-The-Wild-Dataset-Process
jupyter notebook In_The_Wild_Dataset_Process.ipynb
