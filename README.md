# Smart_Snake


# State
### s<sub>t</sub> : 
The last game frame 
### &phi;(s<sub>t</sub>) :
8 features extracted from the frame as below:


![equation](https://latex.codecogs.com/svg.latex?%5Cfn_cs%20%5Csmall%20%5Ctext%7BAdjoining%5C_wall%5C_x%7D%3D%5Cbegin%7Bcases%7D%200%2C%20%26%20%5Ctext%7Bno%20adjoining%20wall%20on%20x%20axis%7D.%5C%5C%201%2C%20%26%20%5Ctext%7Bwall%20on%20snake%20head%20left%7D.%20%5C%5C%202%2C%20%26%20%5Ctext%7Bwall%20on%20snake%20head%20right%7D.%20%5Cend%7Bcases%7D)
# Network
#### Input Data :
###### **(Batch_size, 9)**

#### Layers  : 
###### **FC(1024)** &rarr; **ReLU** &rarr; **FC(1024)** &rarr; **ReLU** &rarr; **FC(1024)** 
