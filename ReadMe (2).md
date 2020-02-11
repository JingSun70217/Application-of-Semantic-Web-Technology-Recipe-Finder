﻿# Yolo Object Detector


## Installation
1.	Install Visual Studio Code (https://code.visualstudio.com/).  
2.	Install the Python Extension for VS Code from the Visual Studio Marketplace (https://code.visualstudio.com/docs/python/python-tutorial).  
3.	Install a Python interpreter  
Install Python 3.7 or Python 3.8 (https://www.python.org/downloads/).   
Please choose “add path to env” when install python, or setting the path manually to your environment.  
5. Start VS Code in a project (workspace) folder  
Open the repository folder in VS Code. That folder becomes your "workspace". VS Code stores settings that are specific to that workspace in **/.vscode/settings.json**. Python path can also be set here.  
6. Select a Python interpreter  
Tell VS Code which interpreter to use in order to run Python code and get Python IntelliSense. (https://code.visualstudio.com/docs/python/python-tutorial)  
7. Install Python packages  
    tensorflow\==1.14.0, opencv, pyqt5, lxml, keras==2.2.4, pillow, matplotlib  


## Running the Whole Process Automatically

Please run main.py in VS Codes directly.   

The output path will be created if it is not existing. After that, each step will be executed automatically. The process will only pause at the second step (annotation). Users can annotate objects by using labelImg tool when labelImg.py is executed. The next steps will be continue executed after closing labelImg GUI.


## Repository Architecture

### .vscode
**launch.json**: Configure the debugger. A variable number of arguments have been passed to functions by configure workspace and args. 

### panorama_Input
Store input images / panorama.

### Codes
The codes part of this repository.   
- **configuration**  
Configure related path and parameters before running codes. 
>Annotation and preprocessing (**anno_preprocess_cfg.json**),  
Training (**train_cfg.json**),   
Prediction (**predict_cfg.json**),  
**labels.txt**

- **label**  
Repository of labelImg tool. Annotate bounding boxes and labels for equalized images. 

- **preprocess**  
Data preprocessing by getting annotated path and generating anchors.  
>**yolo_voc_annotation_to_txt.py**  
**generate_anchor.py**  
**\_\_init__.py**  

- yolo3  
Contain Yolov3 framework which be used in both training and prediction parts.   
>**weights**:  (**trained_mix.h5** and **yolov3.h5**)  
**font**: **FiraMono-Medium.otf** is a font file is used to run scripts with a different font. Please don’t delete this folder. Otherwise, the program will terminate with "OSError: cannot open resource" which is a bug in Pillow on Windows with paths containing non-ASCII characters.  
**voc_classes.txt**: classes of objects  
**yolo.py**  
**units.py**  
**models.py**  
**\_\_init__.py**  

- **entzerren.py**  
Map images from spherical projection to cylindrical projection. Equalize a panorama in to several small images.  
- **train.py**  
- **predict.py**  
- **trained_weights_pre_train.h5**  
 Pre-trained model  
- **\_\_init__.py**  
Used to mark the directory as Python package directories. Import functions from other python files will be easier with the help of it.  

### outputs
Outputs of all the steps.   

- **panorama_entzert**  
Outputs of the first step (Euqalization). Equalize cylindrical projected panorama into small images.   

- **anno_preprocess**  
Outputs of annotation and preprocessing steps.  
 **anno_xml**  
 Outputs of labelImg tool. Annotated image files in xml format.   
**anno_yolo**  
 Outputs of “yolo_voc_annotation_to_txt.py”. Generate   **train_annotation_path.txt** and **test_annotation_path.txt**  
**yolo_anchors.txt**  
Outputs of “generate_anchor.py”. This is one of the input paths of training and  prediction parts.  
- **train**  
**checkpointFiles**  
Checkpoints capture the exact value of all parameters (tf.Variable objects) used by a model.  
**models**  
Final trained model: **trained_weights_final.h5**  
**train_logs**  
events.out.tfevents.XXXXXXX files are used to store summary output. This information is not essential for training and can therefore be deleted. But it might come in handy for debugging or studying behavior of the model after deletion.  
- **prediction**  
              The predicted images are stored in this folder. Objects are marked by bounding boxes, label and confidence.
### \_\_pycache_\_
The interpreter compiles the program to bytecode first and stores it in the \_\_pycache\_\_ folder. It can make your program start a little faster. But you can also ignore it.

