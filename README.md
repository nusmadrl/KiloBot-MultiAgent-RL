# KiloBot-MultiAgent-RL
This is an experimentation to learn about Swarm Robotics with help of MultiAgent Reinforcement learning. We have used KiloBot as a platform as these are very simple in the actions space and have very high degree of symmetry. The Main inspiration of this project is this paper[[1]](#1)

## Setting Up
``` bash
git clone https://github.com/hex-plex/KiloBot-MultiAgent-RL
cd KiloBot-MultiAgent-RL
pip install --upgrade absl-python \
                      tensorflow \
                      gym \
                      opencv-python \
                      tensorflow_probability \
                      keras \
                      pygame
pip install -e gym-kiloBot
```
This should fetch and install the basics packages needed and should install the environment
### Sample of environment
These envs are running on a constant **Dummy-actions!!**

|**Env with Graph Objective**|Env with Localization Objective|
|--|--|
|![Output-1](images/env_test_graph_compress.gif?raw=true)|![Output-2](images/env_test_localize_compress.gif?raw=true)|

## Usage
``` bash
python env-test.py ## This will help you check the functionality of the environement and should give the sample code to understand the apis as well.
python model-train.py \
        --headless=True \             ## for headless training default False
        --objective="localization" \  ## defines the objective default is graph
        --modules=10 \                ## This defines the no of modules to be initialized default 10
        --time_steps=100000 \         ## This is the total no of steps the agent will take while learning
        --histRange=10 \              ## This is the no of mu values for the histograms
        --logdir="logs" \             ## This specifies the log location for TensorBoard
        --checkpoints="checkpoints"   ## This is for defining the location where the model is to be saved
        --load_checkpoint="checkpoints/iter-500" ## This loads the specified iteration

python play-model.py \ ## This should load trained weights and show the performance
        --load_checkpoint="checkpoints/graphs/10" \ ## loads this model
        --modules=10  \                             ## no of modules in the env
        --objective="localization" \                ## Sets the objective function
        --time_steps=10000 \                        ## No of iterations to be run
        --histRange=10                              ## Same def as above
```
## Results
After a exhaustive amount of training on varies combinations of no_of_modules and task in hand I have obtained results of the following algorithm for these parameters.
I have used ``` [5, 10, 15, 20, 25, 50] ``` number of modules to carryout the tests.

One may find the Tensorboard log files here:

[ log_kilobot [Drive Link] (403MB)](https://drive.google.com/file/d/11NtimYoXOBGopIxziAojti0k1kfbaVBQ/view?usp=sharing)

and the Model Weights for each parameters here:

[ checkpoint_kilobot [Drive Link] (63.3MB)](https://drive.google.com/file/d/12qpbPIOrC-hLGVn2a8GETrkNL89bt8Dt/view?usp=sharing)
#### Graph Problem
The below table is based on the number of modules used but for result tabulation I am considering
``` [5, 10, 20, 50] ```
number of modules. To infer many insights of the algorithm in hand.

|Model Trained on **\** Model Run on|5|10|20|50|
|--|--|--|--|--|
|5|![Failed](images/5trainon5.gif?raw=true)| - | - | - |
|10| - | ![Success1](images/10trainon10.gif?raw=true)|![Success2](images/10trainon20.gif?raw=true)| ![Success3](images/10trainon50.gif?raw=true) |
|20| - | - | ![Random1](images/20trainon20.gif?raw=true) | - |
|50| - | - | - | ![Random2](images/50trainon50.gif?raw=true) |

We can see clearly the policy trained with 10 modules have yield a very good amount of coordination 
#### Localization Problem

## References
<a id="1">[1]</a>
**Guided Deep Reinforcement Learning for Swarm Systems** [[arXiv:1709.06011v1]](https://arxiv.org/abs/1709.06011) [cs.MA] 18 Sep 2017
