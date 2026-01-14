# Behaviour-Model-Data

This repository contains the empirical and simulation trajectories for the Circle Antipode experiments, used to benchmark the performance of various pedestrian dynamics models. The data is organized into folders corresponding to each model, with subfolders for experimental runs.

**Data Format:**

All trajectory data is provided in CSV format. The columns are:

| Column Name        | Description                                                          |
| :----------------- | :------------------------------------------------------------------- |
| PEDESTRIAN_ID      | A unique identifier for each pedestrian.                             |
| FRAME              | The frame number of the video recording (sampling rate is 25fps).    |
| X_COORDINATE       | The horizontal position of the pedestrian (in meters).               |
| Y_COORDINATE       | The vertical position of the pedestrian (in meters).                 |
| RUN_ID (for BM)    | Identifier for the specific experimental run.      |

**Example of a few lines from a .csv file:**
```csv
PEDESTRIAN_ID,FRAME,X_COORDINATE,Y_COORDINATE,RUN_ID
0,0,10.0,9.984,1
0,1,10.0,9.955,1
0,2,10.0,9.913,1
0,3,10.0,9.861,1
0,4,10.0,9.801,1
...
1,0,10.0,9.984,2
...

**Important Note on Coordinate System:** Trajectories within this repository have been rotated to align with a common origin (left) and destination (right) for consistent analysis. Please refer to the accompanying publication for detailed information on the coordinate transformation.

## Models Included:

1.  **EXP (Empirical Data)**
    Description: This folder contains the ground truth trajectory data collected from the controlled circle antipode experiments. It serves as the benchmark against which the simulation models' performances are evaluated.
    Corresponding Experiment Details (as described in the paper): The experiments were conducted in an open square at Beijing Jiaotong University. 64 participants were initialized uniformly on the circumference of a circle with a 10 m radius and tasked with simultaneously navigating to their antipodal positions.

2.  **BM (Behavioral Model)**
    Description: This is the proposed Spatially-Deconstructed Hierarchical Model, which couples tactical route planning with operational collision avoidance using Voronoi-Delaunay motion network. 

3.  **SFM (Social Force Model)**
    Description: A force-driven model representing Newtonian dynamics. Pedestrians are modeled as particles influenced by driving forces towards their destination and repulsive forces from other pedestrians and obstacles.
    Corresponding Literature:
        Helbing, D., & Molnar, P. (1995). Social force model for pedestrian dynamics. Physical Review E, 51(5), 4282–4286.
        Helbing, D., Farkas, I., & Vicsek, T. (2000). Simulating dynamical features of escape panic. Nature, 407(6803), 487–490.

4.  **CPF (Potential Field Cellular Automata)**
    Description: A grid-based model that utilizes an Eikonal equation to compute a cost potential field for global pathfinding.
    Corresponding Literature:
        Zhang, P., Jian, X. X., Wong, S. C., & Choi, K. (2012). Potential field cellular automata model for pedestrian flow. Physical Review E, 85(2), 021119.
        Zhang, P., Li, X.-Y., Deng, H.-Y., Lin, Z.-Y., Zhang, X.-N., & Wong, S. C. (2020). Potential field cellular automata model for overcrowded pedestrian flow. Transportation A: Transportation Sci., 16(3), 749–775.

5.  **DVM (Detour Velocity Model)**
    Description: This model incorporates an explicit utility maximization mechanism to balance path length and travel speed, enabling agents to actively select curved routes and perform detours. 
    Corresponding Literature:
        Xu, Q., Yuan, Z., Guo, R., He, B., & Chraibi, M. (2024). Analysis and modeling of detours in pedestrian operational navigation. Transportation Research Part C: Emerging Technologies, 162, 104584.

6.  **HM (Heuristics Model)**
    Description: A rule-based model that prioritizes heuristic rules for movement. It is a representative of reactive models, focusing on local interactions and immediate responses.
    Corresponding Literature:
        Moussaid, M., Helbing, D., & Theraulaz, G. (2011). How simple rules determine pedestrian behavior and crowd disasters. Proceedings of the National Academy of Sciences, 108(17), 6884–6888.

7.  **PECNet (Predicted Endpoint Conditioned Network)**
    Description: A deep learning model based on a Variational Autoencoder (VAE) that explicitly conditions trajectory generation on known endpoints. It learns statistical distributions from data to generate smooth, socially compliant trajectories. This model was retrained using the specific dataset from our 20 repeated experimental runs for fair comparison.
    Corresponding Literature:
        Mangalam, K., Girase, H., Agarwal, S., Lee, K.-H., Adeli, E., Malik, J., & Gaidon, A. (2020). It is not the journey but the destination: Endpoint conditioned trajectory prediction. In Proceedings of the European Conference on Computer Vision (ECCV) (pp. 759–776). Springer.
