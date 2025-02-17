# In-The-Wild Dataset Process

This repository contains a Jupyter notebook documenting the steps taken to create the "In The Wild" dataset, now available on Kaggle. The dataset contains real and fake audios for deepfake detection.

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
```

## Kaggle Links
- [In The Wild Dataset on Kaggel](https://www.kaggle.com/datasets/abdallamohamed312/in-the-wild-audio-deepfake/data).
- [In The Wild Dataset Process Notebook on Kaggel](https://www.kaggle.com/code/abdallamohamed312/in-the-wild-preparation/notebook?scriptVersionId=187680056).

## Steps Followed

### 1. Downloading the Dataset 
- The dataset was downloaded form [Deepfake Total](https://deepfake-total.com/in_the_wild).

### 2. Extracting the Files 
- The downloaded file had no extension, which caused issues during extraction. 
```bash
!unzip /kaggle/input/in-the-wild-dataset/download -d /kaggle/working
!ls /kaggle/working/
```
### 3. Organizing the Files 
- After extraction, we separated the files into real and fake folders based on their content.
```python
def process_files(folder_path, csv_path):
    # Sort files in the folder
    files = sorted(os.listdir(folder_path))
    
    # Read CSV file into a DataFrame
    df = pd.read_csv(csv_path)
    
    # Iterate over sorted files
    for filename in files:
        if filename.endswith('.wav'):
            file_id = os.path.splitext(filename)[0]  # Extract file ID from filename
            file_id_with_extension = filename  # Get file ID with extension for printing
            
            # Get label from DataFrame based on file ID
            label = df.loc[df['file'] == file_id_with_extension, 'label'].values[0]
            
            # Create folder for label if it doesn't exist
            label_folder = os.path.join(folder_path, label)
            os.makedirs(label_folder, exist_ok=True)
            
            # Move file to corresponding label folder
            source_file = os.path.join(folder_path, filename)
            destination_file = os.path.join(label_folder, filename)
            shutil.move(source_file, destination_file)
            print(f"Moved {filename} to {label_folder}")
    print("Data split completed successfully!")

folder_path = '/kaggle/working/release_in_the_wild'
csv_path = '/kaggle/working/modified_meta.csv'
process_files(folder_path, csv_path)
```
### 4. Creating the kaggle dataset from the outputs of the notebook
- Finally, the organized dataset was uploaded to Kaggle. You can find the dataset and notebook links above.

## Contibutors
- [Abdalla Mohammed](https://github.com/Abdalla312)
- [Mohammed Abdeldayem](https://github.com/abdeldayem02)
- We welcome contributions! Please feel free to submit pull requests or open issues for any suggestions or improvements.

## Licence

- This project is licensed under the Apache License, Version 2.0. License - see the LICENSE file for details.




