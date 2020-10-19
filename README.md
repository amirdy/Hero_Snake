# Smart_Snake
In this project, Agent(snake) learns how to play the game<sup>1</sup>.
The game board is 12&times;12 and the learning algorithm is DQN.
###### Average scores : 20
###### Best achieved score : 49



<table>
  <tr>
    <td> <img src="./README_Files/sample1.gif"  alt="gif1" width = 500px height = 250px ></td>
    <td> <img src="./README_Files/sample3.gif"  alt="gif2" width = 500px height = 250px></td>
   </tr> 
   <tr> 
      <td align="center"><b>score = 49</b></td>
      <td align="center"><b>score = 49</b></td>
  </tr>
</table>


<table>
  <tr>
    <td> <img src="./README_Files/sample2.gif"  alt="gif1" width = 330px height = 150px ></td>
    <td> <img src="./README_Files/sample3.gif"  alt="gif2" width = 330px height = 150px></td>
    <td> <img src="./README_Files/sample0.gif"  alt="gif3" width = 330px height = 150px></td>
   </tr> 
   <tr> 
      <td align="center"><b>score = 48</b></td>
      <td align="center"><b>score = 46</b></td>
      <td align="center"><b>score = 43</b></td>
  </tr>
</table>



# Algorithm

|<img src="README_Files/Algorithm1.png"  height="400" width="500" > | 
|:--:| 
| *DQN Pseudo Code (https://storage.googleapis.com/deepmind-media/dqn/DQNNaturePaper.pdf)* |


###### Q = Q<sub>&theta;</sub> = Action-Value Function = Policy network
###### Q<sup>^</sup> = Q<sub>&theta;<sup>-</sup></sub> = Target Function = Target network
### Note:

#### The implementation has some differences with the above algorithm:

1. ##### The training (calculating loss and updating the weights) doesn't apply on the first 2000 steps<sup>3</sup>.
   - ###### Because there is not enough samples in the replay memory<sup>3</sup>.

2. ##### Target Network updates every C episodes (not every C steps)<sup>4</sup>.

# Network
#### Input Data :
###### &nbsp; **(Batch_size, 8)**

#### Layers  : 
###### &nbsp; **FC(1024)** &rarr; **ReLU** &rarr; **FC(1024)** &rarr; **ReLU** &rarr; **FC(512)** &rarr; **ReLU** &rarr; **FC(4)** 

# State
### s<sub>t</sub> : 
&nbsp; The frame of the game after t transitions which converts to a 12&times;12 np array.
##### Example:
|<img src="README_Files/frame_sample_1.png"  height="300" width="500" > | 
|:--:| 
| Frame |

|<img src="README_Files/matrix.png"  height="300" width="500" > | 
|:--:| 
| (12 &times; 12) Np array |

### &phi;(s<sub>t</sub>) :
&nbsp; Based on the <b>Assignment4</b> of the [Artificial Intelligence (CS 440/ECE 448) course](https://courses.engr.illinois.edu/cs440/sp2019/mp4/index.html) course<sup>2</sup>,
8 features extracted from the frame as below:
##### &nbsp; [Adjoining_wall_x, Adjoining_wall_y, food_dir_x, food_dir_y, Adjoining_body_top, Adjoining_body_bottom, Adjoining_body_left, Adjoining_body_right]

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ![equation](./README_Files/feature1.svg)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ![equation](./README_Files/feature2.svg)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ![equation](./README_Files/feature3.svg)
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ![equation](./README_Files/feature4.svg)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ![equation](./README_Files/feature5.svg)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ![equation](./README_Files/feature6.svg)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ![equation](./README_Files/feature7.svg)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ![equation](./README_Files/feature8.svg)
#### &phi;(s<sub>t</sub>) for the previous example:
&nbsp;&nbsp;&nbsp;![equation](./README_Files/features.png)

# Hyperparameters
- #### C: 
   - ###### 10
- #### &gamma;: 
   - ###### 0.99
- #### Batch size : 
   - ###### 128
- #### actions : 
   - ###### (Left, Right, Up, Down) ~ (0, 1, 2, 3)
- #### Rewards : 
   - ###### (Reward<sub>Food</sub> , Reward<sub>Loose</sub> , Reward<sub>Move</sub>) ~ (100, -100, -0.1)
- #### N (Replay Memory Size) : 
   - ###### 50000
- #### M (Number of Episodes) : 
   - ###### 30000
- #### Learning rate : 
   - ###### 0.001
- #### Optimizer : 
   - ###### RMSprop
   
# Result 

##### Plots:
|<img src="README_Files/Train.png"  height="260" width="370" > | <img src="README_Files/Test.png"  height="260" width="370" > | 
|:--|--:| 
| <b><div align="center"><sub>Train</sub><div></b> |<b><div align="center"><sub>Test</sub></div></b> |

#### Notices :
###### &nbsp;&nbsp; Training finished in ~ 209 Minutes on Tesla V100-SXM2-16GB (using Google Colab Pro).
###### &nbsp;&nbsp; Test Result: &nbsp;&nbsp;<b>Mean(scores)</b> : 20.257&nbsp;&nbsp;|   <b>Std(scores)</b> : 6.50




# References
[1]  [Wikipedia - Snake (video game genre)](https://en.wikipedia.org/wiki/Snake_(video_game_genre))

[2]  [CS440/ECE448 Spring 2019 Assignment 4: Reinforcement Learning and Deep Learning (UNIVERSITY OF ILLINOIS URBANA-CHAMPAIGN)](https://courses.engr.illinois.edu/cs440/sp2019/mp4/index.html)

[3]  [https://www.diva-portal.org/smash/get/diva2:1342302/FULLTEXT01.pdf](https://www.diva-portal.org/smash/get/diva2:1342302/FULLTEXT01.pdf)

[4]  [PyTorch - REINFORCEMENT LEARNING (DQN) TUTORIAL](https://pytorch.org/tutorials/intermediate/reinforcement_q_learning.html)
# Useful Resources
[Mnih, V., Kavukcuoglu, K., Silver, D., Graves, A., Antonoglou, I., Wierstra, D., & Riedmiller, M. (2013). Playing atari with deep reinforcement learning. arXiv preprint arXiv:1312.5602.](https://www.cs.toronto.edu/~vmnih/docs/dqn.pdf)

[AI learns to play SNAKE using Reinforcement Learning (Square Robots)](https://www.youtube.com/watch?v=8cdUree20j4)

[How to automate Snake using Reinforcement Learning (DeKay Arts)](https://www.youtube.com/watch?v=RMTfNPKnxhk)

[https://github.com/YuriyGuts/snake-ai-reinforcement/](https://github.com/YuriyGuts/snake-ai-reinforcement/)

[https://github.com/benjamin-dupuis/DQN-snake](https://github.com/benjamin-dupuis/DQN-snake)


 
