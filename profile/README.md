<h1 align="center">🔬💻 Robô CeDRI 2024 👾📟</h1>

## Robot Deploy

> ⚠️ The Robot version is linked to the main branch of the repositories, please be aware of just putting production code in it. ⚠️

## Respository Nomenclature

At the start of the repository name the following letters means that the repository is from a specific robot functionality.

- c_ => Conversation Repositories
- m_ => Moviment Respositories
- i_ => Interface Repositories

## Project Repositories:
- [Rasa](https://github.com/Robot-CeDRI/c_chatbot_rasa)
- [LLM-API](https://github.com/Robot-CeDRI/c_llm_api)
- [LLM-FineTuning](https://github.com/Robot-CeDRI/c_llm_fine_tuning)
- [LLM-CedrinhoModel](https://github.com/Robot-CeDRI/c_cedrinho_llm_model)
- [Facial recognition]()
- [Robot Interface](https://github.com/Robot-CeDRI/i_robot_interface)
___
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
