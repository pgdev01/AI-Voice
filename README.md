## This project focuses on solving an increasing problem of deepfakes.
These are neural networks, designed to generate photos or sounds. There are many examples of a dangerous usage of deepfakes.

For example, there was an accident of stealing the UK energy company money.\
CEO of the company was tricked by a generated voice of the Hungarian supplier.
## Detailed Project Info
This solution was trained on the AVspoof database. There are 3 text files in the **labels/raw** directory.\
Each line contains speaker's id, sound's id (or a file name if you preffer) and label for a sound (bonafide or spoof).\
Before testing your implementation check the **CONFIG.py** module to make sure, that your parameters are correct.\
By default, you should only take a look on **TRAIN_DIR, VALID_DIR, TEST_DIR**. These are directories containing sound files,\
You need to Fill them with the data.

Module **main.py** contains function **main()** which controls the whole project.

### Here is the list of functions you can easily use in the main() function:
**build_labels_from(dir_name)** - Function reads sound names from **dir_name** parameter in the correct order. After reading sound name, it links to a correct text file in **labels/raw** directory (E-eval.txt, D-dev.txt, T-train.txt). Then it checks by name if sound is spoof (saved as 1) or bonafide (saved as 0). Value 0 or 1 is appended to a list.\
At the same time, value is saved to the text file in **labels/clean** with the data directory name, so later you can use **read_labels_from(txt_file_name)**.\

**read_labels_from(txt_file_name)** - Function simply reads text file located in **labels/clean** created in **build_labels_from** function.\
Each line of text file contains 0 or 1. This function speeds up the data set build process after the first training.

**build_data_from(dir_name)** - function reads sounds from **dir_name** parameter (eg. data/train directory).\
For each sound, it tweaks sound length (sound array) to the value in **CONFIG.py**, applies MFCC sampling and Min Max function.

In **callbacks.py** module I have implemented Model Checkpoint (**MCH** namespace) and Early Stopping (**ES** namespace) keras callbacks.