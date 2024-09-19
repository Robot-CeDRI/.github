<h1 align="center">🔬💻 Robô CeDRI 2024 👾📟</h1>


## README Contents:
- [Sync a folder from our repository](#sync-a-folder-from-our-repository)
- [Hardware Setup](#hardware-setup)
- [Navigation](#navigation)
- [Rasa Chatbot](#rasa-chatbot)
- [Facial recognition](#facial-recognition)
- [Interface](#interface)
- [Artificial intelligence](#artificial-intelligence)
- Speech recognition
- Speech generation
___
# Sync a folder from our repository

Step #1: Initialize the Repository
Create a folder where you want to sync your git repo folder and Initialize git
```bash
mkdir tmp && cd tmp && git init
```

Step #2: Add the Remote Repository
Add the remote Git repository with this local git repo as below -
```bash
git remote add origin ssh://git@gitlab.estig.ipb.pt:4589/paulo_leitao/robo_cedri_2023.git
```

Step #4: Enable the Sparse Checkout Properties
Now, we have to enable the Sparse checkout properties and adding the folder name (in our case — ‘any’) in property file which we want to sync.
```bash
git config core.sparsecheckout true

echo any/ >> .git/info/sparse-checkout
```

Step #5: Pull the Specific Folder
This is the last step where we pull the specific folder as below -
```bash
git pull origin main
```

Step #6: List and work with synced directory
```bash
ls -la && cd any
```
---
# Hardware Setup
Equipment and devices used to build the robot:
- Jetson Orin nano 8GB: responsible for processing data related to user interaction, such as chatbot, artificial intelligence and interface.

- Raspberry pi 5: responsible for processing data related to ROS, such as navigation and sensors.

- Hokuyo Lidar: laser sensor that detects the presence of objects at long distances, used for navigation.

- Robot base Magni Silver:Robot structure, controls power supply from Raspberry Pi 5, Lidar and motors.

- Intel camera: checks the position of fiducial markers to aid navigation.

- Raspberry camera: it performs facial recognition and has a built in microphone..

- Display touch 10.1': allows multiple touches and presents a user interface, has a speaker for generating speech.
___
# Navigation

## Useful commands
Commands executed on Raspberyy Pi 5 to use ROS.

Turn on the robot base:
```bash
bas
```
Turn on the Lidar system:
```
las
```  
Initialize the mapping code:
```bash 
track
```
Initialize the navigation code with data input via terminal
```bash
nav 
```

___
# Rasa Chatbot
To see more detailed and accurate information, use the official [Rasa Open Source](https://rasa.com/docs/rasa/) documentation.
## Installation
To install on Windows, Linux or Mac, use the information available in [Rasa installation](https://rasa.com/docs/rasa/installation/environment-set-up/).
### Jetson installation
___
Initially, we will follow the official tutorial step by step. Then, create a virtual environment to isolate your Jetson installation.

```bash 
python3 -m venv ./venv
```

After that, enter the created virtual environment.

```bash 
source ./venv/bin/activate
```

Make sure your pip is on the latest version

```bash 
pip3 install -U pip
```
Finally, install Rasa and if everything goes well, the installation is complete and you can skip the next steps.

```bash 
pip3 install rasa
```
In case of failure, we will start by installing the libraries individually, first tensorflow.

```bash 
pip3 install tensorflow
```
I had an error on the installation of the h5py:

```bash 
ERROR: Could not build wheels for h5py, which is required to install pyproject.toml-based projects
```

To start solving the problem, I updated the system.

```bash 
sudo apt-get update
sudo apt-get upgrade
```

So I tried to update setuptools, my version was the setuptools 44.0.0 and was updateded to 69.5.1.

```bash 
pip install --upgrade setuptools
```
It was necessary install the hdf5, so use the command:

```bash 
sudo apt-get install libhdf5-dev
```

And then h5py was installed.

```bash 
pip install h5py
```

After I tried again to install tensorflow and tensorflow-cpu-aws was with errors. Then I saw that this library is not essential, so I installed tensorflow without it


After spacy.

```bash 
pip3 install spacy
```

In case of failure, we will try to install this library in a different way.

```bash 
python3 -m spacy download en_core_web_md
```

Now, Rasa might be installed withouth any problems, but after that test to see if works properly.

```bash 
pip3 install rasa
```
In my case it worked, I tested the following command to see if everything was ok.

```bash 
rasa shell
```

This command runs rasa, in a previous installation I did there was the problem of running the unknown rasa, but this time it worked well because it responded that it couldn't find the model folder, so I went into the folder that had the model and tested it again and it worked good.

In the folder "Jetson installation" are picutres of some commands used to install in the Jetson nano. The problem encountered was different, mainly involving the scikit-learn library, so I didn't mention it in the tutorial above.

## Useful commands
Activate the virtual environment and then be able to run Rasa:
```bash 
source ./venv/bin/activate
```

Run the chatbot using the command terminal:
```bash
rasa shell
```

Run the chatbot using the interface:
```bash
rasa run -m models --enable-api --cors "*"
```

Run custom actions (must be run in a new terminal):
```bash
rasa run actions
```

Validate the modifications made to the code and check for any errors before training occurs:
```bash
rasa data validate
```

Train a new model based on the last changes made:
```bash
rasa train
```

Run the chatbot in debug mode and check each action it performs:
```bash
rasa interactive 
```
Restart the conversation:
```bash
/restart
```

Leave the conversation:
```bash
/exit
```
___
# Facial recognition

### Libraries installation

To run these files in python you need to install the following libraries:
 - numpy
 ```bash 
        pip3 install numpy
```
 - opencv-python
 ```bash 
        pip3 install opencv-python
```
 - face_recognition
 ```bash 
        pip3 install face_recognition
```

Preferably use the 2023 versions.

__________________________________________________
### Directions:

In the "img" folder, photos of the people you want to be recognized must be placed.

The "engine.py" file analyzes the photos added to the folder. Every time you add a new face to be identified, you need to update the file with the path of the new photos and run the code again so that the new faces are saved in the "rostos_conhecidos.csv" file.

Regarding the "webcam.py" file, this must be executed after "engine.py". The program will start the webcam or other camera you want and compare people's faces with those already registered in the database saved in the file "rostos_conhecidos.csv".

The "webcam_maior_area.py" file works exactly like "webcam.py", but only to identify the person who occupies the largest space in the camera's viewing area. This function is useful for the robot to know who it is talking to in places where there is more than one person.

The "webcam_rasa.py" file has been prepared to integrate with RASA. It works like "webcam_maior_area.py", but prints the name so the robot knows the user's name, instead of displaying recognition to the user.

In the Demo folder there are .gif files demonstrating facial recognition.
_________________________________________________

### Demo: 

* Identifying 1 person using just 1 photo in the database.
<img src="./face_recognition_pedro_lucas/Demo/Apenas1foto.gif" width = "600">

* Identification of multiple people at once. 
<img src="./face_recognition_pedro_lucas/Demo/variaspessoas.gif" width = "600">

# Interface

# Artificial intelligence


# To do
 - Colocar o tutorial de instalação das bibliotecas do Pedro.
 - Colocar o tutorial de instalação do Rasa.
 - Colocar outras informações do robo, tais como hardware, fotos e exemplos.
 - Colocar informações sobre navegação.
 - Colocar tutorial do procedimento para fazer todo o sistema rodar.
